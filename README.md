# tenable.io-autoscan.py
Python script to manage Tenable.io assets first agent scan.


#***********************************************************************

#I have moved onto another company and no longer have tenable.io access#
#If you find issues, please update and submit a pull request.          #

#***********************************************************************

### Purpose
The purpose of this script is to automate certain Tenable.io agent-based scanning tasks. A proper admin should make sure that all their assets have been scanned immediately after agent software provisioning.
#### Use case
The script is programmed to do two simple tasks.
##### Add
The first option, will check the Last Scanned status of every asset in your Tenable.io tenant. If it detects a host that has never been scanned, the script will add it to a specific group as configured in the script (for the sake of the example, we will call such group "Unscanned".).
##### Delete
The second option will check the Last Scanned status of every asset, but this time only those that belong to your Unscanned group. If the script detects a host that has already been scanned, it will pull the host out of the \[Unscanned\] group.  
The joy behind this script is that allows Tenable.io administrators to make sure that every new agent provisioned to the console will be scanned. For this automation to happen, the administrators will require to have a concise schedule plan.
##### Logging
There is an option of --log that accepts a flag of 'debug,info,warning,error,critical' -it will log to a script.log file in the same folder the script is ran from
#### Schedule example
08:00 Launch script with --add parameter  
09:00 Execute a daily scheduled basic agent scan of the Unscanned group (12h scan window)  
20:00 Launch script with --delete parameter  
### Requirements
#### Python libraries
```
os
logging
dotenv  
argparse  
tenable.io -> Source: https://github.com/tenable/pyTenable  
sys
```
#### Script parameters
You **MUST** configure the API keys either through dotenv (as specified in line 29 in the script) OR manually (as specified in line 30 in the script). For more information regarding initial API setup, please refer to the official documentation contained here -> [📖](https://developer.tenable.com/docs/introduction-to-pytenable)  
You **MUST** configure the target_group variable. Replace the XXXXX with whatever group you want to put the agents that never have been scanned. You can extract the group ID from the browser's URL when you're managing the group that you want to use in Tenable.io.  
### Usage
Simply enough, execute one of the following:
```
python3 tenableio_autoscan.py --add
python3 tenableio_autoscan.py --delete
python3 tenableio_autoscan.py --add --log error
python3 tenableio_autoscan.py --delete --log error
```

### Terms and Conditions of Usage
Please, refer to the LICENSE contained in this repository for further information.

### Distinguished Contribuitors
[mixedup4x4](https://github.com/mixedup4x4) [☕](https://www.buymeacoffee.com/mixedup4x4W)
