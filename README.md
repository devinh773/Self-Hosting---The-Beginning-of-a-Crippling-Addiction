# Self-Hosting - Building A Home Media Server
Building a home media server, then setting up the network so my media can be accessed from anywhere.

# Hardware Used
- KAMRUI Essenx E2 N150 Mini PC
- ORICO 2 Bay Hard Drive Enclosure
- Western Digital WD40EFRX (WD-RED 4TB)
- Provided Xfinity Modem/Router
- Primary Desktop
- USB Flash Drive (FAT32)

# Operating Systems
- Windows 11
- ZimaOS (linux)

# Prereqs
- A Seperate machine other than the mini pc that will host our server - This will be used to create our media installation
- RUFUS - this is the pogram used for creating our installation media
- A Flash Drive, preferrably USB 3.0 for speed

# Choosing an OS
Here I already chose ZimaOS for my build but there is a multitude of opperating systems you could use to host your own media server with diferent levels of granularity.
I chose ZimaOS because it is a super light weight linux distribution that is managed from a webapp with a easy to use UX (very low system overhead). This is paramount because I chose a relatively low powered mini pc that peaks at 15 watts and I want as little system overhead as possible so I can direct all of my compute to encoding my media streams. 
Apps run on Docker so I won't need to fiddle with the terminal for application installation.
Shell is accesible from the webapp so I can manage the server without needing to pull it out and set up peripherals after the initial installation and set up.

# Choosing a Mini PC
This is where your choice matters depending on your budget and what you want out of your server.
I chose the KAMRUI Essenx E2 for 4 main reasons:
- The Form Factor - This is going to be tucked away near the router, the smaller the better so it's not an eye sore or inconvenience.
- The Memory - 16 GB of DDR4, more than enough to do more with the server down the line when I decide to and fast enough for my use case.
- The CPU - Supports Modern Codec for video streaming (H.264, H.265, AV1, VP9) which is ideal for streaming 4K content, supports hardware encoding for multiple streams at the same time, additionally very effecient and pulls low power.
- The Networking Capabilities - 1 GB ethernet port, ideal since we will be downloading large files and streaming them as well. (4K is no joke).

# Creating The Installation Media
- Download RUFUS on the seperate computer.
- Download a copy of ZimaOS.
- Use RUFUS to create the installation media on the flash drive.
<img width="474" height="539" alt="rufus" src="https://github.com/user-attachments/assets/cf331b22-9f01-4aa6-a5a5-3cfc7638f517" />

- # Installing ZimaOS
- Plug the USB into the mini pc.
- Turn on the mini pc and boot into the computers BIOS.
- Navigate to the Boot priorities and select the USB and boot priority 1. Change boot type to UEFI.
- Disable secure boot.
- Save bios and let the system boot into the ZimaOS installer from the USB.
- Run through the basic set up and select the mini PC's internal ssd as the install location.
- Format the drive and proceed with the installation (FORMATTING WILL COMPLETELY REMOVE WINDOWS THIS IS THE POINT OF NO RETURN).
- Remove the usb so boot priority is set back to the internal ssd and reboot the machine.

# Setting up ZimaOS
- Once the machine has rebooted it will show you the terminal. From here you can view you devices IP address and set a root password by following the on screen instructions.
- Type your mini PC's IP address into your browser on the machine you used to create the installtion media. From here you can set up ZimaOS through the web client. This is how the server will be configured and controlled from now on.
<img width="4284" height="2941" alt="zima" src="https://github.com/user-attachments/assets/889b1a2b-d0f8-406b-bafb-b0f240e34d9e" />

# Setting up the DAS
- Now that our server is set up we can take our hard drive and mount it inside of our drive cage.
- Plug your DAS into power and your mini PC's fastest usb port.
- Turn on your DAS.
- Restart your server from the ZimaOS web app.
- Navigate to the ZimaOS Storage tab inside of settings. If your drive is already setup and good to go, awesome, otherwise we have to format and mount the drive using the Shell terminal.

# Mounting the Drive with Shell
- Navigate to the general settings within the ZimaOS web app, go to general -> developer settings -> enable SSH access -> click web terminal
- Login to the terminal using the login you setup for root.
- Run: lsblk (this will give you a list of your connected hardware).
- Look for something like sdb1, this will be the name of you drives USB partition.
<img width="615" height="1026" alt="lsblk" src="https://github.com/user-attachments/assets/e8cf8893-0000-4349-8710-f45555ee285d" />

- Create a mount point by running: sudo mkdir -p /mnt/usb
- Next mount the drive by running: sudo mount /dev/sdb1 /mnt/usb
- Now your drive should be mounted and accessible through the ZimaOS web client.
- Now go to your files on the machine used to create the installation media.
- Open your files and right click on 'This PC' then select add network location.
- Add the IP address of your ZimaOS machine and enter your login info.
- Now you can access your servers drives with your main machine through the network.


# Setting up Plex
- First access your drives files with the files app within the web client.
<img width="697" height="653" alt="drivesmedia" src="https://github.com/user-attachments/assets/6deba565-2452-49a6-93a7-e39324caacfd" />

- Add a folder and name it 'Media' then create 3 folders inside named 'Movies', 'TV Shows', and 'Music'.
<img width="717" height="657" alt="drivesmedia2" src="https://github.com/user-attachments/assets/8d3e843b-33fa-4e61-891a-b4d8237cc2b0" />

- Navigate to the appstore within the ZimaOS web client.
- Search for Plex and install.
- Open the Plex App settings before running, ensure that network is set to HOST, and that WEBUI is set to your servers IP and the port to 32400.
- Under volumes leave the folder that says '/DATA/AppData/plex/config' alone, for the path underneath set the file path the Media folder you just created on your drive.
<img width="645" height="1232" alt="plexsettings" src="https://github.com/user-attachments/assets/95e38b15-3562-4c14-af42-3d3e570aab22" />

- Now you can add your medias raw files to their respective folders on your drive and plex will automatically pull meta data and sort them within the plex client.
- Open plex and follow the set up instructions to create your account and preferences.

# Setting up Remote Access to Plex
- First navigate to your routers admin control page, this can be done by looking at the bottom of your router and typing in the routers IP address into your browsers search bar.
- Navigate to DHCP Server/ DHCP Reservation tab.
- Find your mini PC's name and set the machines IP address to static/reserve.
<img width="955" height="1089" alt="reserve ip 1" src="https://github.com/user-attachments/assets/21afc3fe-dd6f-471d-af73-5516e6f67985" />
<img width="954" height="621" alt="reserveip1" src="https://github.com/user-attachments/assets/e7c75624-d408-4d6c-8b9d-4cec12f3bf2f" />

- Navigate to your routers port forwarding settings.
- Select the server and add the port 32400 and set it to TCP so we have a reliable way to stream our content (If set to TCP/UDP or UDP, your streams may drop frames and audio), this is the default port that plex uses and must be set if you want to access your content when not connected to your network.
<img width="660" height="500" alt="Screenshot 2026-04-13 at 1 20 40 AM" src="https://github.com/user-attachments/assets/1608b205-b121-4cdd-9012-040ba6a413f4" />

- Open the Plex app from within the ZimaOS client and navigate to the settings.
- From here navigate to remote access and enable it.
- If you get an error saying you don't have remote access, manually specify the port as 32400.
<img width="1033" height="938" alt="plexremote" src="https://github.com/user-attachments/assets/cb77231b-314e-47b3-b249-28684810e089" />

