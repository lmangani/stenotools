# stenotools
Dummy Stenographer scripts


### Match SDP ports from SIP
```
PORTS=$(sudo stenoraw 'port 5060, after 30m ago' | tshark -r /dev/stdin -T fields -e sip.msg_hdr | grep -i "m=audio" | awk '{print "port " $2 ", "}')
```

#### Pipe to tshark heuristics
```
stenoraw "$PORTS after 30m ago" | tshark  -q -r /dev/stdin -o rtp.heuristic_rtp:TRUE -z rtp,streams
```
