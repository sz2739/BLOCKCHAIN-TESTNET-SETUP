# BLOCKCHAIN-TESTNET-SETUP
Instruction for seting up a testnet blockchain 
# GETTING START
We are setting up a  private testnet that our team can use to explore potentials for blockchain at ZBank.
Testnet will give our team of developers the freedom to experimen since there is no real money involved, and testnets allows for offline development.

# Setup the custom out-of-the-box blockchain
Create accounts for two (or more) nodes for the network with a separate `datadir` for each using `geth`:
Create the first node's data directory using the geth command and a couple of command line flags by running the following line in your terminal window:
1. Navigate to your folder with puppeth 
2. Use the geth command:
```./geth account new --datadir node1```
create a new note name "Node 1 Key" and record the public key of node 1
```./geth account new --datadir node2```
create a new note name "Node 2 Key" and record the public key of node 2

# Configuration
Run 'puppeth', name the network (i.e hw18), and select the option to configure a new genesis blcok
``` ./puppeth```
network name = hw18
Type 2 to pick the Configure new genesis option, then 1 to Create new genesis from scratch
Type 2 to choose Clique (Proof of Authority) consensus algorithm.
Paste both account addresses from the first step one at a time into the list of accounts to seal.
Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.
* You can choose `no` for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.
Choose a chain number (i.e 555) and remember it for the use in the MyCrypto custom network setup 
Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.

* Export genesis configurations. This will fail to create two of the files, but you only need `hw18.json`.

Puppeth Configuration 1 ![Screen Shot 2020-05-08 at 10 45 19 PM](https://user-images.githubusercontent.com/58964615/81462940-f37cb100-9183-11ea-9440-2ea5371b53bd.png)
Puppeth Configuration 2 ![Screen Shot 2020-05-08 at 10 45 28 PM](https://user-images.githubusercontent.com/58964615/81463003-49e9ef80-9184-11ea-8343-0e5dd9d2a6f7.png)

# Initialization
Now we can initialize and tell the nodes to use the genesis blocks that we created 
Initialize the first node, replacing yournetworkname.json with your own: hw18.json
Run command for node 1
```./geth init hw18.json --datadir node1```
Run command for node 2
```./geth init hw18.json --datadir node2```

Initialization ![Screen Shot 2020-05-08 at 11 55 58 PM](https://user-images.githubusercontent.com/58964615/81463418-8408c080-9187-11ea-9338-2168545d8421.png)

# Connect and Start the Chain
Now we will start both nodes that we've created and bring the blcokchain to life
Open a terminal window (Git Bash in Windows) navigate to your Blockchain-Tools folder and follow the next steps.
Launch the first node into mining mode with the following command: (Run the first node, unlock the account, enable mining, and the RPC flag. Only one node needs RPC enabled.)
```./geth --datadir node1 --mine --minerthreads 1 --rpc --unlock 0xf38af9daD204942a07a2bdd816a231B8112FC1Db   --allow-insecure-unlock```
Type and enter the password you created during the running of the command 
You should see the node Committing new mining work:Copy this command into your notes and label it Start Node 1.

Start Node 1 ![Screen Shot 2020-05-09 at 12 02 13 AM](https://user-images.githubusercontent.com/58964615/81463563-5d975500-9188-11ea-95dd-02d74828d867.png)

Now you will launch the second node and configure it to let us talk to the chain:
Scroll up in the terminal window where node1 is running, and copy the entire enode:// address (including the last @address:port segment) of the first node located in the Started P2P Networking line:

We will need this address to tell the second node where to find the first node.

Open another terminal window and navigate to the same directory as before.
Launch the second node, enable RPC, change the sync port, and pass the enode:// address of the first node in quotes by running the following command:
```./geth --datadir node2  --port 30304  --unlock 0x1928AdF33A4b558e0C42F32554aEB4577D10AB6f  --bootnodes "enode://c59b42601102f8a4599ce85a508056b7b5a4fc6ce3004d05e604182a98dd0c5460fcba5673a664e84d409f704ad96da24ac641526548c8f78f96fe0de861eb19@127.0.0.1:30303" --allow-insecure-unlock```

Connect with second node ![Screen Shot 2020-05-09 at 12 03 29 AM](https://user-images.githubusercontent.com/58964615/81463585-89b2d600-9188-11ea-8792-0c1e021d8f46.png)

The output of the second node should show information about Importing block segments and synchronization, Copy this command into your notes and call it Start Node 2.

You should now see both nodes producing new blocks, congratulations!

# Final Transaction
We will be connecting MyCrypto to the custom chain, importing the pre-funded wallet, then sending a test transaction to ourselves!

Set up new network by clicking Changing Network - Add Custom Node: 
<img width="576" alt="Screen Shot 2020-05-09 at 12 06 26 AM" src="https://user-images.githubusercontent.com/58964615/81463631-f3cb7b00-9188-11ea-87f8-ff209e16a417.png">
Once finished, click View & Send  - Keystore FIle and select keysotre file: from the `node1/keystore` directory. This will import the private key.
Input the password and hit unlock
Copy & paste your node 2 address, and select the amount you would send to node 2, and hit send. 
<img width="1259" alt="Screen Shot 2020-05-08 at 11 04 15 PM" src="https://user-images.githubusercontent.com/58964615/81463714-9edc3480-9189-11ea-82ab-3fa0ffc921c3.png">
Copy the transaction hash and paste it into the "TX Status" section of the app, or click "TX Status" in the popup.
<img width="1075" alt="Screen Shot 2020-05-08 at 11 07 39 PM" src="https://user-images.githubusercontent.com/58964615/81463723-a7cd0600-9189-11ea-84f7-fc6b39502684.png">

Celebrate, you just create a blcokchain and sent a transaction! 
