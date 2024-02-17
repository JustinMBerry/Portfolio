## Summary
Collaborated with a team of Infrastructure administrators to achieve compliance with the TX-RAMP certification. Played a key role in the overhaul of Active Directory groups across multiple domains, implementing a comprehensive overhaul to enforce the principle of least privileged access for users.

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
This script queries a list of usernames, and removes those users from the selected group.

Iterate through each username and remove them from the specified Active Directory group

$usernameFile = "*Directory to list of usernames*"
Provide the path to the file containing a list of usernames
