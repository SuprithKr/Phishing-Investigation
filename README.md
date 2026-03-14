# Phishing Email Investigation

SOC investigation analyzing a real phishing email impersonating 
Bradesco bank (Brazil) using email header analysis and 
domain reputation checks.

## Email Summary

| Field | Value |
|---|---|
| From | BANCO DO BRADESCO LIVELO <banco.bradesco@atendimento.com.br> |
| Subject | CLIENTE PRIME - BRADESCO LIVELO: Seu cartão tem 92.990 pontos LIVELO expirando hoje! |
| Date | Tue, 19 Sep 2023 18:35:49 UTC |
| Sender IP | 137.184.34.4 |
| Sender Hostname | ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 (DigitalOcean VPS) |

## Tools Used

- **MXToolbox** — Email header analysis
- **VirusTotal** — Domain reputation check
- **URLScan.io** — URL and landing page analysis

## Authentication Results

| Check | Result | Meaning |
|---|---|---|
| SPF | FAIL | Sender not authorized |
| DKIM | FAIL | Email not signed |
| DMARC | FAIL | No policy found |

## Key IOCs

| Type | Value |
|---|---|
| Sender IP | 137.184.34.4 |
| Fake domain | atendimento.com.br |
| Phishing URL | https://blog1seguimentmydomaine2bra.me/ |
| Phishing path | /lander |
| Registrar | ENOM INC |
| Target | Bradesco bank customers (Brazil) |

## Attack Technique
```
STEP 1 — Urgency trigger
Email claims 92,990 loyalty points expire TODAY
↓
STEP 2 — Fake sender
From: banco.bradesco@atendimento.com.br
Real bank domain: bradesco.com.br
↓
STEP 3 — Malicious link
Button "Resgatar Agora" (Redeem Now)
Links to: blog1seguimentmydomaine2bra.me/lander
↓
STEP 4 — Credential harvest
Victim enters banking credentials on fake page
```

## Investigation Status

✅ Email headers analyzed
✅ SPF/DKIM/DMARC checked
✅ Sender IP identified
✅ Phishing domain extracted
✅ Domain reputation checked
✅ IOCs extracted
✅ Incident report completed
