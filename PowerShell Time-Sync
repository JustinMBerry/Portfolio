# Windows Time-Sync PowerShell Script

## Summary
This script was used in office after an office move left us unable to access a domain controller for a period of time.

## PowerShell Script
```
$w32tmOutput = w32tm /stripchart /computer:time.google.com /samples:1 /dataonly /packetinfo
$TimestampLine = ($w32tmOutput | Select-String "Transmit Timestamp: (.*)").Matches.Groups[1].Value
$Current_Time = ($TimestampLine | Select-String " - (.*PM)") | ForEach-Object { $_.Matches.Groups[1].Value }
if($null -eq $Current_Time)
    {
    $Current_Time = ($TimestampLine | Select-String " - (.*AM)") | ForEach-Object { $_.Matches.Groups[1].Value }
    }

Set-Date -Date $Current_Time
```

## Explanation
$w32tmOutput = w32tm /stripchart /computer:time.google.com /samples:1 /dataonly /packetinfo
      - Runs w32tm command to retrieve the time servers information “time.google.com” in this example.

$TimestampLine = ($w32tmOutput | Select-String "Transmit Timestamp: (.*)").Matches.Groups[1].Value

      - Sets an object named “TimestampLine” to the transmit Timestamp.

$Current_Time = ($TimestampLine | Select-String " - (.*PM)") | ForEach-Object { $_.Matches.Groups[1].Value }

      - Sets an object named “Current_Time” by removing all other information from TimestampLine other then the current Date/Time.

if($null -eq $Current_Time)
    {
    $Current_Time = ($TimestampLine | Select-String " - (.*AM)") | ForEach-Object { $_.Matches.Groups[1].Value }
    }

      - Determines if Date/Time is AM or PM to avoid a Null object.

Set-Date -Date $Current_Time 

      - Ends the script by setting the computer's Date/Time to the stored value.
