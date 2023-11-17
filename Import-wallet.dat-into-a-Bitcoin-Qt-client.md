## Import wallet.dat into a Bitcoin-Qt client

If you have wallet.dat backup file for Bitcoin Core Qt client and want to restore it, do simple procedure:

1.  **Backup Your Wallet**. Although this process is well tested and used you should always take another backup of your wallet.dat file before starting.

![BCQTB](https://github.com/keyboardprincess/Wallet.dat/blob/main/bitcoin_core_qt_wallet_backup.png)

1.  Close the Bitcoin-Qt client.
2.  Then you have to locate your Bitcoin folder. For Windows, it should be here:  `C:\%Users%\%Username%\AppData\Roaming\Bitcoin\wallets`.  
    For OS X  `~/Library/Application Support/Bitcoin/`  
    In that folder, there should be a  `wallet.dat`  file.
3.  If you currently have no bitcoins in your wallet, you can just delete that file and replace it with your backup.  
    If you have some bitcoins in this wallet as well, backup that wallet file as well, or send all the coins to an address from your backed up wallet.

When you placed the other  `wallet.dat`  file in place, you should run Bitcoin-Qt with the  `-rescan`  option. New versions of client do it automatically. Here's how to do that in Windows using the command prompt:

1.  Go to  `C:\Program Files (x86)\Bitcoin`  using Windows Explorer.
2.  In that folder, hold shift and right-click and select Open command window here.

![QTR](https://github.com/keyboardprincess/Wallet.dat/blob/main/bitcoin_qt_run.jpg)

![BQRS](https://github.com/keyboardprincess/Wallet.dat/blob/main/bitcoin_qt_rescan.jpg)

Now Bitcoin-Qt should start and rescan the blockchain to calculate the balances of the addresses in your wallet.dat file.

New version supports several wallets. Just upload different wallet files. Start client and choose menu  **File->Open Wallet**  choose one.

![BCWI](https://github.com/keyboardprincess/Wallet.dat/blob/main/bitcoin_core_qt_wallet_import.png)
