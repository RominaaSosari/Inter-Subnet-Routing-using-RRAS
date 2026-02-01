# Inter Subnet Routing using Windows Server Routing (RRAS)
Scenario: An organization has multiple departments, each located in a separate IP subnet. To enable communication between these isolated networks, Windows Server is used as a software-based router by implementing Routing and Remote Access Services(RRAS)


Lab Environment (in Hyper-V):


    2 Windows Server (Router)
    3 Windows Client (Windows 10)
    3 Virtual Switch (Private Switch)

Design:
  -Each Subnet uses a unique IP Address range
  -Windows Server routes handle traffic routing between subnets
  -Clients uses the router's interface as their default gateway

Network Topology: (Screenshots/Topology.drawio.png)


  
Implementation:




    Router Server 1 (Windows Server):
     -Role: Routing and Remote Access(RRAS)
     -multiple network interface
     -2 virtual network adapters(Private 1 & Private 2):
         IP Private1: 192.168.1.254, Subnet mask: 255.255.255.0
         IP Private2: 192.168.2.254, Subnet mask: 255.255.255.0

    Router Server 2 (Windows Server):
     -Role: Routing and Remote Access(RRAS)
     -multiple network interface
     -2 virtual network adapters(Private 2 & Private 3):
         IP Private2: 192.168.2.253, Subnet mask: 255.255.255.0
         IP Private3: 192.168.3.254, Subnet mask: 255.255.255.0

    Client 1 (Windows Client):
     Windows10-1 connected to Virtual Switch Private1
     IP: 192.168.1.1, Subnet Mask: 255.255.255.0, default gateway: 192.168.1.254

    Client 2 (Windows Client):
     Windows10-2 connected to Virtual Switch Private2
     IP: 192.168.2.1, Subnet Mask: 255.255.255.0, default gateway: 192.168.2.254

    Client 3 (Windows Client):
     Windows10-3 connected to Virtual Switch Private3
     IP: 192.168.3.1, Subnet Mask: 255.255.255.0, default gateway: 192.168.3.254

  Routing Method:
     Static routes were configured (on RRAS Console) on each router to ensure proper traffic forwarding between subnets. 

     
     static route for Router 1 --> (Screenshots/static route in router1.PNG)
     static route for Router 2 --> (Screenshots/static route in router2.PNG)

 Validation & Testing:
   Verified connectivity using ping between clients in different subnets



   
      [ping 1 -> 2] (Screenshots/ping from win10-1 to win10-2.PNG)
      [ping 1 -> 3] (Screenshots/ping from win10-1 to win10-3.PNG)
      [ping 2 -> 3] (Screenshots/ping from win10-2 to win10-3.PNG)
      [ping 3 -> 1] (Screenshots/ping from win10-3 to win10-1.PNG)
      
      
         

    
         
  
   
