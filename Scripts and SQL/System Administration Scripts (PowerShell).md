# Off-Hours System Health Monitor Script
### Develop a script to monitor mulitple servers during non-business hours while maintaining detailed health reports. Automatically track system performance patterns and generate a comprehensive report across multiple systems without manual intervention.

```powershell
# Script Name: Off-Hours-System-Health-Monitor.ps1
# Author: Daniel Rodriguez
# Created: January 8, 2025
# Last Edited: January 8, 2025
# Description: Monitors system health during off-hours and generates CSV reports

# Define server names and IPs
$servers = @(
    "PROD-SRV01" = "192.168.1.10"
    "APP-SRV02" = "192.168.1.11"
    "DB-SRV03" = "192.168.1.12"
    "WEB-SRV04" = "192.168.13"
)

# function to check if current time is within off-hours
function Test-OffHours {
    param (
        [DateTime]$currentTime
    )

    # get current day of week
    $dayOfWeek = $currentTime.DayofWeek

    # Define off-hours criteria
    switch ($dayOfWeek) {
        # Monday through Thursday: 7pm - 6am
        {$_ -in "Monday", "Tuesday", "Wednesday", "Thursday"} {
            return ($currentTime.Hour -ge 19) -or ($currentTime.Hour -lt 6)
        }
        # Friday: After 8 pm
        "Friday" {
            return ($currentTime.Hour -ge 20)
        }
        # Saturday and Sunday: All day
        {$_ -in "Saturday", "Sunday"} {
            return $true
        }
    }
    return $false
}

# Function to test network latency
function Test-NetworkLatency {
    param (
        [string]$serverName,
        [string]$serverIP
    )

    $pingResults = Test-Connection -ComputerName $serverIP -Count 4 -ErrorAction SilentlyContinue
    if ($pingResults) {
        return ($pingResults | Measure-Object -Property ResponseTime -Average).Average
    }
    return $null
}

# Function to get system shutdown count
function Get-SystemShutdowns {
    param (
        [string]$serverName
    )

    $shutdowns = Get-WinEvent -ComputerName $serverName -FilterHastable @{
        LogName = 'System'
        ID = 1074 #Event ID for system shutdown
        StartTime = (Get-Date).AddHours(-24)
    } -ErrorAction SilentlyContinue
}

# Function to check for large data transfers
function Get-LargeDataTransfers {
    param (
        [string]$serverName
    )

    # Define threshold for large transfers (in bytes)
    $threshold = 100MB

    # Check network interface statistics
    $networkStats = Get-WmiObject -ComputerName $serverName -Class Win32_PerfFormattedData_Tcpip_NetworkInterface | Where-Object {$_.BytesTotalPersec -gt $threshold}

    return $networkStats.Count -gt 0
}

# Main monitoring function
function Start-HealthMonitoring {
    $currentTime = Get-Data

    if (-not (Test-OffHours -currentTime $currentTime)) {
        Write-Host "Not in off-hours period. Monitoring not required."
        return
    }

    $results = @()

    foreach ($server in $servers) {
        $latency = Test-NetworkLatency -serverName $server
        $shutdowns = Get-SystemShutdowns -serverName $server
        $largeTransfers = Get-LargeDataTransfers -serverName $server

        $result = [PSCustomObject]@{
            Timestamp = $currentTime
            Server = $server
            NetworkLatency = $latency
            NetworkStatus = if ($latency -gt 55) {'RED'} else {'GREEN'}
            ShutdownCount = $shutdowns
            ShutdownStatus = if ($shutdown -gt 0) {'RED'} else {'GREEN'}
            LargeDataTransfers = $largeTransfers
            ReportingPeriod = "Off-Hours"
        }
        $results += $result
    }
    #Generate CSV report
    $reportPath = "C:\Reports\SystemHealth_$(Get-Date -Format 'yyyMMdd').csv"
    $results | Export-Csv -Path $reportPath -NoTypeInformation

    Write-Host "Health monitoring completed. Report generated at: $reportPath"
}

# Run the monitoring
Start-HealthMonitoring

```

# Local System Health Check Script
### Perform quick, on-demand diagnostic checks on indivual machines when troubleshooting issues. Provide immediate feedback  to quickly berify a single system's health status. 

```powershell
# Script Name: Local-System-Health-Check.ps1
# Description: Performs immediate system health check and displays results

# Define local system parameters
$computerName = $env:COMPUTERNAME
$localIP = (Get-NetIPAddress -AddressFamily IPv4 - InteraceAlias "Ethernet*" | Select-Object -First 1).IPAddress

# Function tog et system performance metrics
function Get-SystemMetrics {
    $cpu = (Get-Counter '\Processor(_Total)\% Processor Time' -SampleInterval 1 -MaxSamples 1).CounterSamples.CookedValue
    $memory = Get-Counter '\Memory\% Commited Bytes in Use' -SampleInterval 1 -MaxSamples 1
    $disk = Get-Counter '\LogicalDisk(_Total)\% Free Space' -SampleInterval 1 -MaxSamples 1

    return @{
        CPUUsage = [math]::Round($cpu, 2)
        MemoryUsage = [math]::Round($memory.CounterSamples.CookedValue, 2)
        DiskSpace = [math]::Round($disk.CounterSamples.CookedValue, 2)
    }
}

# Function to check recent system events
function Get-RecentSystemEvent {
    $events = Get-WinEvent - FilterHashtable @{
        LogName = 'System'
        Level = 1,2,3 #Error, Warning, Information
        StartTime = (Get-Date).AddHours(-1)
    } -MaxEvents 5 -ErrorAction SilentlyContinue

    return $events
}

# Function to check network status
function Test-LocalNetwork {
    $pingResults = Test-Connection -ComputerName "8.8.8.8" -Count 4 -ErroAction SilentlyContinue
    return ($pingResults | Measure-Object -Property ResponseTime -Average).Average
}

#Main Function
function Start-LocalHealthCheck {
    Write-Host "`n=== Local System Health Check ===" -ForegroundColor Cyan
    Write-Host "Computer Name: $computerName"
    Write-Host "Local IP: $localIP"
    Write-Host "Timestamp: $(Get-Date)`n"

    # Get system metrics
    $metrics = Get-SystemMetrics
        Write-Host "--- System Metrics ---" -ForegroundColor Green
        Write-Host "CPU Usage: $($metrics.CPUUsage)%"
        Write-Host "Memory Usage: $($metrics.CPUUsage)%"
        Write-Host "Free Disk Space: $($metrics.DiskSpace)%`n"

    # Check network connectivity
    $networkLatency = Test-LocalNetwork
    Write-Host "--- Network Status ---" -ForegroungColor Green
    if ($networkLatency) {
        Write-Host "Internet Connectivity : OK"
        Write-Host "Average Latency : $([math]::Round($networkLatecny, 2))ms`n"
    } else {
        Write-Host "Internet Connectivity: FAILED`n" - ForegroundColor Red
    }

    # Get recent system events
    Write-Host "--- Recent System Events ---" -ForegroundColor Green
    $events = Get-RecentSystemEvents
    if ($events) {
        foreach ($event in $events) {
            $levelColor = switch ($event.Level) {
                1 { "Red" } # Error
                2 { "Yellow" } # Warning
                3 { "White" } # Information
                default { "Gray" }
            }
            Write-Host "[$($event.TimeCreated)] $($event.LevelDisplayName): $($event.Message.Split([Environment]::NewLine[0]" -ForgroundColor @levelColor))
        }
    } else {
        Write-Host "No significant events in the past hour"
    }
    Write-Host "`n=== Health Check Complete ===`n" -ForegroundColor Cyan
}

# Run the health check
Start-LocalHealthCheck

```



```powershell

```