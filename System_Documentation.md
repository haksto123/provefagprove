# System Documentation

<details>
<Summary> Technology </Summary>

- Omega has built in security, so its easy to get started.
- Also Omega has a lot of built in components which makes it a lot easier than rather having to make them myself
- Omega's framework uses, vue.js, Bootstrap, and Microsoft SQL server, which are very good tools for creating apps, a good backend

- I started using word for my documentation, but decided to switch to github since its easier to share, and people who get access can easily see new updates to my documentation

- I used drawSQL to create my table structure
</details>

<details>
  <summary>Architecture</summary>


  <details>
    <summary>Table Setup</summary>

  [Table Setup](https://drawsql.app/teams/hocus/diagrams/quiz-app)

  </details>


  <details>
    <summary> Views </summary>

| View Name | Description | Pictures |
|-----------------------|------|-------|
| aviw_HaakonStokkenes_Quizes  | This view exists because I need a connection between quizcateogries table and the quiz table  |  <img width="731" height="168" alt="image" src="https://github.com/user-attachments/assets/f7c9332e-3671-4e3a-84c4-0dfda990a3cf" />
| aviw_HaakonStokkenes_MyPermissions  | This view exists because of security reasons, if a person does not have the role "quiz developer" I don't want the tab "Edit quizes" to render in my app. This tab is only avaliable for quiz admins | <img width="1047" height="213" alt="image" src="https://github.com/user-attachments/assets/8bdecc43-e582-45f5-b89b-1e8b7d761e7b" />
| aviw_HaakonStokkenes_QuizScoreboard  | This view is for showing the results in the scoreboard tab, binds to system users so it shows the score each person has | <img width="569" height="359" alt="image" src="https://github.com/user-attachments/assets/11de7fe0-1120-45d2-be41-8dd81842e3ca" />

  </details>

  <details>
  <summary>Procedures</summary>

| Procedure Name | Description | Pictures |
|----------------|-------------|----------|
| astp_HaakonStokkenes_SaveQuizAttempt | This proc executes at the end of a quiz so that the users attempt shows up in the scoreboard. The reason I have the set session context is becuase in my insert trigger I check on sviw_System_MyAccessTables and if that table has allowEdit = 1 the transaction continues. BUT a normal user shouldnt have the ability to insert new rows so the allowEdit for users is set to 0. So I set the session context only in the procedure so the insert trigger check skips. so normal users will be allowed to insert a new record for the scoreboard. | <img width="712" height="246" alt="image" src="https://github.com/user-attachments/assets/e4f819d0-7aa6-4635-8add-835ed1b02efa" />

  </details>

</details>



<details>
<summary> Security </summary>
The webiste authentication happens through Omega365CTP (Core Technology Platform). When users visit the site they immediately get met with a login page. Here you can choose between logging in with microsoft, or use SQL-Login by writing their Mail/Phone number and password.
If the user chooses microsoft, the authentication happens internally at microsoft and it returns a token thats connected to the user in the system.

In Omega365, access control is configured through access tables. Users are assigned roles, and each role defines which modules the user has access to. 
The modules contain information about which applications the user can use and which tables they are allowed to retrieve data from.
It is also specified whether the user has permission to edit data (AllowEdit) or delete data (AllowDelete). In addition, roles can include capabilities, which are more granular permissions that grant users specific types of access.
Every role that is assigned must be linked to an OrgUnit.

# OrgUnits
The orgunits are built around a hierarchy where all orgunits will have a parent orgunit. These orgunits can be different types, for example Company, Contract, Project etc. 
To get access to data a user needs to have role in an orgunit.
Inheritance grants access to underlying OrgUnits (orgunit descendants). By default, users inherit access downwards the OrgUnit hierarchy. 
This means that if you have a role assigned in a higher-level OrgUnit, you automatically have the same role in all OrgUnits beneath it.

Orgunits can also have "DoNotInherit" enabled in the orgunit settings. For these OrgUnits, having a role assigned in a higher level of the hierarchy is not enough. 
Only users with a role assigned directly to the DoNotInherit OrgUnit will be granted access.

# Context
Users also have a orgunit context they can choose to be in. Users will only see data depending on which orgunit they stand in and data in the underlying orgunits. 

### OrgUnit hierarchy example:

<img width="991" height="710" alt="image" src="https://github.com/user-attachments/assets/1d0cdb80-6984-4924-a407-ebb9241cf1ae" />

# Table security
For making sure that not everyone has access to every table, there exists views called atbv's that automatically get created when you make a new table.
These atbv's contain a whereclause that you can use to control who should have access to your table.
Then you can create an aviw that collects the data from the atbv so you can keep the security check. (you can also just use the atbv, but if you need columns from other tables you need to create an aviw)

There should also be a custom security check in the triggers for extra security.

- In my case I have created security checks in both the triggers and the atbv's. So anyone without the quiz user or the quiz admin roles will not have access to this app, and tables. Aswell as anyone without quiz admin will not be able to see the edit quiz tab, or insert into the tables.
  
</details>

<details>
  <summary>App Structure</summary>

See the [User Manual](https://github.com/haksto123/provefagprove/blob/main/User_Manual.md) for a quick walkthrough.

</details> 

