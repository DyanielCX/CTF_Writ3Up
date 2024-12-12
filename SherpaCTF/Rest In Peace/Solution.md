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

Unfortunately, I can't find the usage of the decrypted flag variables and stuck at here for a long period during the competition Q~Q

Suddenly, my teammate ask me "have I view the source code in assemble code form?" Yea true, I forget view it in diassembly

In diassembly form, I found all the variables that related to the flag
![image](https://github.com/user-attachments/assets/9adc5040-9266-4981-a029-45631573742d)
![image](https://github.com/user-attachments/assets/4be00adf-eeb5-4bba-b72e-b6e25a4101b5)

And when I change it show in the graph form, the logic/condition of the program become clearer

In the last three line, the system set `dword [rbp+0x4]` as **0x1**, compare it again with **0x1** and jump to the display flag section if not equal.
This situation will cause the program definitely unable run the flag display part
![image](https://github.com/user-attachments/assets/e6a1ce7f-3e06-4225-8a61-4cc709732c81)

What's idea from our group to bypass/modify this condition is using the patch feature of binary ninja invert the jump condition 
from **jne(jump not equal)** to **je(jump equal)** to make the program move to the flag display section
![image](https://github.com/user-attachments/assets/1d240929-ca0a-422c-aeb6-f5ec44a10352)
![image](https://github.com/user-attachments/assets/5df4d673-df9d-4127-a516-91877bb3ef20)

After this, export the modified program and run it in the window command prompt and you will get the first part of the flag
![image](https://github.com/user-attachments/assets/242c223c-b284-4dbc-95dd-140c07a3820f)

Using the same method in the end of the first flag display section, you give get the second flag
![image](https://github.com/user-attachments/assets/947c0f76-3bd7-46f7-8e4a-cf088e89f237)
![image](https://github.com/user-attachments/assets/a2970314-2ff8-4bee-8433-a0af5ab2e1e8)
![image](https://github.com/user-attachments/assets/287a2cd3-593d-40e1-ac98-7a1dd6a1ce5d)

Combine both part of the flag, Congrats you have get the flag for this challs HURRAY!!! (>⁠ω<)"

 ### Flag: SHCTF24{n0b0dy_c4n_dr46_m3_d0wn_1337}

**ps: This is the way that how I solve this challenge. In between maybe there is some part with wrong information. 
If you find it, welcome come to tell me anytime. I will update it with the correct information**
