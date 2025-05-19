This is still a work in motion. You will see notes to myself in (). Never got to test in production. Once confirmed will update:


# Connect securely to Exchange Online
Connect-ExchangeOnline -UserPrincipalName youradmin@yourdomain.com

# Set threshold for stale mailboxes (180 and 365 days)
$threshold180 = (Get-Date).AddDays(-180)
$threshold = (Get-Date).AddDays(-365)

# Fetch all shared mailboxes and their last logon time (maybe should be # Retrieve shared mailboxes and fetch LastLogonTime)
$mailboxes = Get-Mailbox -RecipientTypeDetails SharedMailbox -ResultSize Unlimited | ForEach-Object {
    $stats = Get-MailboxStatistics $_.Identity
    [PSCustomObject]@{
        DisplayName        = $_.DisplayName
        PrimarySmtpAddress = $_.PrimarySmtpAddress
        LastLogonTime      = $stats.LastLogonTime
    }
}

# Export all shared mailboxes
$mailboxes | Export-Csv -Path "C:\SharedMailboxActivityReport_All.csv" -NoTypeInformation

# Export only inactive shared mailboxes (365+ days inactive or never accessed)
$mailboxes | Where-Object {
    $_.LastLogonTime -lt $threshold -or $_.LastLogonTime -eq $null
} | Export-Csv -Path "C:\SharedMailboxActivityReport_Stale.csv" -NoTypeInformation

Write-Output "Shared Mailbox reports exported successfully to C:\" (should maybe create a folder and change path (which would also change 16 and 20))
