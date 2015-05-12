# bvcRestConfExample1
Example python application that works with RESTConf interface of Brocade Vyatta Controller (BVC) 1.1.1.  It subscribes for changes in topology and adds flows to flood packets from all hosts.

bvcRestConfExample1.py is an example Python application that demonstrates how to use the BVC RESTconf api.

The main goal is as an example of coding to BVC RESTconf api.

bvcRestConfExample1.py uses the BVC RESTconf api to provide packet forwarding between hosts even when the BVC Host Tracker's arphandler is configured to be in passive mode.

bvcRestConfExample1.py is not the best way to provide forwarding.  
bvcRestConfExample1.py is not the best Python code.
bvcRestConfExample1.py has been tested in only one environment: BVC 1.1.1 with HostTracker configured to use passive mode, Mininet in its default topology of one (1) switch and two (2) hosts, although it will probably work with other topologies - just has not been tested.
    

    PRE-REQUISITES:
       1.  Install python-requests:
             a.  sudo easy_install requests OR sudo pip install requests
       2.  Install websocket-client:
             a.  sudo easy_install websocket-client  OR  sudo pip install websocket-client

    SETUP:
       1.  Configure BVC 1.1.1 HostTracker to use passive mode
              - Edit the file /opt/bvc/controller/etc/opendaylight/karaf/54-arphandler.xml
       2.  Start BVC 1.1.1
              - /opt/bvc/bin/start
       3.  Start Mininet and set its controller to BVC
             sudo mn --controller=remote,ip=<ip of BVC>
       4.  Make sure that you can ping the ip of BVC from where you will run bvcRestConfExample1

    RUN:
       1.  At the command line:
             bvcRestConfExample1 --controller <bvc_ip>

           WHERE:
               <bvc_ip> is the ip address of BVC (you should be able to ping it from 
                    where you are running bvcRestConfExample1)

    TRY IT:
       1.  Start bvcRestConfExample1 --controller <bvc_ip>
       2.  On mininet try these commands:
               h1 ping h2
               h2 ping h1

              - the hosts should be able to ping each other (something that normally
                fails when HostTracker is in passive mode).  Note, if you do a pingall
                the first pingall will have failures.  If you do pingall again it will
                work.  THis is because we do not program flows until AFTER the toplogy
                is updated (after the first ARP goes to the arphandler)

    USAGE:
       bvcRestConfExample1.py [options]

       Options:
         --controller <ip address>  the IP address of the BVC 1.1.1 (you should be able to ping it). Example:  192.168.56.101
         -h                            this help

