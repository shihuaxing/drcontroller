How to use neutron-handler.py
===================


 neutron-handler.py can handle the client request of 'primary site' about network , and replicate shadow ofthe network in the 'secondary site'.

----------


neutron-handler can handle the following six commands:
-------------


    net-create
    subnet-create
    net-delete
    subnet-delete
    net-update
    subnet-update



----------


the followings will show you how to work the neutron-handler.py.
-------------------

##'python http_server.py' to listen the request of client.

  1. connect the  drcontroller-neutron of docker container in primary site(10.175.150.15).
  2. use the command "cd  /home/eshufan/projects/drcontroller/drcontroller ; python  http_server.py"to start the client forwarding.

## 'create' test for net/subnet

  1. In primary site, create the networks 'net1' and 'net2', secondary site  will automatically create the replications of  the two network , 'net1_shadow' and 'net2_network';
  2. In net1, create the subnets 'net1-subnet1' and 'net1-subnet2', and , in net2, create the subnet 'net2-subnet1',so secondary site will show 'net1-subnet1_shadow' and 'net1-subnet2_shadow' in net1_shadow , and net2-subnet1_shadow in  net2_shadow .
  3. the specific commands are following:
    
         # neutron  net-create net1
         # neutron  net-create net2 
         # neutron subnet-create --name net1-subnet1 net1 20.0.0.0/24
         # neutron subnet-create --name net1-subnet2 net1 30.0.0.0/24
         # neutron subnet-create --name net2-subnet1 net2 40.0.0.0/24
    
## 'update' test for net/subnet
 
1. rename the netwrok 'net1' of primary site  to 'net1-update',  the subnet 'net1-subnet1' to 'net1-subnet1-update', then the 'net1_shadow' and 'net1-subnet1_shadow' of secondary site will be renamed to 'net1-update_shadow' and 'net1-subnet1-update_shadow', respectively.
2. the specific commands are following:
    
         # neutron net-update net1 --name net1-update
         # neutron subnet-update net1-subnet1 --name net1-subnet1-update
     	

##'delete' test for net/subnet 

1. In primary site, delete 'net2-subnet1' and 'net2',the 'net2-subnet1_shadow' and 'net2_shadow' of secondary site will be also  deleted 
2. Continue deleting 'net1' of primary site ,then 'net1_shadow'  and its  subnets of secondary site will be deleted.
3. The specific commands are following:

         # neutron subnet-delete  net2-subnet1 
         # neutron net-delete net2
         # neutron net-delete net1
     
