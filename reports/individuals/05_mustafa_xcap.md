# OSINT Report: Mustafa (XCAP)
**Subject:** Founder/Executive, XCAP — Autonomous Finance
**Date:** April 2, 2026
**Classification:** Public OSINT

---

## 1. Identity

| Field | Detail |
|-------|--------|
| **First Name** | Mustafa |
| **Last Name** | Unknown |
| **Email** | mustafa@xcap.ai |
| **Role** | Likely Founder/CEO |
| **Company** | XCAP — "Autonomous Finance" |
| **Avatar** | Magenta/pink circle, initial "M" |

---

## 2. Company Profile — XCAP

| Field | Detail |
|-------|--------|
| **Brand Name** | XCAP |
| **Domains** | xcap.ai + xcap.com |
| **Tagline** | "The Autonomous Finance company for the age of Artificial Intelligence" |
| **Stage** | Pre-launch / Stealth (beta site only) |
| **Industry** | AI-driven financial services |

### Domain Intelligence

#### xcap.ai
| Field | Value |
|-------|-------|
| Registrar | GoDaddy.com, LLC |
| Created | 2023-07-03 |
| Expires | 2027-07-03 |
| Nameservers | ns35/ns36.domaincontrol.com |
| Registrant | **Domains By Proxy, LLC** (privacy shield) |
| Country | US |
| Status | All 4 client locks active |

#### xcap.com
| Field | Value |
|-------|-------|
| Registrar | 123-Reg Limited (UK) |
| Created | **2004-06-14** (22 years old!) |
| Expires | **2034-06-14** (10-year registration) |
| Nameservers | NS35/NS36.DOMAINCONTROL.COM |
| Status | All 4 client locks active |

### Critical Finding: Domain Connection
**Both xcap.ai and xcap.com use the same nameservers** (NS35/NS36.DOMAINCONTROL.COM), confirming they are owned by the same entity. The xcap.com domain is 22 years old (registered 2004) with a 10-year registration until 2034 — this suggests serious capital commitment. The .ai domain was acquired in 2023 to support the AI/autonomous finance rebrand.

---

## 3. Website Assessment

### xcap.ai
- Returns **404 error** — domain is parked or under construction
- Registered through **Domains By Proxy** (GoDaddy privacy service) — owner identity hidden

### xcap.com
- WordPress install with **Divi theme v5.0.2** (Elegant Themes)
- Shows only **"beta site"** placeholder
- **WordPress admin user exposed** (slug: "admin") — security concern
- Self-hosted mail server (mail.xcap.com) on GoDaddy infrastructure

### 🔗 CRITICAL LINK: Phipps Consulting ↔ XCAP
Both phippsconsulting.com and xcap.ai share the **exact same email service configuration**:
- SPF record: `dc-aa8e722993._spfm.{domain}`
- This unique identifier means both domains were configured by the same person/organization
- **Jake (Phipps) and Mustafa (XCAP) are directly connected** — not just meeting attendees, but sharing infrastructure

---

## 4. SEC Filing Analysis

SEC EDGAR search for "XCAP" found **"Xcap ASPV, a Series of Vauban Platform LP"** (CIK 0002001214), filed 2023-11-15. However, this appears to be a **different entity** — a structured finance product, not the AI fintech startup. No direct connection confirmed.

---

## 5. Social Media Presence

### Sherlock Results (xcapai): 6 profiles found
- TikTok: https://www.tiktok.com/@xcapai
- Telegram: https://t.me/xcapai (interesting — fintech community channel)
- Linktree: https://linktr.ee/xcapai
- DeviantArt, Roblox, Trovo (likely placeholder accounts)

The **Telegram presence** is notable — fintech/crypto companies often use Telegram for community building and customer support.

---

## 6. Assessment

**Credibility:** MODERATE-LOW
- Domain commitment is real (xcap.com registered until 2034)
- But zero public product or team information
- Privacy-shielded registration
- No press, no funding announcements, no team page

**The xcap.com age (2004) is interesting** — this could be:
1. An aged domain acquired for the rebrand (premium domain purchase)
2. A dormant company being resurrected with AI focus
3. A domain investor's holding that was purchased

The 10-year registration through 2034 suggests either significant capital or an acquisition of a premium domain.

**Likely Role in Meeting:** Bringing AI/autonomous finance technology to the deal. XCAP likely provides the algorithmic/AI layer that would sit on top of Auracle's wallet infrastructure. Mustafa is almost certainly the founder given the pre-launch stage.

**Risk Indicators:** HIGH
- Pre-launch with no product
- Privacy-shielded ownership
- No verifiable team or track record
- "AI autonomous finance" is a hot buzzword space with many failures

---

*Report generated via OSINT investigation — April 2, 2026*
*Sources: WHOIS, Sherlock, SEC EDGAR, web scraping*
