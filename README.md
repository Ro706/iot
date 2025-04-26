# MQTT

## Setup Instructions for IoT

### Setup Section

1. **Install Node-RED**
   Run the following command to install Node-RED globally with unsafe permissions:
   ```bash
   npm install -g --unsafe-perm node-red
   ```
   (This sets up Node-RED.)

2. **Download Mosquitto**
   Download Mosquitto from [https://mosquitto.org/download/](https://mosquitto.org/download/).
   (This sets up Mosquitto.)

   After downloading:

   - Navigate to `C:\Program Files\mosquitto` in your file manager.
   - Open Command Prompt in the Mosquitto folder:
     ```bash
     cd "C:\Program Files\mosquitto"
     ```

3. **Using Mosquitto**

   - **Subscribe to a Topic**
     Use the `mosquitto_sub` command to subscribe to a topic:
     ```bash
     mosquitto_sub -t "<name>"
     ```
     Example:
     ```bash
     mosquitto_sub -t "IOT/Sem6"
     ```

   - **Publish a Message**
     Use the `mosquitto_pub` command to publish a message:
     ```bash
     mosquitto_pub -t "<name>" -m "<message>"
     ```
     Example:
     ```bash
     mosquitto_pub -t "IOT/Sem6" -m "sir is absent today"
     ```

4. **Using Node-RED**

   - **Set Up MQTT in Node-RED**
     - Drag and drop the Debug node and the MQTT In node onto the workspace.
     - Double-click the MQTT In node to open the side menu.
     - Follow these steps:
       - Click the **Add** button to create a new server.
       - Add the server name.
       - Set the server IP to `127.0.0.1` and port to `1883`.
       - Click **Add** (top right).
       - Add the server.
       - Enter the topic name `<name>` (matching the Mosquitto server topic).
       - Click **Done**.
     - Deploy the Node-RED server by clicking **Deploy** (top right).

   - **Check if the Message is Received**
     Publish a message to check if it is received:
     ```bash
     mosquitto_pub -t "IOT/Sem6" -m "hello"
     ```

   - **Send a Message Using Node-RED**
     - Drag and drop the MQTT Out node onto the workspace.
     - Set it up as follows:
       ```yaml
       Name: [Whatever you want]
       Server: [Select your server]
       Topic Name: <name> (Mosquitto server topic)
       QoS: 1
       Retain: true
       ```
       - Click **Done**.
     - Add an Inject node:
       - Configure `msg.payload` to be a string.
       - Add the message you want to send.
       - Click **Done**.
     - Deploy the Node-RED server by clicking **Deploy** (top right).

   - **Debug the Message**
     - Click the Debug icon.
     - Click the message button to see the message output.
```

You can copy and paste this content into a `README.md` file.
