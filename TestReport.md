# Test that all the functionality works as expected

<details>
<summary> Quiz Dashboard </summary>

| Functionality | Result | Description | Pictures |
|---------------|--------|-------------|----------|
| Check that an admin can create quiz | ✅ |  | <img width="1330" height="419" src="https://github.com/user-attachments/assets/65f89f83-79ba-43e8-8bc5-5a315e471cc2" /><br><img width="926" height="299" src="https://github.com/user-attachments/assets/6425f4ea-1ace-42cc-8b6e-079ffd5a917b" /> |
| Check that score decrease cant be a negative number | ❌ | It was able to set scoreDecrease to a negative number, this is bad since in my app I subtract. So if it’s 2 negatives the number will be positive, fixed now though | <img width="985" height="701" src="https://github.com/user-attachments/assets/4d43e158-cd23-42cb-85c0-d7b52a770e34" /> |
| Editing quizes | ✅ | works | |
| Deleting quizes | ✅ | works | |
| Make sure edit quizes doesnt show up for users | ✅ | works | |
| Check that a quiz cannot be created without question, answer, or category | ❌ | doesnt work | <img width="347" height="344" alt="image" src="https://github.com/user-attachments/assets/cf007477-ade2-4c77-b200-cc1127f94a8b" /> |
| New row inserts into quizAttempts | ✅ | works | <img width="753" height="114" alt="image" src="https://github.com/user-attachments/assets/204934c1-cf38-4345-bc3c-08c87faf743b" />|

</details>

<details>
<summary> quiz page </summary>
  
| Functionality | Result | Description | Pictures |
|---------------|--------|-------------|----------|
| cant go next without answering | ✅ | works, button disabled | <img width="1246" height="433" src="https://github.com/user-attachments/assets/37356eb9-d56d-4642-803a-7ca9b5febd39" /> |
| cant spam next button | ✅ | works, button dissapears |  |
| Wrong answers light up, and right answers light up | ✅ | works | <img width="1284" height="602" src="https://github.com/user-attachments/assets/c9205328-6d7a-409f-b92a-c83f561135b8" /> |
| Score increases and decreases depending on answer | ✅ | works |  |
| Check final point score | ✅ | is correct | <img width="568" height="631" src="https://github.com/user-attachments/assets/de72bdf3-9694-458c-85be-b455e2c6126f" /> |
| Retrying and going back to dashboard buttons work | ✅ | works |  |
| See Diploma | ✅ | works, shows up and correct points | <img width="736" height="174" src="https://github.com/user-attachments/assets/9b5390c4-46d5-4f3f-8dd9-d077d5f4dd84" /> |
</details>

###### (I Realize I have a few mistakes/functionality improvments, will try to fix as many as I can)
