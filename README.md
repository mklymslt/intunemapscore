# intunemapscore

Intune Device Compliance check for iOS devices with Cloudflare Access

This solution leverages two device posture checks 

1. Device UUID https://developers.cloudflare.com/cloudflare-one/identity/devices/warp-client-checks/device-uuid/
2. Custom Service Provider https://developers.cloudflare.com/cloudflare-one/identity/devices/service-providers/custom/


Event Flow


![image](https://github.com/user-attachments/assets/e6b9cc2c-055f-407c-92b6-d65b6423d942)


More detail:

Logpush events for the Device UUID check are sent to a Worker. 

Worker : 

1. creates/updates a map of Cloudflare [DeviceID : Intune deviceid] stored in KV
2. requests compliance.State from Graph API for a device id
3. converts compliance.State to s2s_score
4. creates/updates a map of Cloudflare [DeviceID : s2s_score] stored in KV



