# intunemapscore

A Cloudflare Worker that consumes Cloudflare Access Unique client ID Device Posture log events

Then :

1. creates/updates a map of Cloudflare [DeviceID : Intune deviceid] stored in KV
2. requests compliance.State from Graph API for a device id
3. converts compliance.State to s2s_score
4. creates/updates a map of Cloudflare [DeviceID : s2s_score] stored in KV



This solution leverages two device posture checks 

1. Device UUID https://developers.cloudflare.com/cloudflare-one/identity/devices/warp-client-checks/device-uuid/
2. Custom Service Provider https://developers.cloudflare.com/cloudflare-one/identity/devices/service-providers/custom/


Intune MDM embeds a deviceid value into the Cloudflare One iOS app using the mdm parameter 


![ios-intune-compliance drawio](https://github.com/user-attachments/assets/8325e68d-66ae-4530-a50c-868edb242a1f)



