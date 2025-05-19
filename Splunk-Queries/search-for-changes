index=* "*xxxxxx*" EventCode="642" OR EventCode="4738" | rex "(?ms)A user account was changed.+?Display Name:\s(?<wanted_user>\V+)" | table _time Display_Name Account_Name ComputerName     (x equals name)

