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
```
========================= RTP Streams ========================
    Src IP addr  Port    Dest IP addr  Port       SSRC          Payload  Pkts         Lost   Max Delta(ms)  Max Jitter(ms) Mean Jitter(ms) Problems?
   192.168.65.77 28100  192.168.88.254 10000 0x8B551BEE ITU-T G.711 PCMU  1803     0 (0.0%)          140.05            0.16            0.04
 192.168.88.254 10000    192.168.65.77 28100 0x30EFD930 ITU-T G.711 PCMU  2566     0 (0.0%)           20.38            0.15            0.09
   192.168.65.77 22720  192.168.88.254 10000 0x6CFC3B43 ITU-T G.711 PCMU  3413     0 (0.0%)          140.16            4.22            0.06
 192.168.88.254 10000    192.168.65.77 22720 0x275216CC ITU-T G.711 PCMU  4873     0 (0.0%)           40.32            7.16            0.80
   192.168.65.77 17488  192.168.88.254 10000 0x8B419DD4 ITU-T G.711 PCMU  3899     0 (0.0%)          161.45            8.79            0.46
 192.168.88.254 10000    192.168.65.77 17488 0x1E4B9466 ITU-T G.711 PCMU  5944     0 (0.0%)           20.48            0.15            0.10
   192.168.65.77 19192  192.168.88.254 10000 0x6CDC6B2C ITU-T G.711 PCMU  1330     0 (0.0%)          140.17            0.24            0.08
 192.168.88.254 10000    192.168.65.77 19192 0x5DBB1944 ITU-T G.711 PCMU  1535     0 (0.0%)           20.38            0.13            0.09
   192.168.65.77 30198  192.168.88.254 10000 0x6CDB2223 ITU-T G.711 PCMU   218     0 (0.0%)          139.92            0.25            0.10
 192.168.88.254 10000    192.168.65.77 30198 0x052AD7E6 ITU-T G.711 PCMU   323     0 (0.0%)           40.01            3.51            0.95
   192.168.65.77 31722  192.168.88.254 10000 0x7F243C54 ITU-T G.711 PCMU 13886     0 (0.0%)          140.21     33603952.15        38662.83 X
==============================================================
```
