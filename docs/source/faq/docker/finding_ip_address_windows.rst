Finding your IP address on Windows
==================================

1. Open a PowerShell terminal and set your IP address as an environmental variable.
2. Run ``ipconfig``
3. Copy the IP address of your network adapter. It is typically listed under the *Ethernet adapter Ethernet:* category and the *IPv4 Address* field e.g. *135.246.218.122*.
4. Run the following command to save your IP address as an environmental variable ``$env:IPAddress = "YOUR_IP"``, where YOUR_IP is the IP number you copied from the previous step. The quotation marks ("") need to be included in this command.