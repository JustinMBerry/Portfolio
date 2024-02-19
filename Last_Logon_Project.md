# Last Logon Script Project

## Summary
This PowerShell script lists all users who still have AD accounts that are active, and have not logged in for 365 days.

## PowerShell Script
```
$Exited_Users_List = Get-ADGroupMember -Identity ExitedUsers | select SamAccountName
$Enabled_Old_Accounts = Search-ADAccount -AccountInactive -TimeSpan 365.00:00:00 | Where {$_.Enabled -eq "True" -and $_.ObjectClass -eq "User"}

$Enabled_Old_Accounts | ?{$Exited_Users_List -notcontains $_.samaccountname} | Export-CSV *Directory Location + File Name* -NoTypeInformation -Append
```

## Explanation
`$Exited_Users_List = Get-ADGroupMember -Identity ExitedUsers | select SamAccountName`
    
  Creates an object called Exited_Users_List that contains the Username for all members of the ExitedUsers group in Active Directory

`$Enabled_Old_Accounts = Search-ADAccount -AccountInactive -TimeSpan 365.00:00:00 | Where {$_.Enabled -eq "True" -and $_.ObjectClass -eq "User"}`

  Creates an object called Enabled_Old_Accounts that contains a list of all users who's accounts are flagged as currently Enabled, and who have not logged in for at least 365 days.

`$Enabled_Old_Accounts | ?{$Exited_Users_List -notcontains $_.samaccountname} | Export-CSV *Directory Location + File Name* -NoTypeInformation -Append`

  Takes the object Enabled_Old_Accounts, and pipes it into a where-object, where it removes all accounts that are currently a member of the ExitedUsers group. It then Exports that object to a .csv file to the directory listed in place of *Directory Location + File Name.* (If there is a current file with the samee name in that location it will append to the end of the document.
