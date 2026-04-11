# Self-Hosting - Building A Home Media Server
Time to set up my home media server with more plans in the future. For now we start small and acquire freedom from big streaming through creating a home media server while leveraging plex as my front end for my content.

# Hardware Used
- KAMRUI Essenx E2 N150 Mini PC
- ORICO 2 Bay Hard Drive Enclosure
- Western Digital WD40EFRX (WD-RED 4TB)
- Provided Xfinity Modem/Router
- Primary Desktop
- USB Flash Drive

# Operating Systems
- Windows 11
- ZimaOS (linux)

# Prereqs
- A Seperate machine other than the mini pc that will host our server - This will be used to create our media installation
- RUFUS - this is the pogram used for creating our installation media
- A Flash Drive, preferrably USB 3.0 for speed

# Choosing an OS
Here I already chose ZimaOS for my build but there is a multitude of opperating systems you could use to host your own media server with diferent levels of granualarity.
I chose ZimaOS because it is a super light weight linux distrobution that is managed from a webapp with a slick user interface. This is paramount because I chose a relatively low powered mini pc that peaks at 15 watts and I want as little system overhead as possible so I can direct all of my compute to encoding my media streams. I also chose ZimaOS because you can download docker application directly from their curated store front which has everything that I need for this project.

# Choosing a Mini PC
This is where your choice matters depending on your budget and what you want out of your server.
I chose the KAMRUI Essenx E2 for 3 main reasons:
- The Form Factor - While you can definitely do this with old enterprise workstations that youd find in schools and office enviroments and have it work perfectly fine, due to the memory shortage I decided to buy a brand new mini PC for around the same price as lower powered old workstations.
- The CPU and Memory - This computer is equipped with an Intel N150 and 16 Gigabytes of LPDDR4 memory. You could get away with half this amount of memmory and be just fine but this config will give me more headroom down the road if I decide to do more than stream medi. The real star of the show here is the CPU. The N150 is a hyper effiecient 14th gen Twin lake CPU equipped wtih 4 Cores and 4 Threads with a peak power draw of 15 Watts. This is important since this computer is going to be up at all times and only come down for maintenance or troubleshooting so I want it to be fast while also sucking as little power as possible. The second important thing here is that the N150 has superior transcoding capabilities and supports hardware encoding which I will need, if I want to run multiple 4K streams at any given time.
- The Networking Capabilities - This PC is equipped with a 1 Gigabit ethernet port which I am going to want since this computer will be wired to the router and will be receiving and sending large quantities of data.

# Creating The Installation Media
First things first, I will donwload RUFUS and a copy of ZimaOS

  
