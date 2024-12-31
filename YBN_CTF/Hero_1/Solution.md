## Introduction

**Challenge: Hero 1**

**Level: Easy**

**Author: Gr0undUp**

![Screenshot_1](https://github.com/user-attachments/assets/02ad5f0c-62c1-4bde-ad62-523b9c6c1d13)

## Solution
Since the solution has provide a netcat command, I try to run and connect it first. Then, it ask me for two digit and I'm found there are two results.

One is the system seem like stuck after key in two positive number. Another is the system will quit when key in a negative number or non-digit input.

![image](https://github.com/user-attachments/assets/c5dd8dbb-67e4-400d-9689-0730fd181467)
![image](https://github.com/user-attachments/assets/4094bdbf-0288-4b12-8b62-3bd9e49a9eea)

<p>&nbsp;</p>
So far, I know the output result. Now we move to read the provided source code.

#### Source code:
```py
from Crypto.Util.number import getPrime, bytes_to_long

flag = b"YBN24{????????????????????????}"

p = getPrime(256)
q = getPrime(256)
y = getPrime(256)
e = getPrime(64)
c = getPrime(32)


try:
    a = int(eval(input("a: ")))
    b = int(eval(input("b: ")))

    assert a > 0
except:
    quit()


g = q * e
n = ((a) ** (b + c)) * p * q * y

enc = pow(bytes_to_long(flag), e, n)

ct = enc * y

print("g = {}".format(g))
print("n = {}".format(n))
print("ct = {}".format(ct))
```

From the source code, we can know the structure of the system. There is a `try` and `except` function and a `quit()` function in the `except` part.

This mean the system will be end if any error happen. In `try` section, the input a and b are set as integer and restrict must bigger than zero with `assert` function. This is how to lead to the system output.

![image](https://github.com/user-attachments/assets/8c820d3c-e602-44fa-a25b-6d1a39d16871)

In this part, I stuck a long period to find out how to make the system print the flag which is the part at the bottom of source code. 
What I think that moment is this challenge maybe need us to get the output encrypted with RSA like the description mention and write a script to decrypt it.
![image](https://github.com/user-attachments/assets/0b4b061e-c864-4496-b904-22bce4e6d622)

After that, I reread the source code again and again from the start till end and I find a suspicious part which is the `eval`. Normally if the system need ask user input, using `a = int(input("a: "))` already enough. 
So, I go to do some research on the `eval` function.

![image](https://github.com/user-attachments/assets/124d7d1f-f921-411f-907a-22c3897f46b4)

`eval()` function parse the expression argument and evaluate it as a Python expression and runs Python expression (code) within the program. 

What I found from online, `eval()` function consists a vulnerability call Eval Injection. This vulnerability allow attacker easily to call various of functions or commands with the current input.
![image](https://github.com/user-attachments/assets/23eddfcf-a38b-498c-bf53-ab807f27a61b) 

<p>&nbsp;</p>

From this research, I come out with a idea. Since the flag variable is set before the input space. That's mean I maybe can staight away print the flag by exploiting the Eval Injection. 
I try this idea and success to get the flag. Hooray!!!!
![image](https://github.com/user-attachments/assets/0bbd55dd-a8fc-4c5d-8086-650aa48ab1a6)

### Flag: YBN24{RS4_mu1t!prim3_f4ct0r1ng}

## Feeling For Challenege
This challenge is quite interesting. It "exploits" our normal mindset that think what on the challenge description is the challenge hint or way like the **RSA** on this challenge.
This make me take a lot of time on how to retrieve the RSA result and decrypt the result to get the flag. **QwQ**

## Mitigation on Eval Injection
One solution to avoid this vulnerability is to use the dir() method. You may view all of the variables and methods that are available. It’s a good idea to double-check the variables and methods that the user has access to.
![image](https://github.com/user-attachments/assets/44126998-5cb5-4dec-b5ca-4d1f769aad01)


## References
[Eval Function in Python](https://www.geeksforgeeks.org/eval-in-python/) <br>
[Eval Injection](https://owasp.org/www-community/attacks/Direct_Dynamic_Code_Evaluation_Eval%20Injection) <br>
[Mitigation on Eval Injection](https://www.toppr.com/guides/python-guide/references/methods-and-functions/methods/built-in/eval/python-eval/)
