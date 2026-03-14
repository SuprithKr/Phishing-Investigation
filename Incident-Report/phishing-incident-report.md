# Incident Report — Phishing Email
**Date:** 2023-09-19
**Analyst:** Suprith Kr
**Severity:** High
**Status:** Analyzed

---

## 1. Executive Summary

A phishing email impersonating Bradesco bank (Brazil) was analyzed.
The email used urgency tactics claiming loyalty points would expire
that day to trick victims into clicking a malicious link leading to
a credential harvesting page. All email authentication checks
(SPF, DKIM, DMARC) failed. The email was sent from an
attacker-controlled DigitalOcean VPS in San Francisco.

---

## 2. Email Details

| Field | Value |
|---|---|
| From | banco.bradesco@atendimento.com.br |
| Claimed Identity | Banco do Bradesco Livelo |
| Real Bank Domain | bradesco.com.br |
| Subject | Points expiring today — urgent |
| Language | Portuguese (Brazilian) |
| Target | Bradesco bank customers |
| Date | 19 Sep 2023 18:35 UTC |

---

## 3. Authentication Analysis

| Check | Result | Detail |
|---|---|---|
| SPF | FAIL | No nameservers for sender domain |
| DKIM | FAIL | No signature found |
| DMARC | FAIL | No DMARC record |

All three authentication mechanisms failed — confirming
this email is not from the legitimate Bradesco bank.

---

## 4. Sender Infrastructure

| Field | Value |
|---|---|
| Sender IP | 137.184.34.4 |
| Provider | DigitalOcean VPS |
| Location | San Francisco, USA |
| Hostname | ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| Return-Path | root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |

The email was sent from a cheap cloud VPS — standard
attacker infrastructure for phishing campaigns.

---

## 5. Phishing Technique

The attacker used three social engineering tactics:

1. **Urgency** — Points expire TODAY creates panic
2. **Brand impersonation** — Bradesco bank logo and branding
3. **Financial loss fear** — 92,990 points about to be lost

The email body contains a button labeled
"Resgatar Agora" (Redeem Now) linking to:
```
https://blog1seguimentmydomaine2bra.me/lander
```

This is a fake page designed to steal banking credentials.

---

## 6. Domain Analysis

| Field | Value |
|---|---|
| Phishing domain | blog1seguimentmydomaine2bra.me |
| Real domain | bradesco.com.br |
| Registrar | ENOM INC |
| Domain age | 2 years |
| VirusTotal | 0/94 clean |
| URLScan | 20 historical scans of /lander path |

The domain name attempts to mimic legitimacy by including
"bra" (Brazil abbreviation) but is completely unrelated
to Bradesco bank.

---

## 7. IOCs

| Type | Value |
|---|---|
| Sender IP | 137.184.34.4 |
| Phishing URL | https://blog1seguimentmydomaine2bra.me/ |
| Fake domain | atendimento.com.br |
| From address | banco.bradesco@atendimento.com.br |

---

## 8. SOC Response Steps

1. **Block sender IP** 137.184.34.4 at email gateway
2. **Block domain** blog1seguimentmydomaine2bra.me at firewall
3. **Block domain** atendimento.com.br at email gateway
4. **Search email logs** for other recipients of this campaign
5. **Alert users** who received this email
6. **Check proxy logs** for any clicks on the phishing URL
7. **Reset credentials** for any users who clicked the link

---

## 9. Conclusion

This phishing email used classic social engineering tactics —
urgency, brand impersonation, and financial fear — to trick
Brazilian bank customers into visiting a credential harvesting
page. The attack was easily identified through header analysis
showing failed SPF, DKIM, and DMARC checks, and a sender IP
tracing back to an attacker-controlled VPS rather than
legitimate bank infrastructure.
