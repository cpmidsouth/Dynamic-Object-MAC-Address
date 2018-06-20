This script takes advantage of the dynam_obj_upd.sh script originally written by Nuno Sousa & CB Currier.

It has been modified to use a list of MAC addresses to update a dynamic object with IP addresses from those MAC addresses. This script can ONLY be ran on the gateway itself. The dynamic object must already be created and part of the policy other wise you are creating an object that has no use. The script utilizes cpd_sched to schedule an automatic update.

Directions:
  - Move the files onto the gateway in a location of your choosing. Use the TAR File
  - Add MAC Addresses to mac_list.txt
    - make sure they are formatted correctly by running 'arp -n' and copy/paste from there.
  - Edit the variables in dynam_obj_upd.sh to match your needs
    - IP_LIST=/path/to/ip_list.txt (NOTE: This file will be built where you direct it here. It does not need to be pre-built)
    - MAC_LIST=/path/to/mac_list.txt
    - timeout=300  (this is how often you want the FW to poll the file for new IPs default is 5 min. Time is in seconds)
  - mv dynam_obj_upd.sh $CPDIR/bin/
  - cd $CPDIR/bin
  - Execute Script:
      - dynam_obj_upd.sh -o OBJECT_NAME -f /path/to/ip_list.txt -a on   (this will schedule automatic update based on timeout)
      - dynam_obj_upd.sh -o OBJECT_NAME -f /path/to/ip_list.txt -a run  (this will run the script once immediately)
  - To Disable Automatic Updates:
      - dynam_obj_upd.sh -o OBJECT_NAME -a off

You can verify updates in the log file: $FWDIR/log/dynam_obj_upd.log
