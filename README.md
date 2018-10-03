Auto install script for TimeIsMoney (TIM)

TimeIsMoney (TIM) Masternode Install Script
Use this script on a fresh install of Ubuntu 16.04 x64(not lower)

This will guide you to setup a masternode on TIM so follow steps carefully

STEP 1 - Sending Collateral Coins

    Download the latest wallet from : https://github.com/rmcpartner/timeismoneycrypto/releases and install it.
    Open your Windows wallet - MAKE SURE IT IS SYNCED
    Go to Tools -> Debug Console
    Type: getaccountaddress MN# (# is your masternode number you want to use)
    In the Debug Console Type: masternode genkey
    Send 1000 TIM to this address
    Type: masternode outputs (This can take a few minutes before an output is shown)
    Save your TX ID (The first number) and your Index Number (Second number, either a 1 or 0)
    Save your generated key as well as this will be needed in your VPS as your private key
    Save these in a notepad
    Close the wallet

STEP 2 - Setting up your Linux VPS (Read all instructions and follow prompts carefully)

Connect to your linux vps AS ROOT (AWS USERS USE sudo -i TO LOGIN AS ROOT), copy and paste the following line into your VPS. 
Copy paste each line one by one into your console

sudo apt-get install -f git

sudo git clone https://github.com/LEGENDSTER/timenode.git

cd timenode

sudo bash install.sh && cd

enter the genkey save in notepad

you will see error but dont worry about it.

STEP 3 - Editing your Windows Config File

    Open your wallet
    Go to Tools -> Open Masternode Configuration File
    Enter the following on one single line after the example configuration <alias> <ip>:11334 
    <private_key> <tx_id> <index>
    It should look something like this: mn1 127.0.0.2:11334 
    93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 
    572ae2c7135a8da2c1dbf2866240ec209a113f2851104c4e3e9b83e6cb7f0b3d 1
    Save and close the file and restart your wallet.

Goto vps 

type sudo nano /root/.timeismoney/mainnet/timeismoney.conf

paste the following according to the username and password given in your vps

rpcuser=timeismoneyrpc
rpcpassword=caK1W9XYTDGCf4Pn8HbNofNzxQJ
rpcallowip=127.0.0.1
staking=1
listen=1
txindex=1
server=1
daemon=1
maxconnections=256
port=11333
rpcport=11334
masternode=1
masternodeaddr=343.183.33.232:11333
masternodeprivkey=genkey

click on ctrl + x and enter

STEP 4 - Starting the Masternode

    In your wallet, go to Tools -> Debug Console
    Enter masternode start-alias <alias> with <alias> being the name of your masternode from Part 3
    
    Goto vps
    
    type cd /usr/local/bin
Then type ls
you will see 3 green files
type ./timeismoneyd and it will start the timeismoney server

wait for it to sync to the current block
  Enjoy! You can start this process over again for another MN on a fresh Linux VPS!
  
  Part 5 - Checking Masternode Status

    After running the command in step 4, go back to your VPS
    Enter cd to get back to your root directory
    Enter timeismoney-cli mnsync status A synced wallet will show sync status value as true and assets as 999.
    Enter timeismoney-cli masternode status : It should show your vin, service (IP), public key and activation status.
    This will tell you the status of your masternode, any questions, please ask the developers.

CONSIDER SENDING SOME TIPS TO : TvCSDoAGzHeaYEmQCuSmoauqzrE2nLw61f

