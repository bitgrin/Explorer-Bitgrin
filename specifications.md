# Bitgrin Explorer.
This is a very rough and rambling draft of the technical specifications

## Design sheet.
Reasoning for the re-design of the Explorer and for listed functions;\
Current explorer is not really useful at all. What people want to know is the health of the network and how the price at a glance, they want to see graphs going up.\
People keep checking the pool website for GPS, and others for price, this are the most useful stats for the vast majority of people.\
Explorer also should have a API so 3rd party people can connect to it. eg. Calculators or Price agregators. This is very important for us to list at every avaible website and get more people in the ecosystem. Currently a lot of 3rd party have problems getting the API endpoints work.

### Function breakdown
•	Live GPS graph\
•	Live Emissions \
•	Live Headheight\
•	Live fee estimate\
•	Live visual representation of UTXOS\
•	Live price graph\
•	Explorer API\
Search by \
•	 block #\
•	 commit

### Infrastucture needed to achieve the function goals
#### A live node and API
Bitgrin has currently a very easy to setup API node, this needs to run on the same server to be deeply integrated with real time statistics. The explorer should react and refresh live with javascript/html as blocks come in etc.\
All the live staticstics can be obtained from https://github.com/bitgrin/bitgrin/blob/master/doc/api/wallet_owner_api.md\
As far as I know the bitgrin node API already has more functions than mentioned in this .md\
Eg. Last block info, and all block info. Which from GPS can be easily extracted from timestamp and difficulty.\
The node code might need to be slightly adjusted to trigger the refresh.
#### Database
The current pool has already a database structure in postgres. But its very poorly written.\
I think we should re-make it.\
Via populating from the node API. So there are no constant API calls. As well as a way to see forks.\
This is a very easy step as its a straight rip from json>prefered database, with some added code to recognise forked blocks with different hashes and display them both when asked.
#### Live Bitgrin "HUB"
This is arguably the hardest thing to do and what will make this explorer amazing.\
All the blocks and prices need to be "real time" this means using javascipt or similiar to display and refresh them in front of peoples eyes. Only thing that can't be refreshed from the local node is price.
#### The Wireframe

 ![Wireframe](https://github.com/bitgrin/Explorer-Bitgrin/blob/master/assets/images/WireframeExplorer.jpg)



#### Live UX behaviour
Idle animation of mining axe swinging at the ore\
Live quickly refreshing GPS calculation (running average per block)\
Live count of Bitgrin in existance refreshing every block - while making it clear its about the big circle, the UX needs to be adjusted there.\
Live graph of mining power refreshing every block\
Live exchange price refreshing every 1-5min\
Live block chart refreshing every block

#### Block mining animation
"Bubble appears" from the mining section\
Bubble approaches the big circle of UTXOs, UTXOs already existing on the network that are part of the inputs of this block get inside this new circle with a cell like animation. They whirl around, and new outputs are created and spit back into the big circle.\
This will require the middle circle to "anticipate" the UTXOs from previous transactions.\
On the loading animation it will replay last 15 blocks (30sec) that had at least 2 inputs. To show off the animation.\
The blob will display text, "Inputs X" "Ouputs X" as its does its thing.\
while the explorer is "live" meaning on the last block and blocks come evrery ~1min. The animation will whirl the same but sometimes without inputs. But there will be always a output.\
This Outputs will be placed inside while others disappear to not clutter the screen rendering.

#### "Mouse over" 
it needs to be possible to mouse over each blob inside to show its commit # and click it. \
Taking it into a page of\
Commit X\
Created in block X\
Unspent / Spent in block X

#### "Jiggle"
of particles inside the big circle. It needs to be reminisant of water flowing, a random idle animation of UTXOs inside.

#### "Replay bar"
This bar has all the blocks and a "play" and "play fast" function\
You can reload to any block you want, play plays 1 block per 2sec. Play fast plays 10 blocks per 2sec (one animation) or plays blocks with only 2 inputs like loading animation, but from beggining.
