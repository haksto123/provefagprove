# System Documentation

<details>
<Summary> Technology </Summary>

- Omega has built in security, so its easy to get started.
- Also Omega has a lot of built in components which makes it a lot easier than rather having to make them myself
- Omega's framework uses, vue.js, Bootstrap, and Microsoft SQL server, which are very good tools for creating apps, and a good backend

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
| astp_HaakonStokkenes_SaveQuizAttempt | This proc executes at the end of a quiz so that the users attempt shows up in the scoreboard. | <img width="704" height="250" alt="image" src="https://github.com/user-attachments/assets/9a87a796-109d-4a1f-bbb6-28027574f68b" />

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

# Triggers

- All my trigger have a check on sviw_System_MyAccessTables where it checks if AllowEdit = 1 (or AllowDelete = 1 for delete triggers)

  <img width="641" height="122" alt="image" src="https://github.com/user-attachments/assets/ffe341c0-32da-43c4-874d-90dd41fbd7ce" />

- In the quiz attempts insert trigger is the only place where I have an extra check which is 
  <img width="620" height="135" alt="image" src="https://github.com/user-attachments/assets/2a032c38-4b3f-4f0f-8298-8207306f09fd" />

- I have this as an extra check because a person shouldnt be able to insert into other peoples data.

</details>

<details>
  <summary>App Structure</summary>

See the [User Manual](https://github.com/haksto123/provefagprove/blob/main/User_Manual.md) for a quick walkthrough.

---------------------------------------------------------------------
The total amount of apps I have created is 4. One for the quiz dashboard (main page). One for the quiz itself. One for the result screen, and one for the setup app for categories.
Quiz Overview, scoreboard, and the ability to edit quizes are all in the same app (quiz dashboard).
When you click "start quiz", you will be sent to the quiz page with a the corresponding Quiz_ID
After youve clicked and answered a questionm you will get immidiate feedback on if it was wrong or right, or points will then increase or decrease depending on if it was right.
Then you will be sent to the Results page after all questions have been answered, your quiz attempt will be saved and stored in the quiz scoreboard page of the dashboard.

I have made all the frontend using vue (typescript) and styled with mostly custom CSS, but I also use bootstrap.

</details> 

<details>
<summary> Twist </summary>
  I got presented a twist throughout my development of the app, the twist was to add categories to each quiz, and be able to sort by categories.
  I did this by making a new category table, and adding a new column in the quizes table called Category_ID that links to the category table, then I linked the category table and quiz table together in a view.
  
  In my app I made a selectedCategory variable, and a filteredquizes variable containing a filter that checks if the selectedCateogry is equal to quiz.data category.
  Then instead of looping through the quiz data raw, I loop through the filteredQuizes variable.
</details>

<details>
<summary> Challenges during development </summary>
  
### Permissions for quiz user   
- Struggeled with figuring out how I could get a normal quiz user to insert into the quiz attempts table, they need to be able to do this since the procedure inserts a new row.
- In my triggers I have check on sviw_System_MyAccessTables if AllowEdit = 1 (and AllowDelete = 1 on the delete triggers)

#### Solution
I thought the best solution would be to set the session context before the procedure fires to 1. Then in my trigger skip the security check if session_context was = 1
Realized this was way less secure since skipping the trigger isnt the best security... So I switched the security by just setting allowEdit=1 on the quizattempts table for the Quiz_User module.

### Adding a new category
First I thought I could insert a new row in the dropdown of the categories in the edit quiz tab, this wasnt possible since the categories are joined in the view by using a category_ID and the category was owned by a different table
#### Solution
I made a new app called Quiz Categories setup and added it to the O365 setup app. Made a new menu group for quiz setup that is only avaliable for the quiz admin where you can insert edit and delete categories.
  
</details>

<details> 

<summary> Missed functionality </summary>

- instead of creating a seperate view for MyPermission I could have created a new capibility if a person is an admin (would be a cleaner check I think) but I didn't have time to change this as of writing.
</details>

<details>
<summary> extra functionality I didnt have time for </summary>
  
- Adding a timer where if you answer a question very fast you would get more points
- Adding different answer types (multiple answers, text answers etc)
</details>
