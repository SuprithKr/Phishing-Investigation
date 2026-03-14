# Email Header Analysis

## Raw Header Key Fields

| Field | Value |
|---|---|
| From | BANCO DO BRADESCO LIVELO <banco.bradesco@atendimento.com.br> |
| Return-Path | root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| Sender IP | 137.184.34.4 |
| Hostname | ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| Date | Tue, 19 Sep 2023 18:35:49 UTC |
| Message-ID | 20230919183549.39DEA3F725@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |

## Authentication Results

### SPF — FAIL
```
spf=temperror (sender IP is 137.184.34.4)
smtp.mailfrom=ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06
```
No nameservers found for sender domain.
Legitimate banks always have SPF configured.

### DKIM — FAIL
```
dkim=none (message not signed)
header.d=none
```
No DKIM signature present.
Legitimate banks always sign emails with DKIM.

### DMARC — FAIL
```
dmarc=temperror action=none
header.from=atendimento.com.br
compauth=fail reason=001
```
No DMARC record found for atendimento.com.br.

## Suspicious Header Indicators

### 1 — Sender IP is a DigitalOcean VPS
```
Sender IP: 137.184.34.4
Hostname:  ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06
Location:  San Francisco (sfo3)
Provider:  DigitalOcean
```
Legitimate banks send from corporate mail servers.
A DigitalOcean VPS named after its instance type
is a classic attacker-controlled server.

### 2 — Domain mismatch
```
Claimed identity: Banco do Bradesco
From domain:      atendimento.com.br
Real domain:      bradesco.com.br
```
The sender domain does not match the claimed identity.

### 3 — Return-Path reveals true origin
```
Return-Path: root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06
```
Return-Path shows the email was sent as root
from a Linux VPS — not a bank mail server.

### 4 — Microsoft spam score
```
X-Microsoft-Antispam: BCL:9
X-MS-Exchange-Organization-SCL: 5
```
Microsoft assigned a high bulk complaint level (BCL:9)
and spam confidence level (SCL:5) to this email.

## Verdict
PHISHING — All authentication checks failed.
Sent from attacker-controlled VPS.
Domain spoofing legitimate bank identity.
