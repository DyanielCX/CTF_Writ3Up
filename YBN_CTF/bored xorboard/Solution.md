## Introduction

**Challenge: bored xorboard**

**Level: Easy**

**Category: Reverse Engineering**

**Author: duck**

![Screenshot_2](https://github.com/user-attachments/assets/da22e18c-26a6-4888-b62a-946999b8bd41)

## Solution
Before we start reverse engineering, try to run the program that we get in kali linux

Here we can see it will ask us for a input. I guess it might a password checker to let us key in a correct flag
![image](https://github.com/user-attachments/assets/9b09cb06-3c14-4d56-8221-878e327e3ae4)


Now we move to **REVERSE ENGINEERING** part!!! Here I'm using the binary ninja

In the main function, I think can know the whole system operation cuz I can see all the predifined output content in this function.

![image](https://github.com/user-attachments/assets/dc12b2f4-9712-436a-8e65-d6392d08429a)


After source code reading, I find this is the password checker logic and the labeled code is the encryption condition for the flag

![image](https://github.com/user-attachments/assets/fffac477-7b26-4a46-8d2b-2f1af44ce17d)

<p>&nbsp;</p>

**Here is the logic for the encryption condition**
```
data_4080 -> result cheker variable
data_4040 -> XOR encrypt variable
&var_128  -> user input

data_4080 = &var_128 ^ data_4040

^ = XOR
```

To decrypt and get the flag, we need to reverse the formula with the below concept
```
&var_128 =  data_4080 ^ data_4040
```

<p>&nbsp;</p>


So now we know the concept to get the flag, then we need to find the `data_4080` and `data_4040` variable data from the binary and here's it

![image](https://github.com/user-attachments/assets/88517331-0365-4fb1-9dea-48c7db80ea07)

With the decryption concept and the variable data, write a python code and you will get the flag [>⁠ω<] !!

#### Python Script:
```python
# Define the hexadecimal data for data_4040 and data_4080
data_4040 = [
    0x10, 0x51, 0x96, 0xef, 0xac, 0x5d, 0xd2, 0x1b, 0x88, 0xa9, 0x4e, 0x87, 0xa4, 0x35, 0x0a, 0x33, 
    0x00, 0x01, 0x06, 0x1f, 0x9c, 0x0d, 0x42, 0x4b, 0x78, 0x59, 0xbe, 0xb7, 0x94, 0xe5, 0x7a, 0x63, 
    0xf0, 0xb1, 0x76, 0x4f, 0x8c, 0xbd, 0xb2, 0x7b, 0x68, 0x09, 0x2e, 0xe7, 0x84, 0x95, 0xea, 0x93, 
    0xe0, 0x61, 0xe6, 0x7f, 0x7c, 0x6d
]

data_4080 = [
    0x49, 0x13, 0xd8, 0xdd, 0x98, 0x26, 0xbc, 0x2b, 0xfc, 0xc1, 0x7f, 0xe9, 0xc3, 0x6a, 0x66, 0x02,
    0x6b, 0x32, 0x59, 0x6c, 0xac, 0x60, 0x71, 0x14, 0x00, 0x69, 0xcc, 0xc4, 0xcb, 0x91, 0x4a, 0x3c, 
    0xb7, 0xd4, 0x41, 0x10, 0xfe, 0x8c, 0xd6, 0x24, 0x27, 0x6f, 0x71, 0x85, 0xb4, 0xe7, 0x8f, 0xf7, 
    0xd0, 0x0c, 0xc8, 0x51, 0x52, 0x10
]

# Compute XOR result
xor_result = [0] * len(data_4040)

for i in range(len(data_4040)):
    xor_result[i] = data_4040[i] ^ data_4080[i]

# Print the XOR result in hexadecimal
print("XOR Result:")
print("".join(f"{chr(byte)}" for byte in xor_result))
```

Here is the result of script

![image](https://github.com/user-attachments/assets/6a0fd62b-21bc-48c5-9c7d-3f47acf47ce0)

<p>&nbsp;</p>

Using the result flag to run the program again for double checking
![image](https://github.com/user-attachments/assets/7c25bbf5-96dc-4fcf-85b3-d2f1eaf29d72)

 ### Flag: YBN24{n0th1ng_l1k3_s0m3_x0rs_t0_Ge7_r1d_Of_b0red0m...}

**ps: This is the way that how I solve this challenge. In between maybe there is some part with wrong information. 
If you find it, welcome come to tell me anytime. I will update it with the correct information**
