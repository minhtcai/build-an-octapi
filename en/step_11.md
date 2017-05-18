# Controlling the cluster

The `cluster_action.sh` script runs on the client and uses SSH to administer the servers (that's why we used `ssh-keygen` to authenticate the client with the servers). It relies on the correct IP addresses of the servers being listed in the `ip_list` file. It is a good idea to delete this file when booting the cluster for the first time so that the list is regenerated.

1. From a terminal, type the following command to remove the `ip_list` file:

    ```bash
    rm ip_list
    ```

    **Note:** You may need to manually 'ssh' into each server from the client so that the client recognises each server ssh key properly. If needed, this will only happen once.
    ```bash
    ssh <ip address of server>
    ```


1. The following options are available as parameters accepted by the script:

**reboot** – this reboots all the servers (the client and router are ignored)

Example:
    ```bash
    ./cluster_action.sh reboot
    ```

**shutdown** – this shuts down each server and places it into a safe state. If a server is not shut down correctly, it may cause the micro SD card to be corrupted and cause the processor to fail to boot when next used.

Example:

   ```bash
   ./cluster_action.sh shutdown
   ```

**date** – this distributes the client date and time (to the nearest minute) to each server. The Raspberry Pi 3 does not have a real time clock, so the correct time will need to be set on the client first.

Example:
    ```bash
    sudo date -s “11 Apr 2017 12:42”
    ./cluster_action.sh date
    ```

**unicorn** – this option invokes the unicorn scripts on each server and passes it the name and location of a Pimoroni Python script as a parameter. You need to have start_unicorn.sh in /home/pi on each server as described earlier for this to work.

Example:
    ```
    ./cluster_action.sh unicorn /home/pi/unicorn-hat/examples/random_sparkles.py
    ```