# Node-red, TTN, Cayenne

### Install the TTN module for node-red:

```
  cd $HOME/.node-red
  npm install node-red-contrib-ttn
```

### Start (or re-start) node-red at the terminal

```
  node-red
```  

### Consume TTN data from your Cayenne encoded application

Drag a `ttn-message` node from the palette on the left to the main node-red flow.

You will need to create a new application first - ensure the 'App' menu is ste to 'Add new ttn app...' and click the pencil icon.

#### Set the TTN application

Set the `App ID` from your application name on TheThingsNetwork console - it's the human-readable application name.

The `Region or Broker` will need to be set to `eu`, at least until we default ourselves, sputtering, out of Europe, holes in feet and noses ballistically removed from faces.

The 'Access Key' is the long hex string from TheThingsNetwork console for your app.

Once the settings are entered, click 'Add'.

You are now returned to the 'ttn message' node panel.

Set the 'Device ID' to match your human-readble device ID, as set on TheThingsNetwork console.

Click 'Done' to save the 'ttn message node' configuration.

This node now recieves packets sent from your ExpLoRer board.

### Dump the inbound messages

Add a 'debug' node from the left hand side to the main flow.

Double-click it to bring up the options, and set the 'Output' to 'complete msg object'.

Click 'Done' to save the node.

Connect the right-hand output outlet from the 'ttn message' node to the input of the 'msg' node.

### Deploy the application

Click 'Deploy' in the top right. 

Click the 'debug' tab on the right hand side and watch the output from device, parsed by the ThingNetwork, and encoded as a JavaScript JSON-style object.

If you are sending Cayenne LPP data, take a look at the 'payload_fields' object.

You can use 'function' nodes to process the data as needed, and send it on to other objects.

Generally, the `msg.payload` is used to send data from one node to another, so you can use Javascript to parse the `msg.payload_fields.temperature_1' item and store it in the msg.payload - add a 'function' node and enter the following code:

```
msg.payload = "It's "+msg.payload_fields.temperature_1+"°C";
return msg;
```

You could easily connect the output to a Twitter output node, which uses the content of the inbound `msg` object's `payload` property as a string to tweet through an authenticated twitter account.
