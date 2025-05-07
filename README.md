# intunemapscore

A Cloudflare Worker that consumes Cloudflare Access Unique client ID Device Posture log events
creates/updates a map of Cloudflare [DeviceID : Intune deviceid] stores in KV
requests compliance.State from Graph API for a device id
converts compliance.State to s2s_score
creates/updates a map of Cloudflare [DeviceID : s2s_score] stores in KV
