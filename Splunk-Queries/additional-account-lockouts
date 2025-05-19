index=* source=WinEventLog:Security LogName=Security Account_Name=xxxxxxx ("4625" OR "4740" OR "4771" OR "4777")

index=wineventlog * * source="WinEventLog:Security" EventCode="4776"  user=xxxxxx | table _time, EventCode, Account_Domain, user, dvc, Caller_Computer_Name 

(x equals username)
