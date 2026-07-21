#
#
#
#
#
#
#
#

Welcome to RockiT! This is a all in one system for taking the micro management out of rocketeering!
This was a solo project, although my finacee did assist with the building of many of the rockets this was tested and built in,
alongside endless encouragement that helped us reach 1.0.
We hope you enjoy it as much as we do .
Get out there and RockiT like a spaceman!

The main features in the v1.0 release are:

Rockets manage their own flights, allowing for easy multiflight without having to enter the rocket UI at all, in the current release
this only goes as far as remembering where the rocket was last working, but this does allow for repeat
launches of the same rocket only using the launch command inputs. Flights will recall for a number of reasons, keeping your rockets safe
and productive!

Flight programs for miner rockets and scanning rocket to enable easy repeat flights. Supporting up to 8 rockets!

Automated tower extension, retraction and refuelings taking the stress and tedium out of landing and launching
as its all fully automated you can focus on other tasks and just check back at mission control for when its time to hit the launch button.

A simple to use command center featuring simple rocket selection and epic one button launch system with saftey control!

Visual feedback off all of the above!

How to use

To use the system is very simple. Enter your control room, select the rocket you want to launch using a dial
Once you have the wanted rocket selected the status feedback LED will let you know the current state of the ship
these are critical, replace mining head, resupplying, launch ready, need destination, in flight and returning.
As this will be the first flight you will need to use the rocket UI on the computer to pick where you will be mining.
With your selected rocket you will need to pull the lever open, which will unlock and flip open the important button used to trigger the rocket.
Now it the umbilicals will retract, the warning lights come on and there are 30 seconds until the flight commences.
The rocket will self manage the entire mission and return back to where it launched from
once landed if the node it was working at is not exhausted it will keep that destination ready for you to hit the launch button again.
Once its done refuelling of course

How to set up

Before you begin

Each rocket will require : 1 IC housing and chip, 1 pipe analyser 
(for rockets that use oxy and add another analyser to the oxy line, it works on averages so its fine)

Each tower will require :  2 IC housings and chips, 1  pipe analyser, 1 turbo pump (2 of each if your running dual fuel)

Mission control will require : 3 IC housings and chips, 3 logic switch's, 2 lights

Communications will requre, per rocket : 1 rocket datalink, 1 logic transmitter, 2 logic memory


Be aware when setting this up computers count from 0, not 1! So the first rocket will be 0!
To expose named screws turn the power on the IC housing after putting in the chips.

Launch site

Each rocket requires its own launch site, each rocket much have a unique colour as the selector uses a coloured LED as feedback

The Rocket
The script for the rocket controller come in 2 versions depending on ship type
Mining ships need to have the destionation set to a resouce node, they will remember the location they last worked at and keep self setting it untill the 
node is depleted.
Scanner ships are only set for discovery in this version. Set destination to the location and they will discover untill 9 sites are found and then 
return home.
For both scouts and miners you will need to name the rockets IC housing to "RockiT Brain"
For the mainBattery you want this to be the battery that discharges last, you will still need a reserve auxiliary battery separate to this.
This can easily best tested by numbering your batteries allowing them to charge, disconnecting the umbilicals.
Make sure to get this right as it is used as a trigger to recall the rocket.
All the device screws in the housing are named so it should be fairly simple to work out what needs screwing in.
Naming your rocket downlinks is essential.

The Tower
This will use 2 different scripts, the versions of each depending if your set up uses a fuel that requires an oxidiser or not.
The scripts are all named in the steam collection so should be simple enough to figure out.
All the device screws in the housing are named and the only thing that may need extra explanation is the umbilical
It doesnt matter which one it is, its looking for the error state so it does keep trying to dribble fuel in while the rocket is away.
They require the appropriate number of liquid pipe analysers and turbo pumps connecting to enable the refuel to be automated.
You will need a logic transmitter on the circuit in passive mode, I would name these "Tower0,Tower1" etc naming scheme is not critical on these
however you will need to screw the active connection to them so you will need to be able to tell which is which.

Mission Control

Your launch control will require: 1 selected ship indicator LED, 1 ship status LED, 1 selection dial, 1 important button, 1 safety lever.
In game kits that is 3 logic switches and 2 lights.
This physical dial controls how many rockets the system can control, if you only have 2 set the dial to 1 to expose the 0 and 1 values.
The control room will use 3 different scripts

Mission Control will also need share a data network with the communications area.
This area will need, per rocket you wish to connect to this system,1 rocket datalink 1 logic transmitter and 2 memory chips.
The naming on all of these is critical. As the system can support 8 rockets we will number the 0-7
For the rocket uplink the code is set to search for the compact version. If you wish to use the large version change line 15 in the "Launcher" script to
"define TXHASH -1256996603"
This device must be screwed to set the connection to the correct rocket
We must rename the actual part to, while remember to update the number in line with which rocket we are selecting
"Logic Uplink0"
The logic transmitter must be named, once again updating the number for rockets past the 1st
"Logic Transmitter0"
This will need to be screwed in to select the connection, this is why we named the passive side earlier
The two memory chips must be named, when you update the number on these it is the FIRST number you update
"Logic Memory00" and "Logic Memory01"
These will be used by the status updater to know if a rocket is a scanner or a miner, and to know if it home
as such we must set the values on these. 
X0 is the ship type for this 0 (default value) will be miner and 1 will be a scanner. 
So if rocket 6 was a scout, the chip name and setting would be 
"Logic Memory50" with the memory chips setting value as "1"
X1 is for the ships home location, you can get this by aiming a screwdriver at the launch mount, you dont need all the 0's
So for the example ship 1 is a miner with a home site that ended 40-11, when we built the ship we made sure to name the ship rocket downlink "Sara's Grace"
we know everything we need to know to set up the connection
Logic Memory00      = 0 (because this is 0 we dont need to edit it just rename the memory chip)
Logic Memory01      = 4011 
Logic Uplink0       = "Sara's Grace" (on the connection screw)
Logic Transmitter0  = active mode, "Tower0" (on the connection screw)
We need to do this physical install for all 8 ships on the network
A final example will be ship 6, it is a scout, its home site ended 43-11, we named the rocket data downlink "90th Birthday"
Logic Memory50      = 1
Logic Memory51      = 4311
Logic Uplink5       = "90th Birthday"
Logic Transmitter5  = active mode, "Tower5"

Remember computers count from 0, not 1!
The communications center is the most complex part of this, with that done we can move up to the launch controls!

In the control center you will need to install 2 LED's, 1 lever, 1 important button and 1 dail. These must be connected to the same data circuit
as the communications center, you will need 3 IC 10 housings and chips to go with them.
The LEDs will need to be named to separate them as the dial uses one and the status light uses another


Launcher
This device set up is fairly easy, all the screw connections are named.

Dial
This device is simple to set up, all the screws are named.
You can limit this to the number of rockets you have connected.
Within the scripts you can either follow the colour scheme of the rockets I was using when building the system or set them your self
on line 32 you can see the text that needs changing it is the number at the end you change to set the colour and you set it as such
0	Blue	
1	Gray	
2	Green	
3	Orange	
4	Red	
5	Yellow	
6	White	
7	Black	
8	Brown	
9	Khaki	
10	Pink	
11	Purple	
The code for further rockets can be found on lines: 44 56 68 80 92 104 116

Status
All screws are named, remember to use a different LED from the dial.
As long as the guide has been followed fully up to this point this system will function.
The light codes are:
Solid Red         = Critical - the system is not reading any power in the selected ships battery
Flashing Red      = Replace mining head
Flashing Yellow   = Restock in progress
Solid Yellow      = Ship stocked but no destination (remember the ship will store the node it was last mining but you do need to set the node for first flight)
Green             = Flight Ready - go ahead pull the lever and hit the button!
Solid Blue        = Flight in progress
Flashing Blue     = Flight returning

Setting Initial destinations
During testing I found that having the computer with the rocket motherboard on the same network as the dail caused it to stay locked onto the first rocket
regardless of which datalink was powered. With this I moved my computer to a different data network with a single uplink I manually cycle.
