Use for finding shared mailbox information per user.

Get-Mailbox -ResultSize Unlimited | Get-MailboxPermisson -User xxxxxxx | Where-Object { $_.AccessRights -like "*FullAccess*" } | Select-Object Identitiy    
(x equals username)
