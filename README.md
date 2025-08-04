# VPN-XRay-Setup
<!--Setup-->
- [VDS/VPS Rental](#Rental)
- [Configuring the 3X-UI Panel](#Configuring-Panel)
  + [What is 3X-UI](#What-is-it)
  + [Installation](#Installation)
- [Configuring the client for different OS](#Configuring-OS)
  + Windows
  + Android
  + MacOS
  + IOS
- [Sources](#Sources)

# VDS/VPS Rental
<!--Rental-->
**Register** on the website **[4vps](https://4vps.su/)**

**Select** an **[available server, rent](https://4vps.su/dashboard/addserver)** and **launch**
> Choose the appropriate _tariff_ and the _characteristics_ of the leased server

**Recommended** settings:
| Name           | Specifications                                    |
|----------------|---------------------------------------------------|
| Tariff         | 1 core (3.5 GHz) - 2GB RAM - 20 GB NVMe - 2Gbit/s |
| OS             | Debian 11+, Ubuntu 20.04+, CentOS 8+              |
| Quantity of VM | 1                                                 |

# Configuring the 3X-UI Panel
<!--3X-UI-Panel-->
**What is 3X-UI**

> **3X-UI** is an open-source, **multi-protocol panel** for managing **XRay proxy servers**. It is designed to **simplify** the deployment and management of proxy services, supporting various protocols like **VMess**, **VLESS**, **Trojan**, **Shadowsocks**, and more

**Installation**

****
### ⚠️ ***If the parameter is not specified exactly in the article, then leave it by default.*** ⚠️ 
****

First, we need to connect to the virtual machine that we rented just now. To do this, find out your VM's **IPv4-address** and **password**. Then, follow the instructions:

```
ssh root@your_ip
```

Enter the password. **SUCCESS**, we have connected to the server.

> After the first connection, before entering the password, the system may ask "Are you sure about the connection?" answer ```yes```. Also, your **password** will **not be visible**.

Now, as soon as we are connected to the server, we need to install **3X-UI**.

```
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```
> Next, you will be asked if you want to make additional settings, answer - ```y```

Now they're asking for the **port**. Set any one that is available, for **example: 3539**

Installation finished. You can see the ```Username```, ```Password```, ```Port``` and ```WebBasePath```, that you set earlier.

Check the panel to see if it's working correctly, enter the command:
```
x-ui status
```
This must look like that:
![image1](https://firstvds.ru/sites/default/files/all_images/instructions/xray_vpn/image_9.png)

The next step is to go to the browser and enter the address in the URL string in the format: ```server_ip```:```port```/```WebPasePath```

After logging in, we get to the main page. Go to the ```Connections``` section -> ```Add Connection```.

Set settings that below:

| Switch        | Enable |
| --------------|--------|
| Note          | VLESS  |
| Protocol      | vless  |
| Port IP       | -      |
| Port          | 30014  |
| Total expense | 0      |
| Expire date   | -      |

> ```Note``` is **optional**, and the ```port``` is automatically set as **available**.

Now, set settings for client:

| Switch        | Enable |
| --------------|--------|
| Email         | VLESS  |
| ID            | vless  |
| Total expense | 0      |
| Expire date   | -      |

> ```Email``` the unique name of the client, the application will generate it itself, but you can change it if necessary.

Next comes the configuration of the transport protocol:

```Transmission protocol```: TCP

Proxy Protocol, HTTP Masking, Sockopt, and External Proxy should **all be disabled**.

```xVer``` — leave the value 0. 
```Reality``` — must be enabled. 
```uTLS``` — here you need to select the browser through which the VPN connection will interact with other Internet resources. The best option would be to choose Chrome. 
```Dest``` — this field is intended to indicate the "destination" — here you should enter the domain and port for redirection, write the one you selected above or agree with the standard one. 
```Server names is``` the domain that your connection will be redirected to. Replace it with {your domain}.com.
```ShortIds``` is a private key that will be generated automatically.
```Public Key, Private Key``` — click the "Get new keys" button to create the keys automatically.

**Sniffing**, **HTTP**, **TLS**, **QUIC**, **fakedns** are **not enabled**.

If everything is configured **correctly**, the interface should look like **this**:

![image2](https://firstvds.ru/sites/default/files/all_images/instructions/xray_vpn/image_15.png)

# Configuring the client for different OS
<!--Configuring-client-->

+ **Windows** - Invisible Man XRay
  1. Download the archive from **[GitHub](https://github.com/InvisibleManVPN/InvisibleMan-XRayClient/releases/)** and unzip it
  2. Go back to the 3X-UI GUI and add a new client by following these steps: first, click the Menu button in the previously created configuration, then select Add User. In the Email field, enter the client's name, for example, "My Windows", and select xtls-rprx-vision in the Flow section.
  3. Expand the list of clients by clicking on the plus icon. Next to the newly created "My Windows" client, under the Menu item, click on the information icon.

  ![image3](https://firstvds.ru/sites/default/files/all_images/instructions/xray_vpn/image_17.png)
  ![image4](https://firstvds.ru/sites/default/files/all_images/instructions/xray_vpn/image_18.png)

  5. Copy the connection URL by clicking on the copy button located under the URL label.
  6. Transfer this link to your computer in any convenient way and copy it there.
  7. Launch the **Invisible Man XRay** application and open the ```Manage server configuration``` section.
  8. Click on the plus button in the lower right corner of the screen.
  9. Then select the ```Import from link``` option and paste the previously copied link into the appropriate field.
  10. If you have done everything correctly, a new configuration should be added. Close this manager and click ```Run```.
  11. It's done! We also set up a VPN on a computer running the Windows operating system without any problems.
+ **MacOS** - V2Box
  1. Download the app from the **[App Store](https://apps.apple.com/ru/app/v2box-v2ray-client/id6446814690)**.
  2. In **3X-UI**, we create a new client and copy the client's key.
  3. Open the **V2Box** app, tap ```+``` import v2ray from clipboard.
  4. The profile has been successfully added! Now select the connection, click ```Connect```, give permission to add the VPN configuration, and start using the VPN connection.
+ **IOS/Android** - V2Box
  1. Download the app from the **[App Store](https://apps.apple.com/ru/app/v2box-v2ray-client/id6446814690)** or **[Play Market](https://play.google.com/store/apps/details?id=dev.hexasoftware.v2box)**.
  2. In **3X-UI**, we create a new client.
  3. Open the list of clients and under the menu, next to the newly created client, click on the QR code icon.
  4. Open the **V2Box** app, tap ```+``` Import v2ray from the clipboard or scan the QR code from the panel by clicking on the corresponding icon:

  ![image5](https://firstvds.ru/sites/default/files/all_images/instructions/xray_vpn/image_20.png)
  
  6. The profile has been successfully added! Now select the connection, click Connect, give permission to add the VPN configuration, and start using the VPN connection.
 
# Sources
<!--Sources-->

The **[article](https://firstvds.ru/technology/kak-sozdat-i-nastroit-svoy-vpn-na-servere)** from which the information was taken
