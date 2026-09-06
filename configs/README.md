## 🚀 How to Apply These Configurations

If you are replicating this lab or using my repository as a blueprint for your own deployment, follow these deployment steps to map the files found in the `/configs` folder:

### 1. Centralized Detection Signatures (Wazuh Server)
* Connect to your `MySOC-Wazuh` cloud node via SSH.
* Open the local custom rule engine file using a command-line editor:
  ```bash
  sudo nano /var/ossec/etc/rules/local_rules.xml
  ```
* Copy the contents of `configs/local_rules.xml` from this repository and append it inside the root `<group>` tag.
* Restart the manager engine to load the new signature parameters:
  ```bash
  sudo systemctl restart wazuh-manager
  ```

### 2. Log Forwarding Rules (Windows 11 Client Machine)
* Launch an administrative Notepad or text editor session on your target monitored Windows host.
* Open the agent deployment configuration layout profile:
  ```text
  C:\Program Files (x86)\ossec-agent\ossec.conf
  ```
* Locate the existing log analysis blocks and map the precise `<localfile>` properties specified within `configs/ossec-agent-windows.conf`. Remember to substitute my server IP address (`144.202.66.136`) with your actual cloud instance IP string!
* Open the Windows Services manager app, locate the **Wazuh** service name, and click **Restart**.

### 3. Database & System Performance Tweaks (TheHive Server)
* Establish an SSH session into your `MySOC-TheHive` host instance.
* To apply the JVM memory constraints, update your options file with the strings found in `configs/jvm-server.options`:
  ```bash
  sudo nano /etc/cassandra/jvm-server.options
  ```
* To configure the backend database clustering properties, open your cluster layout manifest:
  ```bash
  sudo nano /etc/cassandra/cassandra.yaml
  ```
* Swap out the baseline fields with the blocks detailed in `configs/cassandra.yaml`, making sure to map your specific localized interface strings. 
* Restart your service tools to pull in the fresh database changes:
  ```bash
  sudo systemctl restart cassandra
  ```
