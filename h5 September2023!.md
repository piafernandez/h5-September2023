# Table of contents

- Schneier 2015: Applied Cryptography: 2.3 One-Way Functions and 2.4 One-Way Hash Functions. 
- Särökaari 2018 
- Install Hashcat 
- Crack this hash: 8eb8e307a6d649bc7fb51443a06a216f 
- Gone phishing 

# Schneier 2015: Applied Cryptography: 

> https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html#chap02-sec005

## 2.3 One-Way Functions

- One-way functions are very important in public-key cryptography.
- These functions are easy to compute in one direction but hard to reverse. (Hard in this context would mean that it would take million years to reverse the function, even with all the world's computers)
- An analogy for one-way function is breaking a plate into pieces, which is quite easy, but reassembling the plate is very hard.
- However, despite their importance, there is no mathematical proof that proves the existence of one-way functions.
- One-way functions have limitations; they can't be directly used for encryption because they make the message unreadable.
- Therefore, public-key cryptography requires a different approach.
- Trapdoor one-way functions are a special type of one-way function that includes a secret "trapdoor."
- In trapdoor one-way functions, it's easy to compute f(x) given x and hard to compute x given f(x). However, with the secret information (y), it becomes easy to compute x.
- Analogously, taking apart and reassembling a watch is an example of a trapdoor one-way function, where having the assembly instructions (the "trapdoor") makes reassembly much easier.

## 2.4 One-Way Hash Functions

- One-way hash functions are essential in modern cryptography and are used in various cryptographic protocols.
- They are also known by several names, including compression function, message digest, and cryptographic checksum.
- Hash functions are functions that take a variable-length input (pre-image) and convert it into a fixed-length output (hash value).
- The goal of a hash function is to fingerprint the pre-image, providing an indication of whether a candidate pre-image matches the original.
- One-way hash functions work in one direction: it's easy to compute a hash value from the pre-image but difficult to generate a pre-image that hashes to a specific value.
- A good one-way hash function is collision-free, meaning it's challenging to find two different pre-images that produce the same hash value.
- The security of a one-way hash function lies in its one-wayness and the fact that a small change in the pre-image drastically alters the hash value.
- Message Authentication Codes (MACs) are one-way hash functions enhanced with a secret key. They generate hash values based on both the pre-image and the key, ensuring only those with the key can verify the hash.

# Särökaari 2018

https://www.youtube.com/watch?v=m9YFJGSHYtY

- Phishing involves sending deceptive emails that appear legitimate to steal sensitive data or gain access to networks.
- Phishing emails may contain malicious links and code-executing attachments.

- People click phishing links due to curiosity, expectations, or trust in the sender.
- Legal and ethical considerations are crucial when conducting phishing simulations.
- Email authentication mechanisms like SPF, DKIM, and DMARC can help protect against phishing.
  - Properly configuring SPF records is crucial to prevent hard-to-detect phishing emails.
  - DKIM is an email authentication validation mechanism.
- Attackers can exploit misconfigured SPF records to appear legitimate.
- Attackers can bypass malware filtering and evade detection using obfuscation techniques.
- Website cloning and domain registration play a significant role in phishing campaigns.
- Unfortunately, only few people report phishing incidents, and highly targeted phishing often succeeds.
- User education, security measures, and vigilance are essential for combating phishing attacks.

# Install Hashcat

> https://terokarvinen.com/2022/cracking-passwords-with-hashcat/

## 1.  Open your virtual machine and command prompt

## 2. Install the apps

> `hashid` is a tool used for identifying the types of has functions used to hash passwords or other data. This is helpful to determine which hashing algorithm was used.
>
> `hashcat` is a password recovery and hash cracking tool.

```
$ sudo apt-get update
$ sudo apt-get -y install hashid hashcat wget
```

## 3. Create a new directory 

```
$ mkdir hashed // create a new directory
$ cd hashed // go to the new directory
```

## 4. Get a big dictionary. 

> Rockyou is a popular dictionary with over 14 million words

```
$ wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz // download the compressed file
$ tar xf rockyou.txt.tar.gz // extract the contents
$ rm rockyou.txt.tar.gz // then you can delete/remove the compressed file
```

```
$ head rockyou.txt
123456
12345
123456789
password
iloveyou
princess
1234567
rockyou
12345678
abc123
```

## Let's try to crack a hash

> 6b1628b016dff46e6fa35684be6acc96
>
> Be careful when you copy and paste the hash because just a simple space will completely change the hash.

### 1. Check the type of hash

> In hashid, -m parameter shows the number that's used in the actual cracking, the hashcat parameter with the same name -m.

```
$ hashid -m 6b1628b016dff46e6fa35684be6acc96
```

<img width="436" alt="image" src="https://github.com/piafernandez/h5-September2023/assets/71267247/62436f57-3e88-4017-8501-70f8c297a7ad">


### 2. Crack the hash

> We will use to crack with Mode: 0, which is for MD5 (a very common and very bad hash)

```
$ hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96' rockyou.txt -o solved

-o solved // will save the solution in a new file called "solved"
```

GOOD NEWS ! You have cracked the hash !

<img width="431" alt="image" src="https://github.com/piafernandez/h5-September2023/assets/71267247/4b0bb7ce-a4b6-4e65-8a05-171da4b19392">


### 3. Check the solution

```
$ head solved 
```

<img width="249" alt="image" src="https://github.com/piafernandez/h5-September2023/assets/71267247/143fd000-591a-4f67-8a30-333afc46af43">


The password is summer. It was found in the rockyou dictionary.

# Crack this hash

> 8eb8e307a6d649bc7fb51443a06a216f

## 1. Check the type of hash

```
$ hashid -m 8eb8e307a6d649bc7fb51443a06a216f
```

<img width="430" alt="image" src="https://github.com/piafernandez/h5-September2023/assets/71267247/3cccd36b-8d3c-4a99-b9cf-cd1358fb2c9a">


## 2. Crack the hash

> We will use to crack with Mode: 0, which is for MD5 (a very common and very bad hash)

```
$ hashcat -m 0 '8eb8e307a6d649bc7fb51443a06a216f' rockyou.txt -o solved

-o solved // will save the solution in a the same file called "solved"
```

<img width="430" alt="image" src="https://github.com/piafernandez/h5-September2023/assets/71267247/050cf623-212b-42ca-9f27-d624b50320a8">


## 3. Check the solution

```
$ head solved 
```

<img width="260" alt="image" src="https://github.com/piafernandez/h5-September2023/assets/71267247/b1e849b9-9b55-486b-b905-4534c67600e5">


The password is february. It was found in the rockyou dictionary.

# Gone phishing

<img width="407" alt="image" src="https://github.com/piafernandez/h5-September2023/assets/71267247/133eec75-bcce-4249-bbd0-1d6f4a0baa1f">


## Target

```
The target organization is McAfee, which is a well-known cybersecurtiy company.

The email is intended for individuals who have an account with McAfee and have requested to reset their password.
```

## Goal

```
The goal of the email is to trick the recipient into clicking on the embedded link that appears to lead to a legitimate McAfee website. 

Once on the fake website, the attacker could attempt to collect the recipient's login credentials.
```

## Tactics

### **Technical Tactics:**

**Spoofed Sender Address:** 

```
The email will be sent from "donotreply@authentication.mcaffee.com" which is designed to mimic McAfee's legitimate domain. 
However, the actual domain for McAfee is "mcafee.com." This is a technical tactic to make the email look more convincing.
```

### **Psychological Tactics:**

```
- Urgency: The email creates a sense of urgency by stating that the recipient needs to reset their password in 24 hours. Urgency is a psychological tactic used to pressure recipients into taking action without thinking carefully.
- Trust: The use of "Stay safe, McAfee Team" adds an element of trust.
```

```
This email could potentially pass the common sense test for some recipients due to the following reasons:
- It appears to come from a legitimate source (spoofed domain).
- It uses the name "McAfee Team," which is a trusted brand.
- It creates urgency by claiming the recipient needs to reset their password.
```

# Sources and links

- *CHAPTER 2: Protocol Building Blocks - Applied Cryptography: Protocols, Algorithms and Source Code in C, 20th Anniversary Edition [Book]*. https://www.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html. Accessed 21 Sept. 2023.
- *Disobey 2018 - Phishing through Email - Niklas Särökaari*. *www.youtube.com*, https://www.youtube.com/watch?v=m9YFJGSHYtY. Accessed 21 Sept. 2023.
- *Cracking Passwords with Hashcat*. https://terokarvinen.com/2022/cracking-passwords-with-hashcat/. Accessed 21 Sept. 2023.

- *ChatGPT - OpenAI* [ChatGPT (openai.com)](https://chat.openai.com/?model=text-davinci-002-render-sha) Accessed 22 Sept. 2023.

