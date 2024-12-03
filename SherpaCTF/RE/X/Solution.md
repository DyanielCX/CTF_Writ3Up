## Introduction

**Challenge: X**

**Level: Medium**

**Author: Dell**

<img width="373" alt="Screenshot_2" src="https://github.com/user-attachments/assets/893fa778-fe6c-4371-90fc-759b40d7792c">

## Solution
From the challenge, we get a execatable file. So first I try run the program.

This program is a white window with a **X** word and two tabs, **File** and **Help**. In the `File` tab, the only option is **exit** which will direct quit the window.

![image](https://github.com/user-attachments/assets/3a67cedf-f69b-4996-9009-070c5c47d17e)
![image](https://github.com/user-attachments/assets/b24495bd-75ec-49b2-9e39-6226a440c7f8)

While in the `Help` tab, there is a **about ...** option. When clicking about, a window will pop that seem like a flag checker. 
That's all the information that we can get by running the program.

![image](https://github.com/user-attachments/assets/25b6649a-95ed-4d22-916b-e0abc7229050)
![image](https://github.com/user-attachments/assets/cc2a191b-ff1e-49fd-8637-6240eed69e45)
![image](https://github.com/user-attachments/assets/c96ad758-83eb-4bec-b0ab-7335c755d981)

<p>&nbsp;</p>

Next, we move to diassembly the executable file with the binary ninja and try to find the flag checker part.

Since just now we have get a error message when key in a wrong flag. So, I try to use the find feature in binary ninja to 
search the flag checker section with the message content and the `sub_140001000()` function (flag checker window) is found.
![image](https://github.com/user-attachments/assets/90960636-3e53-4e5c-b699-dd233a277597)
![image](https://github.com/user-attachments/assets/211ad3b6-0d50-480d-98f6-32c1cec78b19)

In this section, I see two functions that might important - `GetDlgItemTextA()` & `SendMessageA()` because I guess the condition for checking maybe in one of them.
When double click `GetDlgItemTextA()` and `SendMessageA()`, these functions seem like only used for read and return the user input without any condition for checking.
![image](https://github.com/user-attachments/assets/f5a8d57a-74d3-4c79-bdd5-4d57df8bec53)
![image](https://github.com/user-attachments/assets/a0634e37-35cd-446b-bc94-db87ab979ad6)
![image](https://github.com/user-attachments/assets/4fe9a562-a650-4559-a61d-0f6dfddd0fb7)

<p>&nbsp;</p>

At this moment, I notice there is a function inside the `SendMessageA()` function. 
When go to the function, yes I think this is what I wonna to find -> **The Flag Checking Condition**
![image](https://github.com/user-attachments/assets/f2625204-a0db-4b57-b8f7-eafe6803bc4f)
![image](https://github.com/user-attachments/assets/713c87dc-f9db-40a2-877e-ceb55b327db5)

After reading the code, I understand that the condition is set in "When the user input in ASCII decrement by 1 is not equal to the provided string, 
the system will display the error message like what we have demo before this".

** **&s = user input**
![image](https://github.com/user-attachments/assets/00c0bd19-f28b-410f-952b-6a53715ac336)

Based on the condition,I copy the the provided string and one by one increment them and get a new string.

#### How the increment process:
![image](https://github.com/user-attachments/assets/e1a3d189-923c-4a56-af1d-05edc3c2f204)
![image](https://github.com/user-attachments/assets/14a9dd40-5b1e-4776-a7fb-491ea5e289c4)

Here we try to insert the new string with the flag format into flag checker and it is correct >w<!!!
![image](https://github.com/user-attachments/assets/ccd6af1d-d9f7-4321-8aec-c4be173271ed)
![image](https://github.com/user-attachments/assets/cc2c59cd-7bb8-4456-b8b8-51e7bf44b04f)

### Flag: SHCTF24{cdc5df19b407428c78ae9ae69f7f2fac}

**ps: This is the way that how I solve this challenge. In between maybe there is some part with wrong information. 
If you find it, welcome come to tell me anytime. I will update it with the correct information**
