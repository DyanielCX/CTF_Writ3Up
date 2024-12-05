## Introduction

**Challenge: IN MY HEADDD**

**Level: Easy**

**Category: MISC**

**Author: PLZ ENTER TEXT**

<img width="373" alt="Screenshot_2" src="https://github.com/user-attachments/assets/00485984-8898-449b-9d18-5c086328cf5a">

## Solution
In the description, we can see a [youtube clip link](https://www.youtube.com/clip/UgkxrLa5UkwGkGiDT3IZoZUS6jDORSAjrCiQ?si=JKvLpTN-mHsA4snO) with a song.... 
"**IN YOUR HEADDDD~ IN YOUR HEADDD~ Zombiee Zombiee~~**" ^O^

Besides, this challenge also has provide a pcapng file. So as normal will open it with **Wireshark**

![image](https://github.com/user-attachments/assets/5038cbff-47a5-4f74-9751-c5e26b29845e)

I have do some checking and analysis on this file with the built-in features in statistic tab. When come to check the *conservartion*, 
I find a suspicious situation which is the large amount of packet transfer between `10.10.1.13` and `10.10.1.9`, with the total 82

![image](https://github.com/user-attachments/assets/c4cc0133-e0ab-498e-b676-ca6ffb7af0dd)
![image](https://github.com/user-attachments/assets/4b7b7812-d9a4-49cc-98f2-12051477f6d0)

When I set it as filter, I see a connection with a lot of red and yellow incompleted traffic. 
At that moment, I remember back the lyrics of the youtube clip song - **ZOMBIEEE**

So, I feel this might something like zombie attack or DDOS attack. After this I stuck at here.... QwQ

<p>&nbsp;</p>

#### After a long long time...
Challenge creator release a hint, something like take attention on the chall and the music (sry I forget what exaclly the hint @3@)

After that, I notice the chall title and the music always repeat... "IN MY HEADDD, IN MY HEADDD" Wait?! **HEADD**?? maybe I think what I need to take attention is the... header?

![image](https://github.com/user-attachments/assets/e9859fc9-419d-4161-a9cf-5775bf600e71)

So I continue move to search something on the header. When I arrange the network activity according to the source address, I found a suspicious situation.
All the activity headers from ip `10.10.1.13` contains some words after the "(" like a, H or R

![image](https://github.com/user-attachments/assets/0ff56b26-f527-4a48-8052-eb8c6fab90bf)

![image](https://github.com/user-attachments/assets/85608727-3ad4-4460-ba8f-8b62c96dbb2e)

However when coming to source ip `10.10.1.9`, there are no any words for all acitivities at that byte

![image](https://github.com/user-attachments/assets/3dff46f2-579d-4aae-a982-afdc469b6b93)

I try to collect all the words from the network activities with source ip `10.10.1.13` and I get this string that seem like encrypted with base 64

**aHR0cHM6Ly95b3V0dS5iZS80eS1aU0xiNHF1RQ==**

<p>&nbsp;</p>

After decrypting it, we get a... youtube link again???
![image](https://github.com/user-attachments/assets/2c4eda45-530d-42c1-aff5-255b4ecebd2f)

But this link is redirected to a video by the author and the flag is at the description box
![image](https://github.com/user-attachments/assets/dd01956b-4a8d-464b-a035-60f893e02de3)

And let's us shake with the video!!!

 <img src="https://i.makeagif.com/media/10-01-2023/LiPcDx.gif"/>

 ### Flag: SHCTF24{uN_D05_7R35_CU47r0_IN_My_H34D_24/7}

**ps: This is the way that how I solve this challenge. In between maybe there is some part with wrong information. 
If you find it, welcome come to tell me anytime. I will update it with the correct information**
