# intunemapscore

Intune Device Compliance check for iOS devices with Cloudflare Access

This solution leverages two device posture checks 

1. Device UUID https://developers.cloudflare.com/cloudflare-one/identity/devices/warp-client-checks/device-uuid/
2. Custom Service Provider https://developers.cloudflare.com/cloudflare-one/identity/devices/service-providers/custom/


Event Flow

![intune-s2s](https://github.com/user-attachments/assets/cc35dbdb-6441-40ef-837d-236eee84069e)




More detail:

Logpush events for the Device UUID check are sent to a Worker. 

Worker : 

1. creates/updates a map of Cloudflare [DeviceID : Intune deviceid] stored in KV/D1
2. requests compliance.State from Graph API for a deviceid
3. converts compliance.State to s2s_score
4. creates/updates a map of Cloudflare [DeviceID : s2s_score] stored in KV/D1

The Device UUID check does not have to pass or be applied to a traffic policy

The Custom Service provider check will be applied to polices





