#Routers and Switches

We are currently at an inflection point when it comes to the ability to device programability directly to a router or switch. NETCONF was extended into IOS in 2005 but the lack of a consistent data model limited adoption. Depending on the platform there are multiple options for accessing the deivce directly.

##WSMA - Web Services Management Agent

WSMA was Cisco's first real attempt at exposing the router to programitic interfaces. The WSMA relies on the integrated HTTP server to allow for sending data in an XML format. 

To enable the WSMA

~~~
ip http authentication local

Once enabled a user can send XML to either set configruaiton or request statistics through show commands. In the example below a user is requesting 'show interface gig2' from a router.

~~~
<?xml version="1.0" encoding="UTF-8"?> 
The router sends the following response

~~~
 <response 

The challenge with using WSMA is the command strucute is fairly picky. Command strings sent are essentially CLI which means any variation in platform CLI will require script modification.

Adam Radford wrote a series of python scripts that leverage WSMA to provide basic router management. You can access his git repository at

~~~
https://github.com/aradford123/wsma_python
~~~

##Netconf/YANG
In 2012 Cisco started standardizing on Netconf/YANG as the methodoly for direct programming of IOS devices. For routing platforms we started introducing Netconf/YANG in IOS-XE 3.17 while the rest of the platforms saw support added with Polaris (IOS 16.x). 

To validate what a device can support use

~~~
ssh -p2022 -l sdn <host address> -s netconf  

The device will respond back with all the various model types supported. 

