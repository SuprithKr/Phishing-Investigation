# Indicators of Compromise — Phishing Investigation

## Network IOCs

| Type | Value | Source |
|---|---|---|
| Sender IP | 137.184.34.4 | Email header |
| Phishing domain | blog1seguimentmydomaine2bra.me | Email body |
| Phishing URL | https://blog1seguimentmydomaine2bra.me/ | Email body |
| Phishing path | /lander | URLScan |
| Fake sender domain | atendimento.com.br | Email header |

## Email IOCs

| Type | Value |
|---|---|
| From address | banco.bradesco@atendimento.com.br |
| Return-Path | root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| Subject | CLIENTE PRIME - BRADESCO LIVELO: Seu cartão tem 92.990 pontos LIVELO expirando hoje! |
| Message-ID | 20230919183549.39DEA3F725@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |

## Infrastructure IOCs

| Type | Value |
|---|---|
| VPS Provider | DigitalOcean |
| VPS Location | San Francisco (sfo3) |
| Hostname | ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| Domain Registrar | ENOM INC |
| Domain Age | 2 years |

## Reputation Check Results

| Tool | Domain | Result |
|---|---|---|
| VirusTotal | blog1seguimentmydomaine2bra.me | 0/94 clean |
| URLScan | blog1seguimentmydomaine2bra.me | 20 scans, /lander path |
| MXToolbox | atendimento.com.br | SPF/DKIM/DMARC all fail |

## Detection Rules

Block these at email gateway:
```
Sender IP:     137.184.34.4
Domain:        atendimento.com.br
Domain:        blog1seguimentmydomaine2bra.me
URL pattern:   blog1seguimentmydomaine2bra.me/lander
```
