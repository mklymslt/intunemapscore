# intunemapscore

1. A Cloudflare Worker that consumes Cloudflare Access Unique client ID Device Posture log events
2. creates/updates a map of Cloudflare [DeviceID : Intune deviceid] stores in KV
2. requests compliance.State from Graph API for a device id
4. converts compliance.State to s2s_score
5. creates/updates a map of Cloudflare [DeviceID : s2s_score] stores in KV
