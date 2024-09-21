# SIP Protocal 


| ClientA | Msg          | FreeSwitch   | Msg          | ClientB |
|---------|--------------|--------------|--------------|---------|
|         | -Invite->    |              |              |         |
|         |              |              | -Invite->    |         |
|         | <-100Trying- |              |              |         |
|         |              |              | <-180 Ring-  |         |
|         | <-180 Ring-  |              |              |         |
|         |              |              | <-200 OK-    |         |
|         | <-200 OK-    |              |              |         |
|         |              |              |              |         |
|         | -ACK->       | -ACK->       | -ACK->       |         |
|         | <-RTP/RTCP-> | <-RTP/RTCP-> | <-RTP/RTCP-> |         |
|         |              |              |              |         |
|         | -BYE->       | -BYE->       | -BYE->       |         |
|         | <-200 OK-    | <-200 OK-    | <-200 OK-    |         |
## 1. INVITE　请求

```SIP
INVITE sip:1009@192.168.31.109:5060;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---78626c9dcaefb665;rport
Max-Forwards: 70
Contact: <sip:1002@192.168.31.142:55747;transport=UDP>
To: <sip:1009@192.168.31.109:5060>
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 1 INVITE
Allow: INVITE, ACK, CANCEL, BYE, NOTIFY, REFER, MESSAGE, OPTIONS, INFO, SUBSCRIBE
Content-Type: application/sdp
Supported: replaces, norefersub, extended-refer, timer, sec-agree, outbound, path, X-cisco-serviceuri
User-Agent: Zoiper v2.10.20.4_1
Allow-Events: presence, kpml, talk, as-feature-event
Content-Length: 264

v=0
o=Z 0 119481653 IN IP4 192.168.31.142
s=Z
c=IN IP4 192.168.31.142
t=0 0
m=audio 62715 RTP/AVP 3 101 110 97 8 0
a=rtpmap:101 telephone-event/8000
a=fmtp:101 0-16
a=rtpmap:110 speex/8000
a=rtpmap:97 iLBC/8000
a=fmtp:97 mode=20
a=sendrecv
a=rtcp-mux

```

## 2. INVITE回复
```SIP
SIP/2.0 407 Proxy Authentication Required
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---78626c9dcaefb665;rport=55747
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
To: <sip:1009@192.168.31.109:5060>;tag=3pDX04j1XvXam
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 1 INVITE
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Accept: application/sdp
Allow: INVITE, ACK, BYE, CANCEL, OPTIONS, MESSAGE, INFO, UPDATE, REGISTER, REFER, NOTIFY, PUBLISH, SUBSCRIBE
Supported: timer, path, replaces
Allow-Events: talk, hold, conference, presence, as-feature-event, dialog, line-seize, call-info, sla, include-session-description, presence.winfo, message-summary, refer
Proxy-Authenticate: Digest realm="192.168.31.109", nonce="5f046960-2eb0-484f-bf16-758576387c3f", algorithm=MD5, qop="auth"
Content-Length: 0

```

## 3. ACK消息
```SIP
ACK sip:1009@192.168.31.109:5060;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---78626c9dcaefb665;rport
Max-Forwards: 70
To: <sip:1009@192.168.31.109:5060>;tag=3pDX04j1XvXam
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 1 ACK
Content-Length: 0
```

## 4. INVITE 请求
```SIP
INVITE sip:1009@192.168.31.109:5060;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---974f0e190ebbfd0d;rport
Max-Forwards: 70
Contact: <sip:1002@192.168.31.142:55747;transport=UDP>
To: <sip:1009@192.168.31.109:5060>
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 2 INVITE
Allow: INVITE, ACK, CANCEL, BYE, NOTIFY, REFER, MESSAGE, OPTIONS, INFO, SUBSCRIBE
Content-Type: application/sdp
Proxy-Authorization: Digest username="1002",realm="192.168.31.109",nonce="5f046960-2eb0-484f-bf16-758576387c3f",uri="sip:1009@192.168.31.109:5060;transport=UDP",response="8bece954ef65ba0456abe71cf1243c6c",cnonce="5362af04830c3186db2b7bda9bb5585d",nc=00000001,qop=auth,algorithm=MD5
Supported: replaces, norefersub, extended-refer, timer, sec-agree, outbound, path, X-cisco-serviceuri
User-Agent: Zoiper v2.10.20.4_1
Allow-Events: presence, kpml, talk, as-feature-event
Content-Length: 264

v=0
o=Z 0 119481653 IN IP4 192.168.31.142
s=Z
c=IN IP4 192.168.31.142
t=0 0
m=audio 62715 RTP/AVP 3 101 110 97 8 0
a=rtpmap:101 telephone-event/8000
a=fmtp:101 0-16
a=rtpmap:110 speex/8000
a=rtpmap:97 iLBC/8000
a=fmtp:97 mode=20
a=sendrecv
a=rtcp-mux
```

## 5. Trying
```SIP
SIP/2.0 100 Trying
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---974f0e190ebbfd0d;rport=55747
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
To: <sip:1009@192.168.31.109:5060>
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 2 INVITE
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Content-Length: 0
```

## 6. INVITE 
```SIP
INVITE sip:1009@192.168.31.109:60119;ob SIP/2.0
Via: SIP/2.0/UDP 192.168.31.109;rport;branch=z9hG4bKmSymF8rmr1cvm
Max-Forwards: 69
From: "Extension 1002" <sip:1002@192.168.31.109>;tag=58Ze4tm8QeagB
To: <sip:1009@192.168.31.109:60119;ob>
Call-ID: 81a36a1e-f284-123d-5799-f111227aced7
CSeq: 88896036 INVITE
Contact: <sip:mod_sofia@192.168.31.109:5060>
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Allow: INVITE, ACK, BYE, CANCEL, OPTIONS, MESSAGE, INFO, UPDATE, REGISTER, REFER, NOTIFY, PUBLISH, SUBSCRIBE
Supported: timer, path, replaces
Allow-Events: talk, hold, conference, presence, as-feature-event, dialog, line-seize, call-info, sla, include-session-description, presence.winfo, message-summary, refer
Content-Type: application/sdp
Content-Disposition: session
Content-Length: 248
X-FS-Support: update_display,send_info
Remote-Party-ID: "Extension 1002" <sip:1002@192.168.31.109>;party=calling;screen=yes;privacy=off

v=0
o=FreeSWITCH 1726882621 1726882622 IN IP4 192.168.31.109
s=FreeSWITCH
c=IN IP4 192.168.31.109
t=0 0
m=audio 17036 RTP/AVP 8 0 101
a=rtpmap:8 PCMA/8000
a=rtpmap:0 PCMU/8000
a=rtpmap:101 telephone-event/8000
a=fmtp:101 0-15
a=ptime:20
```


## 7. TRYING
```SIP
SIP/2.0 100 Trying
Via: SIP/2.0/UDP 192.168.31.109;rport=5060;received=192.168.31.109;branch=z9hG4bKmSymF8rmr1cvm
Call-ID: 81a36a1e-f284-123d-5799-f111227aced7
From: "Extension 1002" <sip:1002@192.168.31.109>;tag=58Ze4tm8QeagB
To: <sip:1009@192.168.31.109;ob>
CSeq: 88896036 INVITE
Content-Length:  0
```

## 8. RING
```SIP
SIP/2.0 180 Ringing
Via: SIP/2.0/UDP 192.168.31.109;rport=5060;received=192.168.31.109;branch=z9hG4bKmSymF8rmr1cvm
Call-ID: 81a36a1e-f284-123d-5799-f111227aced7
From: "Extension 1002" <sip:1002@192.168.31.109>;tag=58Ze4tm8QeagB
To: <sip:1009@192.168.31.109;ob>;tag=d4e3674ca23d4b22bebd2e39245254d5
CSeq: 88896036 INVITE
Contact: "1009" <sip:1009@192.168.31.109:60119;ob>
Allow: PRACK, INVITE, ACK, BYE, CANCEL, UPDATE, INFO, SUBSCRIBE, NOTIFY, REFER, MESSAGE, OPTIONS
Content-Length:  0
```

## 9. Session 
```SIP
SIP/2.0 183 Session Progress
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---974f0e190ebbfd0d;rport=55747
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
To: <sip:1009@192.168.31.109:5060>;tag=4Z6N2Z34t5KXF
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 2 INVITE
Contact: <sip:1009@192.168.31.109:5060;transport=udp>
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Accept: application/sdp
Allow: INVITE, ACK, BYE, CANCEL, OPTIONS, MESSAGE, INFO, UPDATE, REGISTER, REFER, NOTIFY, PUBLISH, SUBSCRIBE
Supported: timer, path, replaces
Allow-Events: talk, hold, conference, presence, as-feature-event, dialog, line-seize, call-info, sla, include-session-description, presence.winfo, message-summary, refer
Content-Type: application/sdp
Content-Disposition: session
Content-Length: 272
Remote-Party-ID: "1009" <sip:1009@192.168.31.109>;party=calling;privacy=off;screen=no

v=0
o=FreeSWITCH 1726881924 1726881925 IN IP4 192.168.31.109
s=FreeSWITCH
c=IN IP4 192.168.31.109
t=0 0
m=audio 17734 RTP/AVP 8 101
a=rtpmap:8 PCMA/8000
a=rtpmap:101 telephone-event/8000
a=fmtp:101 0-15
a=ptime:20
a=rtcp-mux
a=rtcp:17734 IN IP4 192.168.31.109
```

## 10. 200 OK
```SIP
SIP/2.0 200 OK
Via: SIP/2.0/UDP 192.168.31.109;rport=5060;received=192.168.31.109;branch=z9hG4bKmSymF8rmr1cvm
Call-ID: 81a36a1e-f284-123d-5799-f111227aced7
From: "Extension 1002" <sip:1002@192.168.31.109>;tag=58Ze4tm8QeagB
To: <sip:1009@192.168.31.109;ob>;tag=d4e3674ca23d4b22bebd2e39245254d5
CSeq: 88896036 INVITE
Allow: PRACK, INVITE, ACK, BYE, CANCEL, UPDATE, INFO, SUBSCRIBE, NOTIFY, REFER, MESSAGE, OPTIONS
Contact: "1009" <sip:1009@192.168.31.109:60119;ob>
Supported: replaces, 100rel, timer, norefersub
Content-Type: application/sdp
Content-Length:   321

v=0
o=- 3935917257 3935917258 IN IP4 192.168.31.109
s=pjmedia
b=AS:84
t=0 0
a=X-nat:0
m=audio 4008 RTP/AVP 8 101
c=IN IP4 192.168.31.109
b=TIAS:64000
a=rtcp:4009 IN IP4 192.168.31.109
a=sendrecv
a=rtpmap:8 PCMA/8000
a=rtpmap:101 telephone-event/8000
a=fmtp:101 0-16
a=ssrc:824332886 cname:5e9025ae5704649f
```

## 11. ACK
```SIP
ACK sip:1009@192.168.31.109:60119;ob SIP/2.0
Via: SIP/2.0/UDP 192.168.31.109;rport;branch=z9hG4bKN2QDH39QNa3eg
Max-Forwards: 70
From: "Extension 1002" <sip:1002@192.168.31.109>;tag=58Ze4tm8QeagB
To: <sip:1009@192.168.31.109:60119;ob>;tag=d4e3674ca23d4b22bebd2e39245254d5
Call-ID: 81a36a1e-f284-123d-5799-f111227aced7
CSeq: 88896036 ACK
Contact: <sip:mod_sofia@192.168.31.109:5060>
Content-Length: 0
```

## 12. 200 OK
```SIP
SIP/2.0 200 OK
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---974f0e190ebbfd0d;rport=55747
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
To: <sip:1009@192.168.31.109:5060>;tag=4Z6N2Z34t5KXF
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 2 INVITE
Contact: <sip:1009@192.168.31.109:5060;transport=udp>
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Allow: INVITE, ACK, BYE, CANCEL, OPTIONS, MESSAGE, INFO, UPDATE, REGISTER, REFER, NOTIFY, PUBLISH, SUBSCRIBE
Supported: timer, path, replaces
Allow-Events: talk, hold, conference, presence, as-feature-event, dialog, line-seize, call-info, sla, include-session-description, presence.winfo, message-summary, refer
Content-Type: application/sdp
Content-Disposition: session
Content-Length: 272
Remote-Party-ID: "Outbound Call" <sip:1009@192.168.31.109>;party=calling;privacy=off;screen=no

v=0
o=FreeSWITCH 1726881924 1726881925 IN IP4 192.168.31.109
s=FreeSWITCH
c=IN IP4 192.168.31.109
t=0 0
m=audio 17734 RTP/AVP 8 101
a=rtpmap:8 PCMA/8000
a=rtpmap:101 telephone-event/8000
a=fmtp:101 0-15
a=ptime:20
a=rtcp-mux
a=rtcp:17734 IN IP4 192.168.31.109
```


## 13. ACK
```SIP
ACK sip:1009@192.168.31.109:5060;transport=udp SIP/2.0
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---b84e335815c6f6a9;rport
Max-Forwards: 70
Contact: <sip:1002@192.168.31.142:55747;transport=UDP>
To: <sip:1009@192.168.31.109:5060>;tag=4Z6N2Z34t5KXF
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 2 ACK
User-Agent: Zoiper v2.10.20.4_1
Content-Length: 0
```


## 14. REGISTER
```SIP
REGISTER sip:192.168.31.109:5060;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---86aa6dd38424cee1;rport
Max-Forwards: 70
Contact: <sip:1002@192.168.31.142:55747;rinstance=59defe5c8b2788ae;transport=UDP>
To: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=88741f1c
Call-ID: gzK0vdfGjqqhSuekwhNwmg..
CSeq: 3 REGISTER
Expires: 60
Allow: INVITE, ACK, CANCEL, BYE, NOTIFY, REFER, MESSAGE, OPTIONS, INFO, SUBSCRIBE
Supported: replaces, norefersub, extended-refer, timer, sec-agree, outbound, path, X-cisco-serviceuri
User-Agent: Zoiper v2.10.20.4_1
Authorization: Digest username="1002",realm="192.168.31.109",nonce="fffe2121-d01f-4c89-ab62-12a030a1c10d",uri="sip:192.168.31.109:5060;transport=UDP",response="b4418b2b96e05ec2a0beb3c522edbcc9",cnonce="b3468b9ac6827d7c51e85ef96618190f",nc=00000002,qop=auth,algorithm=MD5
Allow-Events: presence, kpml, talk, as-feature-event
Content-Length: 0
```

## 15. 200 OK
```SIP
SIP/2.0 200 OK
Via: SIP/2.0/UDP 192.168.31.142:55747;branch=z9hG4bK-524287-1---86aa6dd38424cee1;rport=55747
From: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=88741f1c
To: "1002" <sip:1002@192.168.31.109:5060;transport=UDP>;tag=6HS75N5BNQ02p
Call-ID: gzK0vdfGjqqhSuekwhNwmg..
CSeq: 3 REGISTER
Contact: <sip:1002@192.168.31.142:55747;rinstance=59defe5c8b2788ae;transport=UDP>;expires=60
Date: Sat, 21 Sep 2024 06:21:03 GMT
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Allow: INVITE, ACK, BYE, CANCEL, OPTIONS, MESSAGE, INFO, UPDATE, REGISTER, REFER, NOTIFY, PUBLISH, SUBSCRIBE
Supported: timer, path, replaces
Content-Length: 0
```

## 16. BYE
```SIP
BYE sip:mod_sofia@192.168.31.109:5060 SIP/2.0
Via: SIP/2.0/UDP 192.168.31.109:60119;rport;branch=z9hG4bKPjf3b1d22a5602462d8ca11d6db5fad320
Max-Forwards: 70
From: <sip:1009@192.168.31.109;ob>;tag=d4e3674ca23d4b22bebd2e39245254d5
To: "Extension 1002" <sip:1002@192.168.31.109>;tag=58Ze4tm8QeagB
Call-ID: 81a36a1e-f284-123d-5799-f111227aced7
CSeq: 30422 BYE
User-Agent: MicroSIP/3.21.4
Content-Length:  0
```

## 17. 200 OK
```SIP
SIP/2.0 200 OK
Via: SIP/2.0/UDP 192.168.31.109:60119;rport=60119;branch=z9hG4bKPjf3b1d22a5602462d8ca11d6db5fad320
From: <sip:1009@192.168.31.109;ob>;tag=d4e3674ca23d4b22bebd2e39245254d5
To: "Extension 1002" <sip:1002@192.168.31.109>;tag=58Ze4tm8QeagB
Call-ID: 81a36a1e-f284-123d-5799-f111227aced7
CSeq: 30422 BYE
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Allow: INVITE, ACK, BYE, CANCEL, OPTIONS, MESSAGE, INFO, UPDATE, REGISTER, REFER, NOTIFY, PUBLISH, SUBSCRIBE
Supported: timer, path, replaces
Content-Length: 0
```

## 18. BYE
```SIP
BYE sip:1002@192.168.31.142:55747;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 192.168.31.109;rport;branch=z9hG4bKpBH6jytUjKS1B
Max-Forwards: 70
From: <sip:1009@192.168.31.109:5060>;tag=4Z6N2Z34t5KXF
To: "1002" <sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 88896041 BYE
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Allow: INVITE, ACK, BYE, CANCEL, OPTIONS, MESSAGE, INFO, UPDATE, REGISTER, REFER, NOTIFY, PUBLISH, SUBSCRIBE
Supported: timer, path, replaces
Reason: Q.850;cause=16;text="NORMAL_CLEARING"
Content-Length: 0
```

## 19. BYE
```SIP
BYE sip:1002@192.168.31.142:55747;transport=UDP SIP/2.0
Via: SIP/2.0/UDP 192.168.31.109;rport;branch=z9hG4bKpBH6jytUjKS1B
Max-Forwards: 70
From: <sip:1009@192.168.31.109:5060>;tag=4Z6N2Z34t5KXF
To: "1002" <sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 88896041 BYE
User-Agent: FreeSWITCH-mod_sofia/1.10.12-release~a88d069d6f~64bit
Allow: INVITE, ACK, BYE, CANCEL, OPTIONS, MESSAGE, INFO, UPDATE, REGISTER, REFER, NOTIFY, PUBLISH, SUBSCRIBE
Supported: timer, path, replaces
Reason: Q.850;cause=16;text="NORMAL_CLEARING"
Content-Length: 0

```
## 20. SIP 200 OK
```SIP
SIP/2.0 200 OK
Via: SIP/2.0/UDP 192.168.31.109;rport=5060;branch=z9hG4bKpBH6jytUjKS1B
Contact: <sip:1002@192.168.31.142:55747;transport=UDP>
To: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
From: <sip:1009@192.168.31.109:5060>;tag=4Z6N2Z34t5KXF
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 88896041 BYE
User-Agent: Zoiper v2.10.20.4_1
Content-Length: 0

```
## 21. SIP 200 OK
```SIP
SIP/2.0 200 OK
Via: SIP/2.0/UDP 192.168.31.109;rport=5060;branch=z9hG4bKpBH6jytUjKS1B
Contact: <sip:1002@192.168.31.142:55747;transport=UDP>
To: "1002"<sip:1002@192.168.31.109:5060;transport=UDP>;tag=0e837329
From: <sip:1009@192.168.31.109:5060>;tag=4Z6N2Z34t5KXF
Call-ID: cqBcUqknj-sTLjz_cI-GKw..
CSeq: 88896041 BYE
User-Agent: Zoiper v2.10.20.4_1
Content-Length: 0
```