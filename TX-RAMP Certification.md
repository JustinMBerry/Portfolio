## Summary
Collaborated with a team of Infrastructure administrators to achieve compliance with the TX-RAMP certification. Played a key role in the overhaul of Active Directory groups across multiple domains, implementing a comprehensive overhaul to enforce the principle of least privileged access for users.

## Process
Documented daily file and folder usage by specific groups to restrict access to unnecessary files.

## PowerShell Scripts Used
### Group Membership Removal
```
$usernameFile = "*Directory to list of usernames*"
$users = Get-Content $usernameFile

ForEach ($user in $users) {
    Remove-ADGroupMember -Identity *AD Group Name* -Members $user -Confirm:$False
}
```
#### Script Summary
This PowerShell script removes users from a selected Active Directory group by reading a list of usernames from a specified file. Customize the script by filling in the information between the asterisks (*). Ensure the Active Directory group name and the file path are accurately provided for proper execution.

$usernameFile = "*Directory to list of usernames*"

    Provides the path to the file containing a list of usernames.

$users = Get-Content $usernameFile

    Imports the list of usernames into Powershell.

ForEach ($user in $users) {Remove-ADGroupMember -Identity *AD Group Name* -Members $user -Confirm:$False}

    Runs a For loop through the user list, removing all users on the list from teh listed Group.
