index=* source="WinEventLog:Security" (EventCode=4720 OR EventCode=624)
    | eval CreatedBy = mvindex(Account_Name,0) 
    | eval New_User = mvindex(Account_Name,1) 
    | search CreatedBy=*
    | table _time EventCode CreatedBy New_User

OR


index=* source="WinEventLog:Security" (EventCode=4720 OR EventCode=624)      | eval CreatedBy = mvindex(Account_Name,0)       | eval New_User = mvindex(Account_Name,1)       | search CreatedBy=*       New_User=xxxxxxx      (x equals username)
