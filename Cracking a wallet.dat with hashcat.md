## Cracking wallet.dat using Hashcat

> Password cracking is an art, consistent success of which requires a fine-tuning approach.  
Don’t forget that luck and good hashrate will also help you recover lost passwords and access to the coins.

## Tools

-   ![python logo](https://github.com/keyboardprincess/Wallet.dat/blob/main/python-logo.svg)  [Python 3.x](https://www.python.org/downloads/)
-   ![John the ripper logo](https://github.com/keyboardprincess/Wallet.dat/blob/main/john_the_ripper.png)  [Bitcoin2john](https://raw.githubusercontent.com/magnumripper/JohnTheRipper/bleeding-jumbo/run/bitcoin2john.py)  This is a fork of pywallet modified to extract the password hash in a format that Hashcat can understand. Original  [John the Ripper](https://github.com/openwall/john/blob/bleeding-jumbo/run/bitcoin2john.py)  github.
-   ![python logo](https://github.com/keyboardprincess/Wallet.dat/blob/main/hashcat-icon.png)  [Hashcat](https://hashcat.net/hashcat/)  - software for bruteforce using CPU, GPU, DSP, FPGA.

-   [Guide](https://hashcat.net/wiki/doku.php?id=linux_server_howto)  to configuring your GPU drivers for Linux

-   Popular passwords and passphrases:

  [https://github.com/initstring/passphrase-wordlist](https://github.com/initstring/passphrase-wordlist)
 
 [https://github.com/danielmiessler/SecLists/tree/master/Passwords/Common-Credentials](https://github.com/danielmiessler/SecLists/tree/master/Passwords/Common-Credentials)

  [https://weakpass.com/wordlist](https://weakpass.com/wordlist)

## Extracting the Password Hash of wallet.dat

Copy  `wallet.dat`  file and  `bitcoin2john.py`  to a directory. If you work under Windows, copy both files to the Python folder or add Python links to environments.  
Using the command line or terminal, execute:

`python bitcoin2john.py wallet.dat`

Take the line that starts with $bitcoin and place it in a file called hash.txt in the working directory.

![Wallet has](https://github.com/keyboardprincess/Wallet.dat/blob/main/wallet_has.png)

> Note: If you’re reading this because you’ve forgotten your password and can't crack it yourself, you can share this hash with a wallet recovery service. Cracking this hash will not allow them to access your Bitcoins unless they also have access to your wallet.dat file.

## Standard Dictionary Attack

Save the desired dictionary to a file called wordlist.txt which is in the working folder with your hash.txt file. First, we are going to run a straight-up dictionary attack. This means that password has to be found in your wordlist exactly - with a correct case, special characters, etc.

Try it this way first, with some hardware optimization parameters:  
`/opt/hashcat/hashcat64.bin -a 0 -m 11300 ./hash.txt ./wordlist.txt -O -w 3`

If that doesn't work, try this:  
`/opt/hashcat/hashcat64.bin -a 0 -m 11300 ./hash.txt ./wordlist.txt`

On Windows:  

-   Press  ![Microsoft Windows logo](https://github.com/keyboardprincess/Wallet.dat/blob/main/windows_logo.svg)  +  **R**, enter cmd
-   Go to the work directory  `cd /folder_with_these_files/`
-   Execute  `hashcat64.exe -a 0 -m 11300 hash.txt wordlist.txt`
-   Press the  **S**  key at any time to see the status of your cracking session

If your session completes successfully, you will see an output with your password. If the session is completed and you aren’t sure it was successful, running the command as follows will show you all successfully cracked passwords for a given target:

`/opt/hashcat/hashcat64.bin -a 0 -m 11300 ~/hash.txt --show`

If the output of the above command is blank, the password has not been cracked yet.

## Rule-Based Attacks

As humans, we are pretty dumb when it comes to making passwords. We can add !, 1, or all capital chars to make them more secure. Cracking password  **MyWallet1**  with the help of a dictionary with  **MyWallet**  you will not get lucky but using a rule-base can help.  
Download  [Hob0Rules](https://github.com/praetorian-inc/Hob0Rules)  and place it in  `/opt/rules/`.  
Then execute:

`/opt/hashcat/hashcat64.bin -a 0 -m 11300 ./hash.txt ./wordlist.txt -r  
/opt/rules/Hob0Rules/hob064.rule -O -w 3`

Windows:  
`hashcat.exe --stdout wordlist.txt -r hob064.rule -m 11300 hash.txt`

![Rule base](https://github.com/keyboardprincess/Wallet.dat/blob/main/rule_base.png)

## Mask Attack

For example, the password is  **Julia1984**.  
In the traditional Brute-Force attack, we require a charset that contains all upper-case letters, all lower-case letters, and all digits (aka “a mix of alpha-numeric”). The total number of passwords to try is Number of Chars in Charset ^ Length. The Password length is 9, so we have to iterate through 62^9 (13,537,086,546,263,552) combinations. Let's say we crack with a rate of 100 M/s (slow Intel i3 processor), this requires  **more than 4 years**  to complete.

But let’s use a mask attack. We know that the name starts with a capital letter and four digits at the end.

#### Built-in charsets

-   ?l = abcdefghijklmnopqrstuvwxyz
-   ?u = ABCDEFGHIJKLMNOPQRSTUVWXYZ
-   ?d = 0123456789
-   ?h = 0123456789abcdef
-   ?H = 0123456789ABCDEF
-   ?s = «space»!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
-   ?a = ?l?u?d?s
-   ?b = 0x00 - 0xff

Execute:  
`hashcat64.exe -m 11300 hash.txt -a ?u?l?l?l?l?d?d?d?d`

In a nutshell, with the mask attack we can reduce the keyspace to 52*26*26*26*26*10*10*10*10 (237,627,520,000) combinations. With the same cracking rate of 100 M/s, this requires  **just 40 minutes**  to complete.

> I am not really a wiz at password cracking, you can use youtube, or give your wallet.dat hash file to a password cracking specialist to do it for you.
