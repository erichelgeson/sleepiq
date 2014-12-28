# Documenting the SleepIQ API
My bed has an API, so I may as well document it.

<https://sleepiq.sleepnumber.com/>

## APIs
### swagger.yml
This file contains the API documentation in `http://swagger.io` format.

Preview/edit the docs here: <http://editor.swagger.io/#/preview?import=https://cdn.rawgit.com/erichelgeson/sleepiq/master/swagger.yml>

### Other
There are a few other endpoints not under the `/rest` api the Ember web app uses.

* http://svcsleepiq.sleepnumber.com/bam/device/getConfig.jsp
* http://svcsleepiq.sleepnumber.com/bam/device/getSoftware.jsp
* https://svcsleepiq.sleepnumber.com/bam/device/getTime.jsp
 * Returns epoch time

## Bed notes
### Configuration
The Sleep Number bed is configured with a USB key and a `.conf` file that is downloaded from the API. The USB keys can be inserted into the Bed to update configuration.

`bam-init.conf`
```
accountNumber = -9999999999999999999
useOpenWifi=0
useHiddenSSID=1
# ssids: [PUTYOURSSIDHERE]
mfgEnable=false
bam-conf=http://svcsleepiq.sleepnumber.com/bam/device/getConfig.jsp
bam-prep=http://svcsleepiq.sleepnumber.com/bam/device/getSoftware.jsp
tunnelURL= devices.zepp.bamlabs.com
timeURL=https://svcsleepiq.sleepnumber.com/bam/device/getTime.jsp
bam-wpa=<public key>
```
# Tech Notes
* Webapp is an Angular.js app
* Phone pairs with bed via bluetooth but is not a discoverable device on my Mac.
* Tech Stack seems to be Java based and hosted in AWS.
* Sessions and ELBs are sticky and Cookies are required for the API, only `JSESSIONID` and `AWSELB` are required.
* Passwords are limited to 30 characters, but no feedback is given. If you create a password that is 35 characters long it will save, then delete 5 characters and you can login.
* Cookie has user/pass in it, not marked as http-only or secure. Pen testers are rolling over in their graves.

# Todo
* Render Swagger API
* See if phone app uses different APIs or auth.
* Writeup blog post with all this.
