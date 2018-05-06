# import the downloaded cEOS-lab.tar.xz image
docker import cEOS-lab.tar.xz ceosimage:4.20.5F

# create docker instances with needed environment variables
docker create --name=ceos1 --privileged -e CEOS=1 -e container=docker -e EOS_PLATFORM=ceossim -e SKIP_ZEROTOUCH_BARRIER_IN_SYSDBINIT=1 -e ETBA=1 -e INTFTYPE=eth -i -t ceosimage:4.20.5F /sbin/init
docker create --name=ceos2 --privileged -e CEOS=1 -e container=docker -e EOS_PLATFORM=ceossim -e SKIP_ZEROTOUCH_BARRIER_IN_SYSDBINIT=1 -e ETBA=1 -e INTFTYPE=eth -i -t ceosimage:4.20.5F /sbin/init

# create docker networks
docker network create net1
docker network create net2

# connect docker instances to the networks
docker network connect net1 ceos1
docker network connect net1 ceos2
docker network connect net2 ceos1
docker network connect net2 ceos2

# start the instances
docker start ceos1
docker start ceos2

# wait for a few minutes for all EOS agents to start

# issue 'Cli' command to be presented with EOS CLI.

core@core-01 ~ $ docker exec -it ceos1 Cli
localhost>en

localhost#show version
Arista cEOSSim
Hardware version:
Serial number:       N/A
System MAC address:  0242.acf9.ee11

Software image version: 4.20.5F
Architecture:           i386
Internal build version: 4.20.5F-8127914.4205F
Internal build ID:      4d6b4859-39b5-4581-993b-f84ac0736664

cEOS tools version: 1.0

Uptime:                 7 hours and 27 minutes
Total memory:           8170952 kB
Free memory:            6449840 kB

localhost#show interfaces status
Port       Name        Status       Vlan     Duplex Speed  Type            Flags
Et1                    connected    1        full   unconf EbraTestPhyPort
Et2                    connected    1        full   unconf EbraTestPhyPort      
