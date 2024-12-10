## Introduction

**Challenge: Rest In Peace**

**Level: Easy**

**Category: Reverse Engineering**

**Author: BM5**

<img width="373" alt="Screenshot_2" src="https://github.com/user-attachments/assets/39f2786b-cb21-4ebb-a7d4-e48fb8d0b9d4">

## Solution
From the challenge, we will given a executable file. I try to run it first in the window command prompt and I get some seem "useless" message...?
![image](https://github.com/user-attachments/assets/da8cbb43-4ccc-472d-8f83-1b59cd22b937)

Then we move to RE this exe file with Binary Ninja

Since just now this program got show a message. So, I find the program user entry point with the message content
![image](https://github.com/user-attachments/assets/f4f0aaab-a2f4-4615-aa6a-45146ebb1602)
![image](https://github.com/user-attachments/assets/a9e0c867-dfff-4ac4-a882-ed216ef5ce5c)

At here, I see some important things about the flag. From the variable declaration, the flag has been break into two parts and both of the parts of flag
have been encrypted.
![image](https://github.com/user-attachments/assets/8494456a-f816-44a6-aa13-ef2ab28dfb5b)

And all of these variables are been called in the main function. So next I have move to view the main function code which is the entry point
![image](https://github.com/user-attachments/assets/2f536ea6-f123-4467-b0b9-8c38ccc9e11f)

Unfortunately, I stuck at here for a long period during the competition Q~Q

