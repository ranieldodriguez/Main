## Create an Automation Script for XSOAR that will lookup a User and a Users Manager within Active Directory

```python
# Retrievces a command / script arguments dict, and then we can 'get' the argument from that dict
email = demisto.args().get("email")

# get the user details, using the email argument
user = demisto.executeCommand("ad-get-user", {"email": email})

# get the rawjson Contents of the executeCommand, so we can utilize it.
user = user[0].get("Contents")

# get the manager details, using the DN of the Manager
# as well as grabbing the Contents from the reponse, so we can utilize it.
manager = demisto.executeCommand("ad-get-user", {"dn": user.get("attributes").get("manager") [0]})[0]["Contents"]

# create our own "Contents" to be reutrend by this automation
result = {
	"UserName": user.get('attributes').get('displayName')[0],
	"UserEmail": user.get('attributes'.get('mail')[0],
	"UserGroups": user.get('attributes').get('memberOf')[0],
	"UserSamAccountName": user.get('attributes').get('sAMAccountName')[0],
	"ManagerName": manager.get('attributes').get('displayName')[0],
	"ManagerEmail": manager.get('attributes').get('mail')[0]
}

# table to markdown to creats a clean war room entry with a dictionary list or a list of the same dictionaries
readable = tableToMarkdown("Active Directory User and Manager Details", result, headers=["UserName", "UserEmail", "UserGroups", "UserSamAccountName", "ManagerName", "ManagerEmail"])

# command results creates the object for return_results
# readable_output = human reable markdown that will be used for the war room entry
# outputs_prefix = The Context Key that the results will be placed under in context
# outputs_key_field = The key in the result that will be used to determine if the exisint item already exists in Context, if so it will update
# outputs = the raw data, in this case the "result" dict from above
# ingore_auto_extract = When set to True, disables auto-extract on the results from this command (default is False)
results = CommandResults(
	readable_output = readable,
	outputs_prefix = 'ADUserandManager',
	outputs_key_field = "UserName",
	outputs = result,
	ingore_auto_extract = True
	)

return_results(results)
```

## Implement a Field Change Script, which will pause the Time to Assignment Timer if an Owner is assigned, and start again if an Owner is unassigned

```python
# This script pauses the Time to Assignment when an Onwer is assigned to an Incident, and starts the Remediation SLA Timer.
# If the Incident is unassigned, then it resumes the Time to Assignment, and pauses the Remedation SLA!

if not demisto.args().get('old') and demisto.args().get('new'): # If owner was no-one and is now someone:
	demisto.executeCommand("pauseTimer", {"timerField": "timetoassignment"})
	demisto.executeCommand("startTimer", {"timerField": "remediationsla"})
	return_results("Assignment of the incident was successful, Time to Assignment has been stopped and the Remedation timer has been started.")
	
if demisto.args().get('old') and not demisto.args().get('new'): # If the owner was someone and is now no-one:
	demisto.executeCommand("pauseTimer", {"timerField": "remedationsla"})
	demisto.executeCommand("startTimer", {"timerField": "timetoassignment"})
	return_results("Incidnet has been unassigned, unpausing Time to Assignment, and pausing Remediation timer")
```

## Prevent a User from being able to modify fields

```python
# get the user who is making the change, and the ID/Username from that user
user = demisto.args().get("user").get("id")

if user != "DBot":
	return_error(f"Dear {user}, You do not have the appropriate permissions to change this field.")
```

## Use a Field display script to change how a Field displays on the New/Edit form in XSOAR

```python
# check if this is a new Incident or not
incident = demisto.incident().get("id")

# if new Incident, the ID will be empty:
if not incident: 
	# get the XSOAR list
	types_list = demisto.executeCommand("getList", {"listName":"DisplayIncidentTypes"})[0]["Contents"].split(",")
	
	# strip whitespace
	types_list = [ x.strip() for x in types_list ]
	
	# return the options to display to the user
	return_results({'hidden': False, 'options': types_list})
else:

	#get the current Incident Type, and only return that type. Preventing the type from being easily changes after creation!
	incident_type = demisto.incident().get("type")
	return_results({'hidden': False, 'options': [incident_type]})
```

## Use an SLA script to take action when the SLA for a Timer is breached

```python
# This script will complete tasks with the timebreach tag value upon timer breach
# Add this as the script upon breach on the given timer field.
# Playbook tasks to complete beed to be tagged timerbreach.

incident = demisto.incident().get('id')
demisto.executeCommand("taskComplete", {"id":"timerbreach", "incidentId":incident})
```

## Create a pair Automation scripts that will be used to dynamically display data on Incident Layouts

```python
# requires an XSOAR list that contains a markdown table with links to import Analyst Tools (wikis, google, etc)
tools_listname = "XETAnalystTools"

# get the list
tools = demisto.executeCommand("getList", {"listName":tools_listname})[0]['Contents']

# check if the list exists
if "Item not found" in tools:
	return_results(f"Tools list appears to be missing, make sure to create the '{tools_listname}' List")
else:
	result = CommandResults(readable_output=tools, ignore_auto_extract = True)
	return_results(result)
```

```python
# requires an XSOAR list that contains the response process for the given Incident Type, and a default list as a fallback
default_response_process_list = "DefaultResponseProcess"
incident_type = demisto.incident().get("type")

# get the list for the IncidentType
response_process = demisto.executeCommand("getList", {"listName":f"{incident_type} Response Process")[0] ['Contents']

# check if the list exists
if "Item not found" in response_process:
	response_process = demisto.executeCommand("getList", {"listName": default_response_process_list})[0]['Contents']
	result = CommandResults(readable_output = response_process, ignore_auto_extract = True)
	return_results(result)
else:
	result = CommandResults(readable_output = response_process, ignore_auto_extract = True)
	return_results(result)
```

## Implement a post processing script, that prevents our Incident from being closed without an Owner being assigned, or the Close Notes being fill out appropriately. 

```python
# Post processing script that returns an error if the Owner isn't assinged as long as the closingUserId isn't DBot.
# If the closingUserId is DBot, this is likely coming from the closeInvesigation task within the playbook, we will allow this.

# get the incident owner, and the closingUserId
owner = demisto.incident().get('owner')
closing_user = demisto.args().get("closingUserId")

return_results(f"The closing user is {closing_user}") # for testing

if not owner and closing_user != "DBot":
	return_error("An Owner must be assigned before closing this Incident")
	
if owner != closing_user and closing_user != "DBot":
	return_error("You are not the owner of this ticket, you do not have the appropriate permission to close it.")
	
if not demisto.args().get("closeNotes") and closing_user != "DBot":
	return_error("Please fill out closing notes with Who, What, When, Where, Why")
```