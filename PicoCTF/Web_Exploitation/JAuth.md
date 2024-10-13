1. Based on the question, login the website with **test** (username) and **Test123!** (password)
![image](https://github.com/user-attachments/assets/73e1eefb-a7a9-40b3-9be7-e9a6f43fba99)
<p>&nbsp;</p>
<p>&nbsp;</p>

2. Since we have given the hint to check the JWT cookie. So now we go to find the cookie
   <p><b>(Inspect -> Application -> Cookies -> token)</b></p> 
![image](https://github.com/user-attachments/assets/48c70e90-d660-4b91-97c9-1f339d331dbc)
<p>&nbsp;</p>
<p>&nbsp;</p>
   
3. Copy the value of token and go to **JWT online decoder** to decode the token
    <p><b>Know more about JWT cookies: </b>https://strapi.io/blog/introduction-to-jwt-and-cookie-storage</p> 
![image](https://github.com/user-attachments/assets/f5a988f4-3de4-4618-b02d-d550eec7f274)
![image](https://github.com/user-attachments/assets/846dd818-ee5e-4d84-8e4f-e2a816097d8c)
<p>&nbsp;</p>
<p>&nbsp;</p>

4. In the challenge, there is a hint ask us to **"become an admin"**. So we change the algorithm to **none** and remove the signing key, the token will just simply check for none algorithm.
    After that, remember also change the role to **admin**.
![image](https://github.com/user-attachments/assets/a284062f-b81d-4296-9a69-3b712dbecab3)
<p>&nbsp;</p>
<p>&nbsp;</p>
   
6. Copy the JWT String and change the token value in cookie with this string
    <p><b>!Remember to add a dot(.) at the end of the JWT String!</b></p> 
![image](https://github.com/user-attachments/assets/aacfe901-461a-4ffa-a55b-fc509ae7b684)
![image](https://github.com/user-attachments/assets/12a3a6eb-c431-49fa-bad6-128a6be185aa)

7. Reload the website and congragulation you have get the flag [>w<]""
![image](https://github.com/user-attachments/assets/99694b8d-737d-47a7-87a3-b22c14ce968a)
