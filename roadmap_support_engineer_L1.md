# 🎧 Support Engineer L1 Learning Roadmap
### From Beginner to Advanced — A Structured, Industry-Aligned Path

> **How to use this roadmap:** Progress sequentially through each phase. Complete all exercises and mini-projects before advancing. Mega-projects cap each major stage and simulate real support scenarios. Estimated total time: **12–18 months** of consistent study and practice (8–12 hrs/week). This roadmap is designed for someone entering technical support at a SaaS, cloud, or infrastructure company.

---

## Table of Contents

1. [Phase 0 — Foundations](#phase-0--foundations-weeks-1-6)
2. [Phase 1 — Core Support Skills](#phase-1--core-support-skills-weeks-7-14)
3. [Phase 2 — Technical Depth](#phase-2--technical-depth-weeks-15-26)
4. [Phase 3 — Advanced Support Operations](#phase-3--advanced-support-operations-weeks-27-38)
5. [Phase 4 — Specialization Tracks](#phase-4--specialization-tracks-weeks-39-52)
6. [Phase 5 — Senior L1 & Growth](#phase-5--senior-l1--growth-weeks-53-65)
7. [Resources & Certifications](#resources--certifications)
8. [Tools & Environment Setup](#tools--environment-setup)

---

## Phase 0 — Foundations (Weeks 1–6)

> **Goal:** Build the baseline knowledge every Support Engineer needs before taking a single ticket — computing fundamentals, networking, operating systems, and professional communication.

### 0.1 Computing & Hardware Fundamentals

**Topics:**
- Computer architecture: CPU, RAM, storage, motherboard — what each does and how they interact
- Storage types: HDD vs. SSD vs. NVMe — performance and failure characteristics
- Operating system types: Windows, macOS, Linux — where each is used in enterprise
- Virtualization concepts: VMs, hypervisors, containers (what they are, not how to build them yet)
- Cloud computing basics: IaaS, PaaS, SaaS — understanding what your company's product fits into
- Binary, hexadecimal, and ASCII — why encoding matters in support

**Learning Materials:**
- *CompTIA IT Fundamentals (ITF+)* study guide — Mike Meyers (or free YouTube equivalents)
- Professor Messer's free CompTIA A+ Course (YouTube)
- Khan Academy: Computers and the Internet (free)
- HowStuffWorks.com: Computer section (free, conceptual)

**Exercises:**
1. Look up the specs of 3 different laptops (one budget, one mid-range, one enterprise). For each, predict what kinds of tasks it would struggle with and why — explain using specific hardware metrics
2. Download CPU-Z (Windows) or `system_profiler` (macOS) on your personal machine. Document every hardware component and write a plain-English explanation of what each one does
3. Draw a diagram of how a request from a browser travels to a web server and back — label every component including OS, NIC, router, DNS, and web server
4. Research 3 common hardware failure symptoms (e.g., blue screen, slow performance, no boot) and for each, list 3 possible causes and how you'd distinguish between them

**Mini-Project — Hardware Troubleshooting Runbook:**
Write a structured troubleshooting runbook for the following 5 scenarios a support engineer might encounter: (1) computer won't power on, (2) system extremely slow, (3) external display not detected, (4) USB device not recognized, (5) overheating and shutting down. Each entry must include: symptom, likely causes ranked by frequency, step-by-step diagnostic questions, and resolution paths. Format as a Markdown document.

---

### 0.2 Networking Fundamentals

**Topics:**
- The OSI model: all 7 layers — what happens at each, why support engineers care
- TCP/IP: IP addressing, subnets, DHCP, DNS, ARP
- Core protocols: HTTP/HTTPS, FTP, SSH, SMTP, IMAP/POP3
- Network hardware: routers, switches, firewalls, WAPs, load balancers
- Network troubleshooting tools: `ping`, `traceroute`/`tracert`, `nslookup`, `dig`, `netstat`, `curl`
- Wi-Fi vs. wired: interference, signal strength, common connectivity issues
- VPN concepts: what they do, split tunneling, common VPN issues

**Learning Materials:**
- Professor Messer's Network+ Course (free on YouTube)
- *CompTIA Network+ Study Guide* — Mike Chapple (Ch. 1–6)
- Cisco Networking Academy: Networking Basics (free)
- TryHackMe: "Pre-Security" → Networking Fundamentals (free)

**Exercises:**
1. Open a terminal and run `ping`, `traceroute` (`tracert` on Windows), `nslookup`, and `curl -I` against 5 different websites. Document and interpret every line of output — what does each hop in traceroute mean?
2. Draw a home or office network diagram: label every device, its IP address (use `ipconfig`/`ifconfig`), its role, and which OSI layer it primarily operates at
3. Use `nslookup` to find the MX, A, CNAME, and TXT records for 3 different company domains. Explain what each record type means and when a support engineer would care about it
4. Simulate 5 networking support scenarios in writing: a user can't access the internet, email isn't sending, VPN won't connect, a specific website is unreachable, slow file transfers. For each, write the first 5 diagnostic questions you'd ask

**Mini-Project — Network Troubleshooting Decision Tree:**
Build a visual troubleshooting decision tree for "User cannot connect to the internet." The tree must branch based on: device type, wired vs. wireless, whether other users are affected, whether the issue is all sites or one site, and VPN status. Each terminal node must specify a resolution action and an escalation condition. Deliver as a Markdown document with ASCII or Mermaid diagram.

---

### 0.3 Operating Systems in Depth

**Topics:**
- Windows: file system (NTFS), registry basics, Event Viewer, Task Manager, Services, Group Policy concepts
- Linux: file system hierarchy, permissions (`chmod`, `chown`), process management, `systemctl`, package managers
- macOS: directory structure, Activity Monitor, Console, Keychain, common enterprise management (Jamf concepts)
- Command line proficiency: navigation, file operations, searching, piping, redirection
- Log file locations and formats across all three OS types
- Remote access tools: RDP, SSH, VNC, TeamViewer, Zoom screen share — when to use each

**Learning Materials:**
- *The Linux Command Line* — William Shotts (free at linuxcommand.org)
- Microsoft Learn: Windows Server Administration Fundamentals (free)
- OverTheWire: Bandit (levels 0–15) — gamified Linux CLI
- Apple Support: macOS User Guide (free)

**Exercises:**
1. Complete OverTheWire Bandit levels 0–12, documenting the command used and what it teaches at each level
2. On a Windows machine, find and interpret: 5 different Event IDs in Event Viewer, a running service you can stop/start safely, a startup program, and a scheduled task. Write what each one does
3. On Linux (use a free VM or WSL), write a bash one-liner for each: find all files modified in the last 24 hours, search for the word "error" in all `.log` files in `/var/log`, list the top 5 processes by memory usage, and count lines in a file
4. Document the exact location of system logs on Windows, Linux, and macOS — build a reference table with: log name, path, what it contains, and when a support engineer would read it

**Mini-Project — Cross-Platform Admin Reference Guide:**
Create a comprehensive, formatted reference guide (Markdown) covering the most important support tasks across Windows, Linux, and macOS in parallel columns: checking disk space, managing processes, viewing network connections, reading logs, managing users, installing software, and checking system resource usage. This becomes a personal cheat sheet you use throughout the rest of the roadmap.

---

### 0.4 Professional Communication Fundamentals

**Topics:**
- Written communication: clarity, tone, concision — writing for non-technical users
- The anatomy of a great support reply: acknowledge, clarify, resolve, next steps
- Active listening in voice/chat support — paraphrasing, probing questions
- Empathy in technical communication: frustrated users, high-pressure situations
- Internal vs. external communication: how you write to a customer vs. a colleague
- Email etiquette: subject lines, threading, CC/BCC discipline
- Documentation basics: why you write what you write

**Learning Materials:**
- *The Elements of Style* — Strunk & White (short, essential)
- Zendesk Blog: "How to Write a Good Support Email" (free)
- *Crucial Conversations* — Patterson et al. (Ch. 1–4 for conflict basics)
- HubSpot Academy: Customer Service Fundamentals (free certification)

**Exercises:**
1. Rewrite these 3 bad support replies into professional, empathetic, clear responses: (a) "Did you restart it?" (b) "That's not something we support." (c) "I don't know, I'll check." — For each, write the corrected version and explain every change you made
2. Write a response to a furious customer who says the product deleted 3 months of their work and they're threatening legal action. You don't yet know if data recovery is possible. Practice acknowledging, de-escalating, setting expectations, and committing to specific next steps
3. Read 5 real company support documentation pages (pick any major SaaS product). Score each on: clarity (1–5), completeness (1–5), scannability (1–5), and tone (1–5). Write one paragraph of improvement suggestions for each
4. Write a professional internal escalation message for a critical customer issue: include a one-sentence summary, what's been tried, customer impact, urgency level, and what you need from the escalation team

**Mini-Project — Customer Communication Playbook:**
Write a personal playbook (Markdown) of 10 common support situations with template responses for each, including: first response to a new ticket, request for more information, delivering bad news (can't fix), setting timeline expectations, escalating to a specialist, closing a ticket, following up after no response, responding to a review/complaint, handling a VIP/executive customer, and responding to a billing dispute. Each template must be customizable and include notes on when to use it.

---

### ✅ Phase 0 Mega-Project — New Hire Orientation Guide

Imagine you just joined a fictional B2B SaaS company called **Nexora** (project management software, 500 employees, SMB market). Create a complete orientation guide for the next support hire covering everything in Phase 0:

**Deliverables:**
- **Hardware reference card:** What specs matter for common Nexora customer issues
- **Network troubleshooting flowchart:** Tailored to Nexora's web-based product
- **OS quick-reference guide:** The commands and tools most relevant to supporting Nexora customers across Windows, Linux, and macOS
- **Communication standards document:** Nexora's voice and tone, 5 template responses, escalation procedure

Format: a single organized Markdown document structured as an actual company onboarding guide, minimum 2,500 words. This document should be good enough that a real new hire could use it on day one.

---

## Phase 1 — Core Support Skills (Weeks 7–14)

> **Goal:** Develop the operational skills of an effective Support Engineer L1 — ticketing, troubleshooting methodology, knowledge management, and SLA management.

### 1.1 Ticketing Systems & Workflow

**Topics:**
- Ticketing system anatomy: ticket fields, statuses, priorities, queues, SLAs
- Major platforms: Zendesk, Freshdesk, Jira Service Management, ServiceNow — core concepts
- Ticket lifecycle: open → in-progress → pending → resolved → closed
- ITIL basics: Incident Management, Problem Management, Change Management, Service Request
- Queue management: triage, prioritization, load balancing
- Macros, triggers, automations — what they do and why they save time
- SLA definitions: First Response Time (FRT), Time to Resolution (TTR), breach alerting

**Learning Materials:**
- Zendesk Support Training (free on Zendesk Learn)
- Freshdesk Academy (free)
- ITIL 4 Foundation overview — Axelos (free primer available)
- Atlassian: ITIL Incident Management guide (free blog)

**Exercises:**
1. Set up a free Zendesk or Freshdesk trial account. Create: 3 ticket forms with custom fields, 2 SLA policies (one for free users, one for paid), 3 automated triggers (auto-reply on new ticket, escalation warning at 80% SLA, close after 5 days no response), and 5 macros for common responses
2. Given 15 mixed incoming tickets (write them yourself or use samples below), triage them by priority (P1–P4) with written justification for each prioritization decision. Include: 3 critical outage reports, 3 billing questions, 3 feature requests, 3 how-to questions, and 3 login issues
3. Map the full ITIL Incident Management lifecycle to a real scenario: a SaaS product's API goes down for enterprise customers. Write what happens at each stage, who is involved, and what communications go out
4. Design a ticket escalation matrix for a 3-tier support team: define what L1 handles, what gets escalated to L2 (technical specialists), and what goes to L3 (engineering). Include specific criteria for each escalation path

**Mini-Project — Zendesk/Freshdesk Configuration Portfolio:**
Using your trial account, build a complete support system for fictional company Nexora: full ticket form, 4 SLA policies by customer tier, view configurations for different queue types (new, urgent, overdue, my tickets), 10 macros covering the most common scenarios, 5 automation rules, and a satisfaction survey trigger. Export screenshots and configuration descriptions into a documented portfolio.

---

### 1.2 Troubleshooting Methodology

**Topics:**
- Structured troubleshooting frameworks: 5 Whys, Divide and Conquer, OSI-layer approach
- Information gathering: asking the right questions, reproducing the issue
- Hypothesis formation and testing — eliminating variables systematically
- Distinguishing symptoms from root causes
- When to escalate vs. when to keep investigating
- Documentation while troubleshooting: notes, screenshots, log collection
- Avoiding common traps: confirmation bias, anchoring, scope creep

**Learning Materials:**
- *The Practice of System and Network Administration* — Limoncelli et al. (Ch. 1–3)
- CompTIA A+ Troubleshooting Theory (any study guide — the methodology section)
- Google SRE Book: Chapter on troubleshooting (free at sre.google)

**Exercises:**
1. Apply the 5 Whys to 5 fictional support scenarios: (a) customer can't log in, (b) emails not sending, (c) dashboard loading slowly, (d) file upload failing, (e) API returning 500 errors. For each, write all 5 "why" levels and the root cause revealed
2. Given a complex fictional scenario (a user reports "nothing works"), write out every clarifying question you'd ask in the first message, organized by OSI layer — from application down to physical
3. Role-play a troubleshooting session in writing: a customer says "my integration broke." Write the full conversation — your questions, their answers (invent them), your hypotheses, your tests, and the resolution — in 10 exchanges
4. Create a "troubleshooting journal" for 5 fake tickets you resolve from start to finish: document your initial theory, what you tried, what failed, what succeeded, and what you learned

**Mini-Project — Troubleshooting Playbooks (5 Scenarios):**
Write detailed troubleshooting playbooks for 5 common SaaS support scenarios, each including: symptom description, information to gather upfront, diagnostic steps in order, decision points (continue investigating vs. escalate), resolution paths for each branch, and a post-resolution verification step. Scenarios: (1) User can't log in, (2) Third-party integration not syncing, (3) Feature working for some users but not others, (4) Performance is slow for one customer, (5) Email notifications not arriving.

---

### 1.3 Knowledge Base Management

**Topics:**
- Knowledge-Centered Service (KCS) methodology: capture, structure, reuse, improve
- Anatomy of a great KB article: title, symptoms, cause, resolution, related articles
- Writing for scanability: headers, numbered steps, screenshots, code blocks
- Article maintenance: when to update, when to retire, ownership and review cycles
- Internal KB vs. customer-facing KB: different purposes, different writing styles
- Search optimization for KB articles: keywords, tagging, metadata
- Measuring KB effectiveness: deflection rate, search-to-click, article feedback

**Learning Materials:**
- KCS Academy: KCS v6 Practices Guide (free PDF)
- Confluence documentation: Space and page best practices (free)
- Atlassian Team Playbook: Documentation Health Check (free)
- *Docs for Developers* — Bhatti et al. (practical technical writing)

**Exercises:**
1. Find 5 KB articles from real companies (any major SaaS product's help center). Score each using a rubric: title clarity, symptom coverage, step clarity, screenshot use, and freshness. Write improvement notes for each
2. Take a complex support ticket resolution (invent one) and convert it into a polished, customer-facing KB article following KCS structure. Then rewrite it as an internal technical note for L2 engineers
3. Build a KB article template in Markdown with placeholder sections for every required element. Include guidance notes (in comments) on what to write in each section
4. Given a list of 20 support tickets on similar topics, identify which 3 KB articles would deflect the most tickets. Write titles, outlines, and the first section of each

**Mini-Project — Nexora Help Center (10 Articles):**
Write 10 complete, publication-ready KB articles for Nexora covering: account setup, password reset, SSO configuration, API key generation, webhook setup, billing FAQ, data export, third-party integrations (2 articles), and troubleshooting common errors. Each article must include a title, meta description, symptom section, step-by-step resolution with numbered steps, at least one code block or configuration example, and related article links.

---

### 1.4 SLA Management & Prioritization

**Topics:**
- SLA anatomy: response time, resolution time, uptime guarantees, penalties
- Priority matrices: impact × urgency = priority
- P1–P4 definitions across different company types and customer tiers
- Time management in a support queue: batching, focus time, context switching cost
- Escalation triggers: SLA breach warnings, customer escalation, executive involvement
- Communicating proactively during high-load periods
- Personal productivity tools: time blocking, ticket batching, EOD queue reviews

**Learning Materials:**
- PagerDuty: Incident Response Documentation (free)
- Intercom Blog: "How to manage support queue" (free)
- *Getting Things Done* — David Allen (Ch. 1–4 for triage methodology)

**Exercises:**
1. Design a priority matrix for Nexora: define P1 through P4 with specific criteria for each, differentiated by customer tier (free, growth, enterprise). Include example tickets that fit each cell
2. Given a queue of 30 tickets with mixed priorities and SLA deadlines, write a prioritized work plan for an 8-hour shift: what you tackle first, when you batch similar work, what you defer, and when you take breaks
3. Write 3 proactive customer communication templates for: (a) you're about to breach an SLA and need more time, (b) you're waiting on engineering and have no ETA, (c) an incident is affecting the customer and you're on it before they noticed
4. Track your own time for one full workday (or simulate it): log every task, its priority, how long it took, and whether you'd do it differently with better prioritization

**Mini-Project — SLA Operations Manual:**
Write a complete SLA operations manual for Nexora's support team including: SLA definitions by tier and priority, breach prevention checklist, escalation workflow diagram, shift handoff template, queue health metrics to monitor daily, and a personal time management framework for handling 40+ tickets per day. Minimum 1,500 words.

---

### ✅ Phase 1 Mega-Project — Simulate a Full Support Week

Simulate a complete week of L1 support work for Nexora. Create 40 fictional but realistic tickets (mix of priorities, customer types, and issue categories). Then:

**Day 1 (Monday):** Triage all 40 tickets, assign priorities, create your work plan for the week  
**Day 2 (Tuesday):** Resolve 10 tickets in writing — full responses, troubleshooting steps, KB links  
**Day 3 (Wednesday):** Escalate 5 tickets with full escalation notes; handle 2 SLA-at-risk tickets with proactive communication  
**Day 4 (Thursday):** Write 3 new KB articles from patterns observed in the ticket queue  
**Day 5 (Friday):** Write end-of-week report: tickets resolved, SLA compliance rate, patterns spotted, knowledge gaps identified, and 3 process improvement suggestions

**Deliverable:** A complete Markdown document structured as a week's worth of work — this simulates a real L1 Support Engineer's output and becomes the centerpiece of your portfolio.

---

## Phase 2 — Technical Depth (Weeks 15–26)

> **Goal:** Develop the technical skills that separate an exceptional L1 from an average one — web technologies, APIs, databases, logs, and cloud basics.

### 2.1 Web Technologies & HTTP

**Topics:**
- HTTP/HTTPS: methods (GET, POST, PUT, DELETE, PATCH), status codes (all families: 1xx–5xx), headers
- Request/response anatomy: URL structure, query parameters, request body, response body
- Authentication methods: Basic Auth, API keys, OAuth 2.0, JWT — how each works and common issues
- Cookies, sessions, and local storage — what breaks when these have problems
- CORS: what it is, why it blocks requests, how it's configured
- SSL/TLS: certificates, chain of trust, common certificate errors
- Browser developer tools: Network tab, Console, Application tab — using them for support

**Learning Materials:**
- MDN Web Docs: HTTP documentation (free — read every status code page)
- *HTTP: The Definitive Guide* — Gourley et al. (Ch. 1–6)
- Postman Learning Center (free)
- Chrome DevTools documentation (free at developer.chrome.com)

**Exercises:**
1. Use `curl` to make GET, POST, PUT, and DELETE requests to a public test API (httpbin.org or jsonplaceholder.typicode.com). Document every request, every response, and every header — explain what each header does
2. In Chrome DevTools Network tab, capture and analyze a login flow on any website. Identify: the authentication request, the cookie set, the redirect chain, and any failed requests. Document findings
3. Reproduce these 5 HTTP errors in a browser and explain root cause and resolution for each: 400, 401, 403, 404, 500, 502, 503 — then write a customer-facing explanation for each in plain English
4. Set up Postman and create a collection with 10 requests against a public API (GitHub, OpenWeatherMap, etc.). Add tests that verify: status code, response time under 2 seconds, specific field in response body

**Mini-Project — API Troubleshooting Guide:**
Write a comprehensive API troubleshooting guide for Nexora's REST API covering: all common HTTP errors customers encounter (with causes and fixes), authentication issue diagnosis (wrong key, expired token, wrong scope), rate limiting explanation and avoidance, CORS issue resolution for web integrations, and a Postman collection with examples of correct API usage. Minimum 20 documented scenarios.

---

### 2.2 APIs & Integrations Support

**Topics:**
- REST API fundamentals: endpoints, resources, pagination, versioning
- Webhooks: payload structure, delivery, retries, signature verification
- API authentication deep dive: OAuth flows (Authorization Code, Client Credentials), token refresh
- Common integration patterns: polling vs. push, sync vs. async
- Rate limiting: types (per-minute, per-day, per-key), handling 429 errors, exponential backoff
- API error diagnosis: reading error messages, request IDs, correlation IDs
- Integration platforms: Zapier, Make (Integromat), n8n — understanding what they do and common failure modes

**Learning Materials:**
- Postman API Fundamentals Student Expert (free certification)
- *Designing Web APIs* — Jin, Sahni & Shevat (Ch. 1–5)
- Zapier Engineering Blog: "How webhooks work" (free)
- Stripe Developer Documentation (model of excellent API docs — study as an example)

**Exercises:**
1. Build a Postman collection that tests an OAuth 2.0 Client Credentials flow end-to-end: get token, use token, handle expiry, refresh. Use a real OAuth provider (GitHub, Google) or mock one
2. Set up a webhook receiver using webhook.site or a simple Node.js/Python script. Trigger webhooks from a real service (GitHub, Stripe test mode, etc.) and document the payload structure, headers, and retry behavior
3. Debug these 5 fictional integration scenarios in writing: (a) Zapier integration stops syncing, (b) webhook not delivering, (c) OAuth token expires and breaks automation, (d) API rate limit hit at peak time, (e) different data in source vs. destination system
4. Read and compare the API documentation quality of 3 companies (Stripe, Twilio, Slack). Score each on: completeness, examples, error documentation, authentication clarity, and SDKs available. Write recommendations for improvement

**Mini-Project — Integration Troubleshooting Playbook:**
Build a complete integration support playbook for Nexora's top 5 integrations (invent them: e.g., Salesforce, Slack, Google Workspace, Zapier, custom REST). For each integration, document: how it works technically, common failure modes, diagnostic steps, fix or workaround, and when to escalate to engineering. Include sample API calls and webhook payloads for each.

---

### 2.3 Databases & Data Issues

**Topics:**
- Relational database fundamentals: tables, rows, columns, primary/foreign keys, indexes
- SQL basics for support: `SELECT`, `WHERE`, `JOIN`, `ORDER BY`, `LIMIT`, `COUNT` — reading data, not writing
- Common data issues: missing data, duplicate records, encoding problems, timezone mismatches
- NoSQL basics: document stores, key-value stores — what they are and when they cause issues
- Data import/export: CSV, JSON, XML formats — common customer data problems
- Database connection issues: connection strings, credentials, timeouts, pool exhaustion
- GDPR/data privacy: what support engineers can and cannot access

**Learning Materials:**
- SQLZoo (sqlzoo.net — free, interactive SQL practice)
- *Learning SQL* — Alan Beaulieu (Ch. 1–8)
- Mode Analytics SQL Tutorial (free)
- MySQL or PostgreSQL documentation: data types reference

**Exercises:**
1. Complete SQLZoo tutorials 1–7 (SELECT basics through JOIN) — write a reflection on how each concept applies to diagnosing customer data issues
2. Given a fictional database schema for Nexora (users, projects, tasks, integrations tables), write 10 SQL queries a support engineer might run: find all tasks created by a user this week, find projects with no tasks, find users who haven't logged in for 30 days, etc.
3. Debug these 5 data problems in writing: (a) customer exports CSV with garbled special characters, (b) timestamps showing wrong timezone in reports, (c) duplicate records appearing after import, (d) data syncing from integration but missing 10% of records, (e) search returning zero results for data that exists
4. Write a data privacy SOP: what data can L1 access, what requires manager approval, what is never accessible, and how to handle a customer request for their data

**Mini-Project — Data Issue Resolution Guide:**
Write a complete guide for diagnosing and resolving the 15 most common data-related support issues for a SaaS product: CSV import errors, export formatting problems, timezone confusion, duplicate records, missing data after migration, encoding issues, sync conflicts, API data mismatches, report calculation errors, and data deletion confirmations. Each entry: symptoms, root cause explanation, resolution steps, and prevention advice.

---

### 2.4 Cloud & Infrastructure Basics

**Topics:**
- Cloud providers: AWS, Azure, GCP — core services every support engineer should know
- Key services: compute (EC2/VMs), storage (S3/Blob), databases (RDS), networking (VPC)
- Availability and reliability: uptime, SLAs, regions, availability zones, failover
- Status pages and incident communication: how to read them, how to use them
- DNS management: A records, CNAMEs, MX records, TTL — common customer DNS issues
- CDN basics: how Cloudflare/CloudFront work, cache invalidation, edge locations
- SSL certificate management: Let's Encrypt, certificate renewal, mixed content errors

**Learning Materials:**
- AWS Cloud Practitioner Essentials (free on AWS Skill Builder)
- Google Cloud Fundamentals (free on Coursera)
- *The Cloud Adoption Playbook* — IBM (free PDF)
- Cloudflare Learning Center (free — excellent explanations)

**Exercises:**
1. Create a free AWS account and explore: launch a t2.micro EC2 instance, create an S3 bucket, set up a simple security group. Document what you did and what each service does — then terminate everything to avoid charges
2. Read the status pages for AWS, Google Cloud, and Cloudflare during a 2-week period. Document any incidents: what went down, how it was communicated, how long it took to resolve, and what the postmortem said
3. Troubleshoot these 5 DNS scenarios in writing: (a) CNAME not resolving, (b) TTL too high causing stale records, (c) MX records missing after domain migration, (d) SSL cert showing for wrong domain, (e) CDN serving cached old version of site
4. For each of the following customer messages, identify whether the issue is likely their infrastructure, Nexora's infrastructure, or a third party — and write your diagnostic approach: (a) "Your site is down," (b) "My custom domain isn't working," (c) "Our email notifications aren't arriving," (d) "The API is timing out"

**Mini-Project — Infrastructure Issues Playbook:**
Write a support playbook for the 10 most common infrastructure-related issues in a SaaS product: site down (Nexora's fault), site down (customer's network), custom domain not working, SSL certificate errors, email deliverability issues, slow load times (CDN/cache), API timeout under load, file upload size limits, CORS configuration errors, and IP allowlist/blocklist issues. Each entry must include: diagnosis steps, what to check in internal tools, customer communication template, and escalation criteria.

---

### ✅ Phase 2 Mega-Project — Technical Deep Dive Case Studies

Write 5 detailed technical case studies of complex support issues (fictional but realistic), each covering a different domain from Phase 2:

**Case Study 1 — Authentication Failure:** Enterprise customer can't SSO after their IT team updated their IdP. Walk through the full investigation: SAML trace analysis, error messages, HTTP debugging, resolution.

**Case Study 2 — Webhook Reliability:** Customer reports 30% of webhooks not delivering. Diagnose: server timeouts, retry logic, signature verification failure, IP allowlist issue. Deliver root cause and fix.

**Case Study 3 — Data Migration Crisis:** Customer migrated 50,000 records via CSV import; 3,000 are missing and 500 are duplicates. SQL queries to identify them, root cause analysis, and remediation plan.

**Case Study 4 — Performance Degradation:** Enterprise customer reports dashboards 10x slower than usual. Diagnose: CDN cache miss, database query spike, third-party API latency. Timeline reconstruction and fix.

**Case Study 5 — Integration Breakdown:** Customer's Salesforce integration stopped syncing after Salesforce OAuth token rotation. Full OAuth debugging, token refresh implementation, and prevention steps.

Each case study: 600–800 words, includes sample log snippets, HTTP traces, or SQL queries as appropriate, and ends with a lessons-learned section and KB article outline.

---

## Phase 3 — Advanced Support Operations (Weeks 27–38)

> **Goal:** Operate at the highest level of L1 — handle incidents, build processes, mentor peers, and interface with engineering and product teams.

### 3.1 Incident Management

**Topics:**
- Incident severity levels: SEV1–SEV4 — definitions and response requirements
- Incident roles: Incident Commander, Communications Lead, Technical Lead, Scribe
- Incident lifecycle: detection → triage → communication → resolution → postmortem
- Status page management: what to publish, when, and how
- Customer communication during incidents: frequency, tone, content, channels
- Internal war room: Slack channels, Zoom bridges, runbooks
- Postmortem methodology: blameless culture, timeline reconstruction, action items
- PagerDuty/OpsGenie: alerting, on-call rotations, escalation policies

**Learning Materials:**
- PagerDuty Incident Response Guide (free ebook at pagerduty.com)
- Google SRE Book: Chapter on Incident Management (free at sre.google)
- Atlassian: Incident Management Handbook (free)
- *Site Reliability Engineering* — Google (Ch. 14: Managing Incidents)

**Exercises:**
1. Run a tabletop incident exercise: Nexora's API goes down at 2 PM on a Tuesday. Write out the full response in real-time narrative: who gets paged, what gets posted where, what the first 30 minutes look like, what the customer communication says, and how the incident closes
2. Write a postmortem for a fictional incident: Nexora database failover caused 45 minutes of write unavailability affecting 500 enterprise customers. Include: timeline (minute by minute), contributing factors, root cause, impact assessment, and 5 action items with owners and due dates
3. Draft 5 status page updates for different stages of an incident: initial detection (limited info), active investigation (cause unknown), identified (working on fix), fix deployed (monitoring), and resolved (full RCA link)
4. Design an on-call runbook for a specific alert type (e.g., "API error rate > 5% for 5 minutes"): what to check first, what actions to take, when to escalate, and what to log

**Mini-Project — Incident Response Playbook:**
Write a complete incident response playbook for Nexora covering: severity definitions with examples, incident role cards (what each person does), communication templates for each severity and each stage, status page guidelines, postmortem template, and a blameless postmortem facilitation guide. Deliver as a professional operations document — something a team would actually use during a live incident.

---

### 3.2 Advanced Troubleshooting & Log Analysis

**Topics:**
- Log formats: structured (JSON) vs. unstructured, common log levels (DEBUG, INFO, WARN, ERROR, FATAL)
- Log analysis tools: Kibana/Elasticsearch, Splunk (basics), Datadog Logs, Papertrail
- Reading application logs: identifying error patterns, request IDs, tracing a request end-to-end
- Performance troubleshooting: latency, throughput, error rates — the "golden signals"
- Network packet analysis: Wireshark basics for support (not security)
- HAR files: capturing and reading browser network traces for escalation
- `grep`, `awk`, `sed` for log parsing in the command line

**Learning Materials:**
- Elastic: Getting Started with Kibana (free tutorial)
- Datadog Learning Center (free)
- *Systems Performance* — Brendan Gregg (Ch. 2 — Methodology)
- Wireshark User's Guide (free at wireshark.org)

**Exercises:**
1. Given a sample application log file (create a realistic one with 500 lines including errors), write `grep` commands to: extract all ERROR lines, find all requests from a specific user ID, count occurrences of each error type, and show the 10 lines before and after each FATAL error
2. Analyze a provided HAR file (export one from Chrome DevTools from any website) and identify: slowest requests, failed requests, largest payloads, redirect chains, and any suspicious patterns
3. Set up a free Papertrail or Logtail account, send sample logs to it, and build 3 saved searches: all errors in the last hour, requests from a specific IP, and requests taking more than 2 seconds
4. Given 5 snippets of application logs with errors, diagnose what's happening, classify the severity, and write the escalation message you'd send to engineering for each

**Mini-Project — Log Analysis Workbook:**
Create a log analysis workbook containing: 10 real log snippets (fictional but realistic) with your analysis of each, a library of `grep`/`awk` one-liners for the 20 most common log analysis tasks, a guide to reading Nexora's (fictional) application logs including field definitions and common patterns, and a HAR file analysis checklist for reproducing customer-reported frontend issues.

---

### 3.3 Product Feedback & Cross-Functional Collaboration

**Topics:**
- Translating support tickets into product insights: bug vs. feature request vs. UX issue
- Writing bug reports that engineers actually use: steps to reproduce, expected vs. actual, environment
- Feature request documentation: customer impact, frequency, use case, workaround
- Working with product managers: how roadmap decisions get made, how support feeds in
- Customer advisory input: using support data to make product cases
- Support-driven development: support as a product feedback loop
- Stakeholder communication: writing executive summaries of support trends

**Learning Materials:**
- *Continuous Discovery Habits* — Teresa Torres (Ch. 1–4)
- Intercom Blog: "How support and product teams should work together" (free)
- JIRA documentation: Bug reporting best practices (free)

**Exercises:**
1. Write 5 engineering-quality bug reports from these vague customer descriptions: (a) "the button doesn't work," (b) "my data disappeared," (c) "it's slow sometimes," (d) "the integration is broken," (e) "I can't see my team's stuff." Each report must include: title, severity, environment, steps to reproduce, expected result, actual result, and supporting evidence
2. Analyze 20 fictional tickets (write them) and produce a product insights report: top 3 bugs by frequency, top 3 feature requests by customer impact, top UX friction point, and 2 documentation gaps. Write the executive summary version (200 words) and the detailed version (800 words)
3. Write a business case for prioritizing one specific product fix based on support ticket volume, customer tier impact, and churn risk. Structure it as a proposal to a product manager
4. Design a monthly support insights report template that a team could use to consistently communicate trends to product and engineering leadership

**Mini-Project — Quarterly Support Insights Report:**
Write a complete, fictional quarterly support insights report for Nexora as if you're presenting to leadership. Include: ticket volume trends, SLA compliance, top issue categories (with ticket counts), recurring bugs, feature requests ranked by customer impact, customer satisfaction trends, churn risk signals from support data, and 5 recommended actions for product and engineering. Make it look like a real business document — use tables, data, and an executive summary.

---

### 3.4 Mentoring & Knowledge Sharing

**Topics:**
- Peer mentoring: how to teach troubleshooting, not just give answers
- Code reviews for KB articles: how to give feedback on others' documentation
- Shadowing and reverse-shadowing programs
- Running ticket review sessions: what makes a ticket response excellent
- Building team playbooks and standard operating procedures (SOPs)
- Presenting in team meetings: sharing learnings from complex tickets
- Onboarding new team members: structured 30-60-90 day plans

**Learning Materials:**
- *The Coaching Habit* — Michael Bungay Stanier (short, practical)
- *Radical Candor* — Kim Scott (feedback and mentoring)
- First Round Review: "How to Be a Great Mentor" (free article)

**Exercises:**
1. Write a 30-60-90 day onboarding plan for a brand-new L1 support engineer joining Nexora. Be specific: what they learn each week, what tasks they take on when, and what milestones they must hit
2. Choose 3 KB articles you've written in previous phases. Conduct a "self code review" — review each as if someone else wrote it. What would you change, add, or remove? Write the feedback you'd give
3. Create a 15-minute training session outline (slides or document) on a technical topic from Phase 2 — as if you're presenting it to 5 new team members who are non-technical
4. Write a team retrospective agenda and facilitator guide for a monthly support team meeting: what to review, how to surface problems safely, how to generate action items, and how to follow up

**Mini-Project — Team Enablement Package:**
Create a complete enablement package for Nexora's L1 support team including: new hire 30-60-90 day plan, team SOP for the top 5 most common ticket types, KB article quality rubric, ticket response quality rubric (for peer review), a monthly team health dashboard template (tracking SLA, volume, CSAT, escalation rate), and a quarterly skill assessment checklist for L1 engineers. Package as a single professional Markdown document.

---

### ✅ Phase 3 Mega-Project — Support Operations Handbook

Write a complete, professional-grade Support Operations Handbook for Nexora — a document that could be handed to a new support manager on day one and used to run the team.

**Required sections:**
- Team structure and roles (L1, L2, L3, manager)
- Ticketing system configuration and workflow
- SLA definitions and breach escalation procedures
- Priority matrix and triage guidelines
- Incident response playbook
- KB management standards and governance
- Bug reporting and product feedback process
- New hire onboarding program
- Team health metrics and reporting cadence
- Cross-functional communication protocols (with Engineering, Product, Sales, Customer Success)

**Minimum 5,000 words.** Format professionally with a table of contents, numbered sections, tables, diagrams (Mermaid or ASCII), and template documents embedded throughout. This is the flagship portfolio piece of Phase 3.

---

## Phase 4 — Specialization Tracks (Weeks 39–52)

> **Goal:** Develop expertise in a domain that opens the path to L2, a specialist role, or a higher-impact position.

---

### Track A — API & Developer Support Specialist

**Industry Demand:** Very High | **Transition Path:** Developer Support Engineer, Technical Account Manager

**Topics:**
- Deep REST and GraphQL API support
- SDK troubleshooting across languages (Python, JavaScript, Ruby, Java)
- Developer experience: evaluating API documentation quality, SDK usability
- Postman advanced features: environments, scripts, monitors, mock servers
- Reading and debugging code in support context (not writing production code)
- Webhook delivery systems: queuing, retries, dead letter queues
- API security: OAuth, rate limiting, scopes, IP allowlisting

**Exercises & Projects:**
1. Build a Postman mock server that simulates Nexora's API — use it to reproduce customer issues without hitting production
2. Debug 10 code snippets (Python, JavaScript, curl) sent by fictional customers — find the bug in each and write a corrected version with explanation
3. Write a complete "Getting Started" guide for Nexora's API aimed at developers who've never used it — include real code samples in 3 languages
4. Create an API health monitoring Postman collection that runs on a schedule and alerts if any endpoint returns unexpected responses

**Track Mega-Project:** Build a complete Developer Support Kit: Postman collection (20+ requests, full OAuth flow, error examples), SDK quickstart guides for 3 languages, an interactive API troubleshooting guide, a webhook testing toolkit, and a common integration patterns document. Publish everything to a public GitHub repo with a polished README.

---

### Track B — Cloud & Infrastructure Support Specialist

**Industry Demand:** Very High | **Transition Path:** Cloud Support Engineer, SRE, Platform Engineer

**Topics:**
- AWS/Azure/GCP deep dive: compute, networking, storage, IAM, billing
- Infrastructure as Code: Terraform and CloudFormation basics (reading, not authoring)
- Container support: Docker fundamentals, Kubernetes concepts (pod, service, deployment)
- Monitoring and observability: Datadog, New Relic, Prometheus/Grafana — reading dashboards
- Network troubleshooting in cloud: VPC, security groups, NACLs, peering
- Cloud billing and cost anomaly investigation
- On-call and alerting: PagerDuty setup, runbook execution

**Exercises & Projects:**
1. Set up a Docker container running a simple web application; practice starting, stopping, inspecting logs, and troubleshooting a broken container
2. Read and interpret a Terraform plan output for a cloud deployment — identify what resources will be created, modified, and destroyed and what risks exist
3. Build a Datadog or Grafana dashboard (free tier) that monitors key metrics for a simple application: request rate, error rate, latency (the "golden signals")
4. Write runbooks for 5 common cloud infrastructure alerts: high CPU, disk space full, network packet loss, unhealthy load balancer target, certificate expiring

**Track Mega-Project:** Design and document a cloud infrastructure support program for Nexora: runbooks for the 10 most critical infrastructure alerts, a cloud cost anomaly investigation procedure, a deployment rollback SOP, a disaster recovery communication plan, and a vendor escalation guide (how to open and manage AWS/Azure/GCP support tickets effectively). Deliver as a complete operations document.

---

### Track C — Enterprise & Strategic Account Support

**Industry Demand:** High | **Transition Path:** Technical Account Manager, Customer Success Engineer, Enterprise Support Lead

**Topics:**
- Enterprise customer dynamics: stakeholder mapping, IT vs. business buyer
- SLA negotiation and custom support agreements
- Executive escalation management: VP-to-VP communication, war rooms
- Quarterly Business Reviews (QBRs): presenting support data to customers
- Customer health scoring: how to detect churn risk in support data
- Enterprise security requirements: SSO, SCIM, audit logs, data residency
- Change management support: helping enterprises roll out new software

**Exercises & Projects:**
1. Write an executive escalation communication for a situation where Nexora caused 4 hours of downtime for a customer's 500-person team — address the CTO
2. Build a QBR presentation template for an enterprise customer: SLA compliance, ticket trends, product usage, upcoming features, and action items — for a 30-minute executive meeting
3. Develop a customer health scorecard using support signals: ticket volume trend, CSAT scores, escalation frequency, feature adoption, and response to follow-ups
4. Write a custom SLA proposal for a fictional enterprise customer with specific requirements: 15-minute response for P1, 24/7 coverage, dedicated support engineer, and monthly reporting

**Track Mega-Project:** Create a complete Enterprise Support Program for Nexora: tiered SLA definitions, dedicated customer onboarding playbook, QBR template and facilitation guide, executive escalation protocol, customer health monitoring dashboard, churn early-warning system using support metrics, and a customer advocacy program framework for turning high-satisfaction customers into references. Deliver as a board-ready business document.

---

### Track D — Support Engineering & Tooling

**Industry Demand:** High | **Transition Path:** Support Engineer (L2/L3), Software Engineer in Support, Technical Program Manager

**Topics:**
- Python scripting for support automation: ticket analysis, bulk updates, reporting
- REST API automation: using support tool APIs (Zendesk, Jira) to automate workflows
- Data analysis for support: pandas, Excel/Google Sheets for ticket trend analysis
- Building internal tools: simple dashboards, Slack bots, automation scripts
- AI in support: LLM-assisted responses, ticket classification, KB suggestions
- Metrics and reporting: building support dashboards that drive decisions
- SQL for support analytics: writing queries against support data

**Exercises & Projects:**
1. Write a Python script that calls the Zendesk API (or mock it) to: pull all open tickets, group them by priority and type, calculate SLA breach risk, and output a formatted daily digest
2. Build a Slack bot (using Slack API) that allows support engineers to look up customer account status, recent tickets, and open incidents by typing a command
3. Write SQL queries to power a support analytics dashboard: average TTR by priority, CSAT trend by month, ticket volume by category, top 10 customers by ticket count, and SLA breach rate by team member
4. Prototype an AI-assisted ticket routing system: given a ticket subject and body, use an LLM API to classify it into a category and suggest the top 3 KB articles

**Track Mega-Project:** Build a complete Support Intelligence Platform for Nexora: Python backend that pulls from ticketing API, a SQL data model for support analytics, a web dashboard (simple HTML/JS or Streamlit) showing key metrics, an automated daily digest Slack bot, an AI-powered KB suggestion tool, and a ticket trend anomaly detector that flags unusual spikes. Publish to GitHub with documentation.

---

## Phase 5 — Senior L1 & Growth (Weeks 53–65)

> **Goal:** Operate as a senior-level L1 engineer — a technical authority, process owner, and bridge between support and engineering.

### 5.1 Technical Authority Development

**Topics:**
- Becoming a subject matter expert (SME): picking a product domain and going deep
- Handling the tickets no one else can: escalation as a last resort, not a first move
- Building internal technical guides: architecture diagrams, system explanations for support
- Reading engineering documentation: architecture decision records (ADRs), technical specs
- Participating in engineering reviews: providing the support perspective on new features
- Security awareness in support: recognizing social engineering, data handling, access control

**Exercises:**
1. Pick one product area of Nexora (invent it — e.g., the reporting engine). Write a complete technical deep-dive document explaining how it works, what can go wrong, and how to troubleshoot every failure mode
2. Shadow (or simulate) an engineering standup — write a "support translation" of what engineering discussed into customer-impact language
3. Review a fictional engineering spec for a new feature and write the support readiness checklist: what training is needed, what KB articles must be written, what questions customers will ask
4. Create a "top 10 hardest tickets" analysis: describe 10 complex fictional tickets, why they were hard, what you had to learn to resolve them, and what you built to prevent them recurring

---

### 5.2 Process Ownership & Continuous Improvement

**Topics:**
- Support process auditing: identifying bottlenecks, redundancies, and gaps
- Metrics-driven improvement: using data to make the case for process changes
- A/B testing in support: testing response templates, KB article formats, workflows
- Automation opportunity identification: what to automate first and why
- Building a culture of feedback: retrospectives, 1:1s, peer reviews
- Writing proposals for process improvements: structure, evidence, ROI

**Exercises:**
1. Audit your fictional Nexora support team's processes (use everything you've built in this roadmap) — identify the top 5 inefficiencies and write a prioritized improvement plan
2. Design an A/B test for a KB article: write two versions of the same article with different formats, define your success metric, and outline how you'd run the test for 4 weeks
3. Write a business case for implementing AI-assisted ticket classification at Nexora: time saved per week, cost of implementation, expected error rate, and a rollout plan
4. Build a quarterly retrospective framework for a support team: what to review, how to surface problems, how to measure improvement month-over-month

---

### 5.3 Career Positioning & Professional Growth

**Career Paths from L1 Support Engineer:**

| Path | Timeline | Key Skills to Build Now |
|------|----------|------------------------|
| L2 / Senior Technical Support | 12–18 months | Deep product expertise, scripting, log analysis |
| Developer Support Engineer | 12–24 months | API depth, coding ability, developer empathy |
| Technical Account Manager | 18–30 months | Enterprise communication, business acumen |
| Solutions Engineer / Pre-Sales | 18–30 months | Product demos, technical storytelling |
| Customer Success Manager | 12–24 months | Relationship management, metrics, renewal |
| Support Engineer (Product) | 24–36 months | Python, APIs, data analysis, internal tooling |
| Site Reliability Engineer | 36–48 months | Infrastructure, coding, on-call, monitoring |

**Building Your Portfolio:**
- **GitHub:** Document all projects from this roadmap — clean READMEs, organized folders
- **LinkedIn:** Write 3 long-form posts about lessons from support work — demonstrates expertise publicly
- **Internal reputation:** Be the person who writes the best KB articles, runs the best incidents, mentors the newest hires
- **Metrics you own:** Track your own CSAT, TTR, FRT, escalation rate, KB articles authored — bring these to performance reviews

---

### ✅ Phase 5 Mega-Project — Capstone: Support Excellence Program

Design and deliver a complete Support Excellence Program for Nexora as your final capstone. This is a senior-level strategic document that demonstrates full mastery of L1 support engineering.

**Required deliverables:**

1. **Technical Competency Framework:** Skills matrix for L1 through L3 — what each level must know and be able to do, with assessment criteria
2. **Support Architecture Document:** How Nexora's support system is built — tools, workflows, integrations, data flows — with diagrams
3. **Annual Support Strategy:** Goals for the year, OKRs for the support team, quarterly milestones, metrics and targets
4. **Knowledge Management System Design:** How KB is governed, measured, maintained, and improved over time
5. **Automation Roadmap:** 5 automation opportunities ranked by impact and feasibility, with implementation plans
6. **AI Integration Proposal:** How to incorporate AI assistance into the support workflow, with risk mitigation
7. **Team Development Program:** Career ladders, mentoring structure, training curriculum, performance review framework

**Minimum 8,000 words across all sections.** This document is your flagship portfolio piece — it demonstrates that you can operate not just as an excellent L1 support engineer, but as someone ready to lead and shape a support organization.

---

## Resources & Certifications

### Certification Roadmap by Phase

| Phase | Certification | Provider | Cost | Value |
|-------|--------------|----------|------|-------|
| 0 | CompTIA IT Fundamentals (ITF+) | CompTIA | $$ | Entry-level baseline |
| 0–1 | Google IT Support Certificate | Coursera/Google | $ | Widely recognized entry cert |
| 1 | HDI Customer Service Representative | HDI | $$ | Support-specific credential |
| 1–2 | CompTIA A+ | CompTIA | $$$ | Industry standard IT support |
| 2 | ITIL 4 Foundation | Axelos/PeopleCert | $$$ | Service management standard |
| 2 | Postman API Fundamentals Expert | Postman | Free | Strong API signal |
| 2–3 | CompTIA Network+ | CompTIA | $$$ | Networking depth |
| 3 | AWS Cloud Practitioner | AWS | $$ | Cloud credibility |
| 4A | Postman API Test Automation | Postman | Free | Developer support track |
| 4B | AWS Solutions Architect Associate | AWS | $$$ | Infrastructure track |
| 4C | HDI Support Center Analyst | HDI | $$ | Enterprise support track |
| 5 | ITIL 4 Specialist | Axelos | $$$$ | Senior operations |

> **$ = <$100 | $$ = $100–300 | $$$ = $300–500 | $$$$ = $500+**

> 💡 In support engineering, your ticket metrics, KB contributions, and documented projects matter as much as certifications. Build both.

### Essential Free Resources

**Technical Learning:**
- Professor Messer (professormesser.com) — CompTIA A+ and Network+ free courses
- OverTheWire Bandit — Linux CLI practice (gamified)
- SQLZoo (sqlzoo.net) — SQL practice
- HTTPbin.org — HTTP request testing
- MDN Web Docs — HTTP and web fundamentals reference

**Support Craft:**
- Zendesk Blog (zendesk.com/blog) — support operations insights
- Intercom Blog — customer communication best practices
- Support Driven Community (supportdriven.com) — support professional community
- Help Scout Blog — support leadership articles
- Rethink Support Podcast

**Industry Reading:**
- Google SRE Book (sre.google — free online)
- PagerDuty Incident Response Guide (free ebook)
- KCS Academy resources (serviceinnovation.org)

---

## Tools & Environment Setup

### Core Toolchain for Support Engineers

**Communication & Ticketing:**
- Zendesk or Freshdesk (free trial accounts for practice)
- Slack (free tier for personal learning)
- Confluence or Notion (free tier for KB practice)
- JIRA (free tier for bug tracking practice)

**Technical Tools:**
- Terminal / Command Prompt — use it daily, always
- Postman (free) — API testing and documentation
- Chrome DevTools — built into browser, no install needed
- Wireshark (free) — network packet analysis
- VS Code (free) — editing Markdown, scripts, log files

**Log & Monitoring:**
- Papertrail or Logtail (free tier) — log management practice
- Datadog (free trial) — monitoring and APM
- UptimeRobot (free) — uptime monitoring

**Productivity:**
- Obsidian or Notion — personal knowledge management
- Loom (free tier) — async video for customer explanations
- Calendly (free tier) — scheduling for support calls

### Recommended Learning Environment

```
Your Learning Setup/
├── projects/
│   ├── phase-0-hardware-runbook/
│   ├── phase-0-network-decision-tree/
│   ├── phase-1-zendesk-portfolio/
│   ├── phase-1-support-week-simulation/
│   ├── phase-2-api-troubleshooting-guide/
│   ├── phase-2-technical-case-studies/
│   ├── phase-3-incident-playbook/
│   ├── phase-3-support-ops-handbook/
│   ├── phase-4-specialization-project/
│   └── phase-5-excellence-program/
├── references/
│   ├── command-line-cheatsheet.md
│   ├── http-status-codes.md
│   ├── sql-queries-library.md
│   └── communication-templates.md
└── learning-log.md  ← Track what you learn each week
```

### Daily Practice Habits

These habits, done consistently, will accelerate your development faster than any single resource:

- **Spend 20 minutes daily** on OverTheWire Bandit or SQLZoo — small daily practice compounds
- **Read one support or technical blog post** per day (bookmark Zendesk Blog, Intercom, Google SRE)
- **Write something every day** — a KB draft, a ticket response, a troubleshooting note — writing is the core skill
- **Use the terminal** for at least one task daily — file management, log grep, curl request — anything
- **Review one real incident postmortem per week** — engineering blogs (GitHub, Cloudflare, Stripe) publish excellent ones

---

## Progress Checkpoints

### Readiness Tests Before Each Phase

**Before Phase 1:** Can you explain the OSI model, run 5 network diagnostic commands, and write a professional reply to an angry customer?

**Before Phase 2:** Can you manage a ticket queue, write a structured troubleshooting playbook, and build a KB article from scratch?

**Before Phase 3:** Can you debug an HTTP request, explain OAuth, write a SQL query, and diagnose a DNS problem?

**Before Phase 4:** Can you manage a P1 incident, write a postmortem, analyze application logs, and present support data to stakeholders?

**Before Phase 5:** Have you completed a specialization track and built a complete portfolio of projects from Phases 0–4?

---

*Last updated: 2025 | This roadmap aligns with: HDI Support Center Practices, ITIL 4 Foundation, CompTIA CertMaster paths, and L1–L2 Support Engineer job description analysis across 200+ SaaS companies.*