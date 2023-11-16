## What is Wallet.dat?

Wallet.dat is a file that **contains your private keys, public keys, scripts (which correspond to addresses), key metadata (e.g. labels), and the transactions related to your wallet**. If you have an HD wallet, it also includes the HD seed and the derivation paths for each private key.

## How to check wallet.dat is real or fake?

> NOTE: Bitcoin-QT wallet.dat files sometimes even include password clues or hints for cracking. With some luck, skills, and sufficient computing power, you may recover lost passwords and would be able to take a chance on guessing a password to some wallet and get access to bitcoins and altcoins. However, most of these files are fake or forged.

####  How to distinguish the authenticity of a file?

The file itself is a Berkeley DB database that includes an address book, private keys, setting parameters and transactions.

1. To get started, use a hex editor for the search word “xingfeng” (these are the most popular fakes made in China). If you found that website address in the code, no need to go on. Sorry, it’s fake
![](https://github.com/keyboardprincess/Wallet.dat/blob/026a5343f6ff57c7e06f72a6f1c326381f4175c5/xingfeng.png)

2. Next, let’s put the file into the folder ‘wallets’ and synchronize it with Bitcoin-QT. If there are balances and watch-only entries, then the addresses are only for viewing and no private keys at all.

![](https://github.com/keyboardprincess/Wallet.dat/blob/4cfcb49833dcdc96bfb199f7e2e1b156fadb4600/watch-only.png)

It happens that a fake-maker using a hexadecimal editor was replaced only by the wallet address. Then old transactions and the balance appear after the synchronization. It looks like the wallet is real.

3. However, if you send coins (even dust) to that address, the transaction will not occur, because the real address is different.

4. Also, the number of transactions in the list must match the ones in blockchain explorers. All the incoming and outcoming addresses can be found by searching for "name" in the hex editor. If there is a discrepancy in the number of transactions, then the wallet is 100% fake too.

![](https://github.com/keyboardprincess/Wallet.dat/blob/13da03f24427cc1213757d5d6144b30b9aa7be31/wallet.dat_name.png)

5. In old wallets, when creating a new address, several addresses are created and all of them are stored in a file, while the file size changes.

6. After accepting  BIP32 (HD Wallet) a new bitcoin address is created for each payment, and the keys are stored in xpriv, and the file size does not change regardless of the number of addresses. This is also one of the ways to spot the fake. In addition, you can check the types of addresses (segwit  or p2pkh) according to the wallet version.

![](https://github.com/keyboardprincess/Wallet.dat/blob/454de6c50d5611152704c961cc663816606ff763/hd-wallet.png)

7. If the wallet.dat file is open in the Bitcoin-QT application by default, then enter the following CLI command: "`dumpprivkey 1LfV1tSt3KNyHpFJnAzrqsLFdeD2EvU1MK`", which returns:

-   code 10 (or 13), which means you shall enter a passphrase (password)  
    “`Error: Please enter the wallet passphrase with wallet passphrase first. (code -13)`”
-   The private key, if the password is entered or not set
-   error "`Private key for address 1LfV1tSt3KNyHpFJnAzrqsLFdeD2EvU1MK is unknown (code -4)`", which means the file is fake.
