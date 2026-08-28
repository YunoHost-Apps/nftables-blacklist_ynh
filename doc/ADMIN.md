The `__APP__` service makes sure the block lists survive server restart while `__APP__-update` fetches the updated blocklists daily.

Note that stopping either of the services **does not** disable blocking, you need to actually stop the `__APP__` service and manually drop the `blacklist` table via `nft delete table inet blacklist`. It'll be recreated when the service starts up again.

Due to upstream limitations it is impossible to run this app with no blocked IPs, hence `203.0.113.1` was elected as default-blocked. It's reserved by [rfc5737](https://datatracker.ietf.org/doc/html/rfc5737#section-3) for documentation purposes, no one should be using it anyways.

Blanked blocking the whole United States of America (`us`) will brick the app as both inbound and outbound traffic to Github will break.

From upstream docs:

```
# List the blacklist table
sudo nft list table inet blacklist

# Show IPv4 set contents
sudo nft list set inet blacklist blacklist4

# Show IPv6 set contents
sudo nft list set inet blacklist blacklist6

# Check drop counters
sudo nft list chain inet blacklist input

# Drop all the rules
sudo nft delete table inet blacklist
```