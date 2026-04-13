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
- The Networking Capabilities - 1 GB ethernet port, ideal since we will be downloading large files and streaming them as well. (4K is no joke)

# Creating The Installation Media
- Download RUFUS on the seperate computer.
- Download a copy of ZimaOS.
- Use RUFUS to create the installation media on the flash drive.

- # Installing ZimaOS
- Plug the USB into the mini pc
- Turn on the mini pc and boot into the computers BIOS
- Navigate to the Boot priorities and select the USB and boot priority 1. Change boot type to UEFI.
- Disable secure boot
- Save bios and let the system boot into the ZimaOS installer from the USB
- Run through the basic set up and select the mini PC's internal ssd as the install location
- Format the drive and proceed with the installation (FORMATTING WILL COMPLETELY REMOVE WINDOWS THIS IS THE POINT OF NO RETURN)
- Remove the usb so boot priority is set back to the internal ssd and reboot the machine

# Setting up ZimaOS
- Once the machine has rebooted it will show you the terminal. From here you can view you devices IP address and set a root password by following the on screen instructions.
- Type your mini PC's IP address into your browser on the machine you used to create the installtion media. From here you can set up ZimaOS through the web client. This is how the server will be configured and controlled from now on.

# Setting up the DAS
- Now that our server is set up we can take our hard drive and mount it inside of our drive cage.
- Plug your DAS into power and your mini PC's fastest usb port.
- Turn on your DAS.
- Restart your server from the ZimaOS web app
- Navigate to the ZimaOS Storage tab inside of settings. If your drive is already setup and good to go, awesome, otherwise we have to format and mount the drive using the Shell terminal.

# Mounting the Drive with Shell
- Navigate to the general settings within the ZimaOS web app, go to general -> developer settings -> enable SSH access -> click web terminal
- Login to the terminal using the login you setup for root.
- Run: lsblk (this will give you a list of your connected hardware)
- Look for something like sdb1, this will be the name of you drives USB partition
- Create a mount point by running: sudo mkdir -p /mnt/usb
- Next mount the drive by running: sudo mount /dev/sdb1 /mnt/usb
- Now your drive should be mounted and accessible through the ZimaOS web client

# Setting up Plex
- First access your drives files with the files app within the web client
- Add a folder and name it 'Media' then create 3 folders inside named 'Movies', 'TV Shows', and 'Music'
- Navigate to the appstore within the ZimaOS web client.
- Search for Plex and install
- Open the Plex App settings before running, ensure that network is set to HOST, and that WEBUI is set to your servers IP and the port to 32400
- Under volumes leave the folder that says '/DATA/AppData/plex/config' alone, for the path underneath set the file path the Media folder you just created on your drive
- Now you can add your medias raw files to their respective folders on your drive and plex will automatically pull meta data and sort them within the plex client.
- Open plex and follow the set up instructions to create your account and preferences

# Setting up Remote Access to Plex
- First navigate to your routers admin control page, this can be done by looking at the bottom of your router and typing in the routers IP address into your browsers search bar.
- Navigate to DHCP Server/ DHCP Reservation tab
- Find your mini PC's name and set the machines IP address to static/reserve.
- Navigate to your routers port forwarding settings.
- Select the server and add the port 32400 and set it to TCP so we have a reliable way to stream our content (If set to TCP/UDP or UDP, your streams may drop frames and audio), this is the default port that plex uses and must be set if you want to access your content when not connected to your network.
- Open the Plex app from within the ZimaOS client and navigate to the settings.
- From here navigate to remote access and enable it.
- If you get an error saying you don't have remote access, manually specify the port as 32400
