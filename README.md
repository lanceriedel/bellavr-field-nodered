bellavr-field-nodered
=====================

field control

### Install Node Red
Install node red:
```bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
node-red admin init
sudo shutdown -r now
```

### Install SQLite

Requires SQLLite - 
For background see: 
https://flows.nodered.org/node/node-red-node-sqlite

But this is what you need to do:

To install:
 ```
 cd ~/.node-red/
 npm i --unsafe-perm node-red-node-sqlite
 ```

Create this directory (to store the database):
```
mkdir /home/pi/sqlite-storage
```
The database is configured in node red with the file:
```
/home/pi/sqlite-storage/sqlite
```
Note that the first time you create a table, it will automatically create the file in the directory and start writing to it.

 Then just run the following injections to create the table ( found on the Storage Management tab ):
 "Create Game Table"

 if you want to drop the table and start over:
 "Drop Game Table"
 
 ### Field Config Setup
 This sets up the mapping of Arduino nodes to the raspberry pi.  The key is that you need Arudinos with unique IDs.  In order to do this, you should run this sketch on each Arduino on the field. https://github.com/lanceriedel/burn-uuid-eeprom
 This will set a unique ID on the EEPROM that can be read by later sketches (it is 'permanent'). Be sure to put a sticker on the arduino with the new ID.  The ID can be found in the Serial out put when the sketch is run.
 
Then the following instructions:
Config for the field contains the mapping of UUID (as written to each arduino board) and the node id as defined in the field diagram (containing LBO, RBO, etc)

1. Write a text file in the following format:
```
EDGE_UUID,EDGE_NODE_ID
7452C441,LBO
7452C442,LBM
...
```
2. Place on the raspberry pi in this location:

/home/pi/field-config.csv

    2.a -- emergency option, you can force a config down in the "Write config to file"  on the Field Config Tab -- see instructions there

3. Create and/or drop the table -  Create using the "Create Config Table"
4. Run "Load Config File into Config Table"



### UI 
Depending on the IP address of the Raspbery Pi (here it is assumed 192.168.1.112 )
If you installed the UI for the SQLite (very useful) -- it is here:
http://192.168.1.112:8080/

The Dashboard is here:
http://192.168.1.112:1880/ui

