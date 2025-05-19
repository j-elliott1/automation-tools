index="*" earliest=-180d latest=now() source=WinEventLog:Security

(Group_Name="Domain Admins")

(EventCode=4728 OR EventCode=4729 OR EventCode=4732 OR EventCode=4733 OR EventCode=4756 OR EventCode=4757)

| eval Time=strftime(_time, "%m/%d/%y %H:%M:%S") | sort -_time

| eval EventCode=case(EventCode==4728, "4728 [+] GG Sec", EventCode==4729, "4729 [-] GG Sec", EventCode==4732, "4732 [+] DL/BL Sec", EventCode==4733, "4733 [-] DL/BL Sec", EventCode==4756, "4756 [+] UG Sec", EventCode==4757, "4757 [-] UG Sec", 1=1, EventCode)

| rex "Subject:\s+[^\n]+\s+Account Name:\s+(?<ActionBy>.*)" | rex "Subject:\s+[^\n]+\s+[^\n]+\s+Account Domain:\s+(?<ActionByDomain>.*)"

| rex "Member:\s+\w+\s\w+:\s+(?<Member>.*)" | rex "Member:\s+Security ID:[^\n]+\s+Account Name:\s+(?<MemberDN>.*)"

| rex "Group:\s+[^\n]+\s+Group Name:\s+(?<Group>.*)" | rex "Group:\s+[^\n]+\s+[^\n]+\s+Group Domain:\s+(?<GroupDomain>.*)"

`comment("4756 uses 'Account', not 'Group'")` | rex "Group:\s+[^\n]+\s+Account Name:\s+(?<Group>.*)" | rex "Group:\s+[^\n]+\s+[^\n]+\s+Account Domain:\s+(?<GroupDomain>.*)"

| rename ComputerName as "Computer", name as "EventDescription"

| table Time, GroupDomain, Group, EventCode, Member, MemberDN, ActionBy, ActionByDomain, Computer, EventDescription
