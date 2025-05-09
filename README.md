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

1. creates/updates a map of Cloudflare [DeviceID : Intune deviceid] stored in KV/D1
2. requests compliance.State from Graph API for a deviceid
3. converts compliance.State to s2s_score
4. creates/updates a map of Cloudflare [DeviceID : s2s_score] stored in KV/D1

The Device UUID check does not have to pass or be applied to a traffic policy

The Custom Service provider check will be applied to polices

Pieces to make this work :

1. create Unique client ID list
2. create Unique client ID posture check for iOS
3. create kv for cfdeviceid-ituuid
4. create kv for cfdeviceid-itscore
5. create logger worker to receive posture log events
6. create logpush filtered to posture check created in step 2, destination is logger worker, included fields should be DeviceID, PostureReceivedJSON
7. create custom s2 access app
8. create custom s2s_worker
9. create custom s2s posture check , destination is custom s2s access app
10. create custom s2s posture check scoring threshold
11. apply custom s2s posture check to gateway policy




