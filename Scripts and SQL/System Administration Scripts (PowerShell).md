# Off-Hours System Health Monitor Script
### Develop a script to monitor mulitple servers during non-business hours while maintaining detailed health reports. Automatically track system performance patterns and generate a comprehensive report across multiple systems without manual intervention.

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