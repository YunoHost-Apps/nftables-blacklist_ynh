The `__APP__` service makes sure the block lists survive server restart while `__APP__-update` fetches the updated blocklists daily.

Note that stopping either of the services **does not** disable blocking, you need to actually stop the `__APP__` service and manuall drop the `blacklist` table via `nft delete table inet blacklist`. It'll be recreated when the service starts up again.

Due to upstream limitations it is impossible to run this app with no blocked IPs, hence `203.0.113.1` was elected as default-blocked. It's reserved by [rfc5737](https://datatracker.ietf.org/doc/html/rfc5737#section-3) for documentation purposes, no one should be using it anyways.