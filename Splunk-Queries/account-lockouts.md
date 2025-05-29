index=wineventlog * * source="WinEventLog:Security" EventCode="4740"  user=xxxxxxx | table _time, EventCode, Account_Domain, user, dvc, Caller_Computer_Name    (x equals username)
