# intunemapscore

Intune Device Compliance check for iOS devices with Cloudflare Access

This solution leverages two device posture checks and Cloudflare Workers

1. Device UUID https://developers.cloudflare.com/cloudflare-one/identity/devices/warp-client-checks/device-uuid/
2. Custom Service Provider https://developers.cloudflare.com/cloudflare-one/identity/devices/service-providers/custom/
3. Cloudflare Workers: https://developers.cloudflare.com/workers/
4. Cloudflare KV https://developers.cloudflare.com/kv/


Event Flow

![intune-s2s](https://github.com/user-attachments/assets/cc35dbdb-6441-40ef-837d-236eee84069e)




More detail:

Logpush events for the Device UUID check are sent to a Worker. 

Worker : 

1. creates/updates a map of [ Cloudflare DeviceID : Intune deviceid] stored in KV
2. requests compliance.State from Graph API for a deviceid
3. converts compliance.State to s2s_score
4. creates/updates a map of Cloudflare [Cloudflare DeviceID : s2s_score] stored in KV


The Custom Service provider check consumes the s2s_score and is applied to Cloudflare polices. As an example can allow or block traffic to an App or URL based on the score threshold 


**Intune paraameter**


    <key>unique_client_id</key>
    <string>{{deviceid}}</string>
  


**Graph API devices response** 

{
"id": "f65083ac-4cd3-21c6-a106-a1a5abc94e58",
"userId": "101723da-5432-4677-a76e-0fa2b0b04a2a",
"deviceName": "Test iPhone",
"managedDeviceOwnerType": "personal",
"enrolledDateTime": "2025-04-16T22:21:24Z",
"lastSyncDateTime": "2025-04-16T22:34:23Z",
"operatingSystem": "iOS",
**"complianceState": "compliant",**
**"jailBroken": "False",**
}


