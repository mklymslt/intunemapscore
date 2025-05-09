# intunemapscore

Intune Device Compliance check for iOS devices with Cloudflare Access

This solution leverages two device posture checks 

1. Device UUID https://developers.cloudflare.com/cloudflare-one/identity/devices/warp-client-checks/device-uuid/
2. Custom Service Provider https://developers.cloudflare.com/cloudflare-one/identity/devices/service-providers/custom/



![ios-intune-compliance drawio](https://github.com/user-attachments/assets/8325e68d-66ae-4530-a50c-868edb242a1f)


How it works:

Logpush events for the Device UUID check are sent to a Worker.

Worker then :

1. creates/updates a map of Cloudflare [DeviceID : Intune deviceid] stored in KV
2. requests compliance.State from Graph API for a device id
3. converts compliance.State to s2s_score
4. creates/updates a map of Cloudflare [DeviceID : s2s_score] stored in KV



