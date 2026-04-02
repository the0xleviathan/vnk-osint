# OSINT Process Playbook — Repeatable Investigation Methodology
**Version:** 1.0
**Created:** April 2, 2026
**Purpose:** Repeatable OSINT investigation workflow for meeting attendee background checks

---

## Overview

This playbook documents the end-to-end process for conducting OSINT investigations on individuals and organizations identified from meeting screenshots or attendee lists. Designed for repeatable deployment as a service.

---

## Phase 1: Preparation (15 min)

### 1.1 Environment Setup
```bash
# Create project structure
mkdir -p ~/osint-project/{tools,reports/{individuals,executive},docs,raw-data/{linkedin,domains,companies,social,sec,whois}}

# Install OSINT tools via ClawHub
clawhub install linkedin-api
clawhub install apollo-enrichment
clawhub install whois-toolkit
clawhub install whoislookup
clawhub install domain-checker
clawhub install market-research-agent
clawhub install olo-sec-scanner
clawhub install 51mee-background-check-list
clawhub install fact-cross-check

# Install system tools
pip3 install sherlock-project --break-system-packages

# Verify installation
sherlock --version
which agent-browser
```

### 1.2 Malware Verification
```bash
# Scan all installed skills
for skill in ~/.openclaw/workspace/skills/*/; do
  name=$(basename "$skill")
  issues=$(grep -ril "eval\|exec\|base64 -d\|subprocess\.call\|os\.system\|rm -rf\|curl.*|.*sh\|wget.*|.*sh\|nc -l\|reverse_shell\|/dev/tcp\|chmod 777\|mkfifo\|/bin/sh\|/bin/bash" "$skill" 2>/dev/null | grep -v "SKILL.md" | wc -l)
  if [ "$issues" -gt 0 ]; then
    echo "⚠️  $name: $issues suspicious patterns"
  else
    echo "✅ $name: Clean"
  fi
done
```

---

## Phase 2: Target Identification (10 min)

### 2.1 Screenshot Analysis
- Use image analysis tool to extract attendee names, emails, roles
- Document all visible information (names, domains, avatars, roles)

### 2.2 Target Matrix
Create a structured list:
```json
{
  "targets": [
    {"name": "...", "email": "...", "company": "...", "domain": "..."}
  ]
}
```

---

## Phase 3: Domain Intelligence (20 min)

### 3.1 WHOIS Deep Dive
```bash
cd ~/.openclaw/workspace/skills/whois-toolkit

# Batch WHOIS lookup
for domain in domain1.com domain2.ai domain3.io; do
  python3 scripts/whois_lookup.py $domain --json > ~/osint-project/raw-data/whois/$domain.json
done
```

### Key Data Points to Extract:
- Registrar, creation date, expiry date
- Nameserver relationships (shared NS = same owner)
- Privacy/proxy registration
- Domain lock status
- Days until expiry (flag if < 30)

### 3.2 DNS Analysis
```bash
# Check for shared infrastructure
for domain in domain1.com domain2.ai; do
  echo "=== $domain ==="
  dig +short NS $domain
  dig +short A $domain
  dig +short MX $domain
done
```

---

## Phase 4: Social Media Reconnaissance (30 min)

### 4.1 Sherlock Username Search
```bash
# Company usernames
sherlock companyname --print-found --timeout 8 --no-txt

# Personal usernames
sherlock firstname-lastname --print-found --timeout 8 --no-txt
sherlock firstnamelastname --print-found --timeout 8 --no-txt

# Variations
sherlock username1 username2 username3 --print-found --timeout 8 --no-txt
```

### 4.2 Platform-Specific Checks
- LinkedIn (via public profiles)
- Twitter/X (via web fetch)
- TikTok (via web fetch)
- Telegram (via web fetch)
- GitHub (via web fetch)

---

## Phase 5: Company Intelligence (30 min)

### 5.1 Company Research
- Company website (full scrape)
- About/Team pages
- Press/Blog pages
- Awards and accreditations

### 5.2 Regulatory Checks
```bash
# SEC EDGAR (US)
curl -s "https://efts.sec.gov/LATEST/search-index?q=%22Company+Name%22" \
  -H "User-Agent: OSINT/1.0 (contact@example.com)"

# SAM.gov (federal vendors)
# BBB (business bureau)
# State incorporation records
```

### 5.3 App Store Intelligence
- Apple App Store listings
- Google Play listings
- Download counts, reviews, developer info

---

## Phase 6: Contact Enrichment (15 min)

### 6.1 Apollo Enrichment (requires API key)
```bash
cd ~/.openclaw/workspace/skills/apollo-enrichment
export APOLLO_API_KEY=your_key

# Enrich person
python3 apollo.py enrich --email "person@company.com"

# Enrich company
python3 apollo.py enrich-company --domain "company.com"
```

### 6.2 LinkedIn API (requires MATON_API_KEY)
```bash
export MATON_API_KEY=your_key

# Get profile
curl -s "https://gateway.maton.ai/linkedin/rest/people/{id}" \
  -H "Authorization: Bearer $MATON_API_KEY" \
  -H "LinkedIn-Version: 202506"
```

---

## Phase 7: Analysis & Reporting (45 min)

### 7.1 Individual Report Template
Each report should include:
1. Identity (name, email, role, company)
2. Company profile (legal name, domain, industry, team)
3. Domain intelligence (WHOIS, DNS)
4. Social media presence
5. Regulatory/SEC filings
6. Credibility assessment (HIGH/MODERATE/LOW)
7. Role in meeting hypothesis
8. Risk indicators (LOW/MODERATE/HIGH)

### 7.2 Executive Summary
- Attendee summary matrix
- Organizational relationship map
- Deal hypothesis (most likely scenario + alternatives)
- Key intelligence highlights
- Risk flags
- Recommended due diligence
- Intelligence gaps

---

## Phase 8: Quality Assurance (15 min)

### 8.1 Cross-Verification
- Verify at least 2 independent sources per key claim
- Flag any conflicting information
- Document confidence levels

### 8.2 Final Review
- All individual reports complete
- Executive summary drafted
- Intelligence gaps documented
- Process documented

---

## Tool Reference

### Installed Tools
| Tool | Command | API Key Required |
|------|---------|-----------------|
| WHOIS Toolkit | `python3 scripts/whois_lookup.py domain.com` | No |
| Sherlock | `sherlock username` | No |
| Agent Browser | `agent-browser open url` | No |
| Apollo | `python3 apollo.py enrich --email` | Yes (APOLLO_API_KEY) |
| LinkedIn | curl to gateway.maton.ai | Yes (MATON_API_KEY) |
| SEC Scanner | curl to efts.sec.gov | No |

### Built-in Tools
- web_search (DuckDuckGo)
- web_fetch (direct page scraping)
- image analysis (screenshot interpretation)
- exec (curl, dig, whois, nslookup)

---

## Time Estimates

| Phase | Time | Cumulative |
|-------|------|------------|
| Preparation | 15 min | 15 min |
| Target ID | 10 min | 25 min |
| Domain Intel | 20 min | 45 min |
| Social Recon | 30 min | 75 min |
| Company Intel | 30 min | 105 min |
| Contact Enrichment | 15 min | 120 min |
| Analysis & Reporting | 45 min | 165 min |
| QA | 15 min | 180 min |
| **Total** | **~3 hours** | |

---

## Pricing Model Suggestions

| Scope | Deliverables | Suggested Price |
|-------|-------------|-----------------|
| **Basic** | WHOIS + Social + Company scrape | $500 |
| **Standard** | + Sherlock + SEC + Individual reports | $1,500 |
| **Premium** | + Apollo enrichment + Executive summary + Due diligence recs | $3,000 |
| **Enterprise** | + LinkedIn API + Deep dive + Ongoing monitoring | $5,000+ |

---

## Notes for Future Runs

1. **Rate limiting is real** — DuckDuckGo, Google, Bing all CAPTCHA after ~10 searches. Space queries or rotate IPs.
2. **API keys needed** — Apollo and LinkedIn API significantly improve data quality. Budget for paid tiers.
3. **Sherlock false positives** — Common names (Jason Singh) produce 60+ results, most irrelevant. Focus on unique names first.
4. **Domain privacy is common** — Domains By Proxy, Cloudflare hide registrant info. DNS correlation helps.
5. **Agent-browser** — Best for bypassing bot detection on search engines. Use sparingly to avoid blocks.

---

*Playbook v1.0 — April 2, 2026*
*Optimized for OpenClaw agent environment*
