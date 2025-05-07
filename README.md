# intunemapscore

A Cloudflare Worker that consumes Cloudflare Access Unique client ID Device Posture log events

Then :

1. creates/updates a map of Cloudflare [DeviceID : Intune deviceid] stored in KV
2. requests compliance.State from Graph API for a device id
3. converts compliance.State to s2s_score
4. creates/updates a map of Cloudflare [DeviceID : s2s_score] stored in KV
