# Ping Capture Analysis

Analysis of three ICMP echo-request/echo-reply captures: `localhost.pcapng`, `gateway.pcapng`, and `google.pcapng`.

## Gateway IP

- `gateway.pcapng` shows ICMP traffic with **source and destination both `192.168.43.71`** — the host's own address on its local (hotspot-style) network. Both request and reply frames carry this IP, with no other host involved.

## Response Times

| Target | IP | Packets | Avg RTT | Notes |
|---|---|---|---|---|
| Gateway | 192.168.43.71 | 4/4 replied | ~0.011 ms | Fastest — effectively instant, local interface |
| Localhost | 127.0.0.1 | 4/4 replied | ~0.013 ms | Near-identical to gateway, also local loopback |
| Google | 142.251.43.206 | 4/4 replied | ~22.8 ms | Slowest by far — real network round trip |

**Fastest:** the gateway (`192.168.43.71`), with localhost essentially tied — both are sub-millisecond since no traffic actually leaves the machine.

**Slowest:** Google (`142.251.43.206`, resolved via DNS for `google.com`), at roughly **22–24 ms** per round trip — consistent with an actual internet hop. No requests failed or timed out in any of the three captures; all four pings in each file received a reply.
