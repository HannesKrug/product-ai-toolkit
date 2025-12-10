# State Of The Product Report
*Threedy GmbH - Q4 2025 & Year-End Review*

---
**Date:** 2025-12-09

**Period Covered:** Q4 2025 (Oct-Dec)

**Audience:** All Departments (R&D, Commercial, Leadership)

**Author:** Hannes Krug, Senior Product Manager

---

## 1. Executive Summary

instant3Dhub demonstrated **resilience and growth in 2025**, with Unique Sessions averaging 111K/month (vs. 90K in Q4 2024), peaking at 137K in July. We completed critical strategic projects (Catena-X, USD Support, MB Digitale Prozesskette, MB Sma4u, 3D Suite) and advanced BRIX development for 2026 launch. However, **systematic feedback from both internal teams and customers reveals critical product gaps that are limiting adoption, slowing integration, and creating competitive vulnerabilities.**

**This report focuses on what we learned from comprehensive Internal and Customer Advisory Board sessions, identifying 10 prioritized product gaps that must be addressed to unlock growth in 2026.**

**Key Wins Q4 2025:**
- Strategic projects delivered: Catena-X standard integration (ZF, BMW, Mercedes, Bosch contributing), USD Support, MB Digitale Prozesskette, MB Sma4u, 3D Suite
- BRIX library development progressing (planned 2026 launch - foundation for developer ecosystem)
- First Fortune 500 customer closed (enterprise credibility milestone)
- Unique Sessions growth trajectory sustained (~+23% vs Q4 2024)

**Key Challenges:**
- **Integration & deployment complexity** blocking customer onboarding (Bosch, Grimme delays; Daimler Truck Helm challenges)
- **Product adoption at End Users remains fragile** – DT (Daimler Truck) is one major example supporting this
- **Documentation & developer self-service gaps** causing support overhead and slow time-to-value
- **Missing core features** (e.g. viewer/visualisation parity, collision detection) losing deals and mindshare
- **Competitive pressure intensifying** - CoLab winning customers with AI Engineering Review, faster iteration cycles

**Outlook for 2026:**
**We must shift from platform capability to customer outcomes.** Prioritize closing the 10 critical product gaps—starting with onboarding/integration friction and core viewer features — to convert fragile platform potential into defensible market position.

---

## 2. Product Vision & Strategic Lens

### Vision

**The Future of Spatial Data**

We believe that spatial data will be the key enabler and accelerator for the fusion of industrial technology with human experience.

### Mission

**Redefining Industrial Workflows**

We create foundational technology to enable integrated spatial twins that interweave data and realities to blur the boundaries between digital and physical spaces and overcome information locality for the industrial workers of the future.


### Strategic Pillars

Our product strategy rests on three outcome-focused themes that align with how our buyers (Industrial Innovation Leaders), End Users (Engineers), Integrators (operating and integrating instant3Dhub into IT Landscape) and Developers (using our APIs) evaluate success:

TBD

---

### Our Go-to-Market Approach

TBD

### Target Users / Target Workflows

**Primary Decision Makers (ICP):**
- **Title:** Head of Digital Transformation / CTO / Director of Engineering IT
- **Organization:** Mid to large-sized enterprises (2,000+ employees) in Manufacturing, Automotive, Machinery, Industrial sectors
- **Geography:** Europe (primary), expanding internationally
- **Mindset:** Visionary but pragmatic—drives innovation but demands proven ROI and integration feasibility. Data-driven, acts as change agent, risk-conscious but open to technology with strong business case.

**Key Goals:**
- Drive digital transformation and Industry 4.0 initiatives
- Modernize legacy PLM/CAD workflows with web-based, collaborative tools
- Enable cross-functional collaboration (Engineering, Sales, Manufacturing, Customer Success)
- Reduce time-to-market and improve product development cycles
- Demonstrate measurable ROI on technology investments

**Pain Points:**
- Stuck with legacy 3D tools (desktop-only, poor collaboration, limited integration)
- Engineering data locked in silos, inaccessible to non-technical teams
- High costs and complexity of existing 3D visualization solutions
- Lack of web-based 3D tools that integrate with existing enterprise systems (PLM, ERP, Customer Relationship Management (CRM))
- Resistance to change from engineering teams familiar with legacy tools

**The Three Personas Using instant3Dhub:**

**1. Integrators / Operators (IT Admins, DevOps Engineers)**
- Deploy and operate instant3Dhub infrastructure
- Integrate with existing enterprise systems (PLM, ERP, Active Workspace, Teamcenter)
- Manage authentication (SSO, OAuth), databases, storage, scaling
- Responsible for: Installation, updates, performance, reliability, security

**2. Developers (Frontend Developers, Application Developers)**
- Build applications using instant3Dhub APIs and SDKs
- Create custom 3D viewers, dashboards, and workflows
- Integrate instant3Dhub into existing B2B SaaS products or internal tools
- Responsible for: API integration, custom UI development, feature implementation

**3. End Users (Engineers, Designers, Manufacturing Teams, Sales, CS)**
- Use applications built on instant3Dhub for daily work
- Conduct engineering reviews, design collaboration, visualization
- Experience the performance, rendering quality, and application UX
- Responsible for: Design decisions, engineering validation, collaboration

**Core Workflows We Must Nail (By Persona):**

**For Integrators/Operators:**
1. **Deploy instant3Dhub to production infrastructure**
   Current: Helm chart "most challenging," database corruptions, unclear Azure setup (Daimler Truck)
   Target: One-click or fully-documented enterprise deployment with robust defaults

2. **Integrate with PLM/ERP systems**
   Current: Weeks-to-months with significant friction (Bosch, Grimme, Porsche all cited difficulties)
   Target: Days with clear documentation, pre-built connectors, and validation tools

**For Developers:**
3. **New project setup → first 3D scene rendering**
   Current: 2-4 hours of trial-and-error (per Daimler Truck feedback)
   Target: <30 minutes with clear quick-start guides and working examples

**For End Users:**
4. **Visualize complex CAD assemblies accurately**
   Current: Missing colors, flexible parts issues, PMI problems (multiple customers)
   Target: True-to-source visualization out-of-box that engineers can trust for decisions

### What "Success" Looks Like Long-Term

**Success in 2027-2028:**
- **Spatial twins are standard in industrial workflows:** Manufacturing, engineering, and design teams rely on integrated spatial data as naturally as they use email or CAD today
- **instant3Dhub powers the digital-physical fusion:** Our platform is the foundational technology enabling seamless integration of spatial data across industrial ecosystems
- **Industrial workers access data contextually:** Information locality is overcome—workers interact with relevant spatial data wherever they are, without barriers between digital and physical spaces
- **Ecosystem adoption:** 5K+ developers and industrial solution providers building on instant3Dhub to create spatial twin applications
- **Market position:** Recognized as the enabling platform for spatial data integration in industrial contexts ("the platform for spatial twins")
- **Customer satisfaction:** Developer Net Promoter Score (NPS) consistently above 60, reflecting ease of building spatial twin solutions on our platform

---

## 3. High-Level Metrics Snapshot

*Quantitative health of the product in Q4 2025.*

**This is the first time we are formally introducing a metrics framework for instant3Dhub across the organization.** These four metrics will serve as our primary indicators of product health, customer engagement, and strategic progress going forward.

### Our Product Metrics Framework

We've selected metrics that align with our strategic priorities and provide actionable insights:

1. **Unique Sessions per Month** → Measures overall platform usage and growth trajectory
2. **Feature Adoption Rate (FAR)** → Reveals which features resonate with users and drive value (Coming Q1 2026)
3. **Active Customer Accounts** → Tracks our customer base health and growth
4. **Developer Documentation Engagement** → Proxy metric for API adoption and developer ecosystem health

These metrics are **outcome-focused**: they tell us whether customers are actively using instant3Dhub and which capabilities matter most to them. This visibility is critical for making informed product, sales, and customer success decisions.

**Important caveats as we establish this framework:**

⚠️ **Baseline Period:** Q4 2024 and 2025 data serve as our baseline. Expect refinements to methodology and data collection as we mature our instrumentation.

⚠️ **Coverage Gaps:** Current data excludes some customer contracts (e.g., Mercedes Benz on separate licensing structure) and has occasional tracking gaps. **Reported usage is understated**—true usage likely 10-15% higher than shown.

⚠️ **No Per-Customer Segmentation (Yet):** We aggregate all sessions but don't yet break down by individual customer, use case, or user cohort. This masks important signals (e.g., one customer driving 80% of sessions while others decline). Per-customer dashboards planned for 2026.

---

### Metric 1: Unique Sessions per Month

**What It Measures:** Total unique user sessions across all customers where the session lasted at least 120 seconds and included feature usage (meaningful engagement, not just page loads).

**Q4 2025 Data:**

| Month | Unique Sessions | Trend |
|-------|----------------|-------|
| **Q4 2024 Baseline** | | |
| Oct 2024 | 106K | - |
| Nov 2024 | 103K | 📉 -3% |
| Dec 2024 | 62.1K | 📉 -40% (holiday) |
| **Q4 2024 Avg** | **~90K** | |
| | | |
| **2025 Performance** | | |
| Jan 2025 | 98.4K | 📈 +58% (recovery) |
| Feb 2025 | 112K | 📈 +14% |
| Mar 2025 | 119K | 📈 +6% |
| **Q1 2025 Avg** | **109.8K** | 📈 +21% vs Q4 2024 |
| Apr 2025 | 107K | 📉 -10% |
| May 2025 | 114K | 📈 +7% |
| Jun 2025 | 106K | 📉 -7% |
| **Q2 2025 Avg** | **109K** | → Flat vs Q1 |
| Jul 2025 | 137K | 📈 +29% **(PEAK)** |
| Aug 2025 | 101K | 📉 -26% |
| Sep 2025 | 120K | 📈 +19% |
| **Q3 2025 Avg** | **119.3K** | 📈 +9% vs Q2 |
| | | |
| **2025 Avg (Jan-Sep)** | **~111K/month** | 📈 +23% vs Q4 2024 |

**Interpretation:**

instant3Dhub demonstrates **resilient growth in 2025**, with sessions averaging 111K/month (+23% vs Q4 2024). The platform sustained usage around 110-120K sessions/month with a peak of 137K in July, coming from around 10 accounts with Mercedes Benz, BMW, and Daimler Trucks NA contributing most of the usage.

**Key Insights:**
- **Platform usage is growing:** Unique Sessions grew from ~90K/month (Q4 2024) to ~111K/month average in 2025, showing existing customers increasing their usage (deeper adoption)
- **"Sticky when adopted" quality:** Sustained engagement demonstrates platform delivers ongoing value
- **Seasonal patterns visible:** December holiday drop, July peak aligns with industrial project cycles

**Strategic Implications:**
- ✅ **Strength:** Platform demonstrates value retention—customers who adopt continue using
- ⚠️ **Challenge:** Growth is from existing customer expansion, not new customer acquisition (see Active Customer Accounts)
- 🎯 **2026 Focus:** Maintain engagement within existing accounts while addressing onboarding gaps to grow customer base

---

### Metric 2: Feature Adoption Rate (FAR)

**What It Measures:** For each feature, the percentage of unique sessions that included at least one usage ping containing that feature. High FAR (>40%) = widely adopted; Medium (15-40%) = subset usage; Low (<15%) = underutilized or not relevant.

**Q4 2025 Status:** Implementation in Progress 🟡

Feature Adoption Rate tracking is being implemented in Q1 2026. This metric will reveal which features drive value and which are underutilized, enabling data-driven roadmap decisions.



**2026 Priority:** Establish FAR baseline in Q1, use Q2 data to inform H2 2026 roadmap decisions.

---

### Metric 3: Active Customer Accounts

**What It Measures:** Number of customers with active production instances generating sessions. Tracks customer base health—growth indicates successful onboarding, flat/declining signals churn or stalled pipeline.

**Q4 2025 Data:**

**Current: 10 active accounts**

This includes enterprise customers and partners. Note: Some partners are scheduled for offboarding in 2026 as we sharpen our focus on enterprise use cases.

**Interpretation:**

10 active accounts in Q4 2025 reflects **stable retention but limited new customer acquisition**. Combined with usage growth (+23%), this reveals:

**Key Insights:**
- **Good news:** Existing customers are expanding usage (land-and-expand working within accounts)
- **Challenge:** Sales pipeline needs acceleration to grow beyond current base
- **Pattern:** Growth is "deepening" (more usage per customer) rather than "widening" (more customers)

**Strategic Implications:**
- ✅ **Strength:** High retention—customers who onboard stay and expand
- ⚠️ **Critical gap:** Onboarding/deployment friction blocking new customer acquisition (Gap 5.1)
- 🎯 **2026 Focus:** Address deployment complexity to unlock sales pipeline and double customer base

**Bottom Line:** Platform demonstrates value for customers who successfully onboard. The barrier is *getting* customers onboarded, not keeping them engaged post-onboarding.


### Metric 4: Developer Documentation Portal Engagement

**What It Measures:** Documentation portal traffic as a proxy metric for API adoption and developer ecosystem health. Higher engagement indicates active development on instant3Dhub APIs; low engagement suggests limited expansion within customer developer teams.

**Q4 2025 Data (Nov 10 - Dec 9, 2025):**

| Metric | Value | Interpretation |
|--------|-------|----------------|
| **Daily Unique Visitors** | 10-27 per day (avg ~12/day) | Low volume, consistent |
| **Total Visits (30 days)** | ~450 visits | Small, stable developer base |
| **Actions per Visit** | 2-10 actions average | Shallow engagement |
| **Bounce Rate (New Visitors)** | 33-100% | Many leave after one page |

**Geographic Patterns:**

| Location | Likely Customer |
|----------|----------------|
| **Stuttgart area (Germany)** | Mercedes Benz development teams |
| **Portugal (Porto, Lisboa)** | BMW development team |

**Interpretation:**

Documentation engagement reveals a **maintenance mode, not growth mode** pattern. Same customer teams (Mercedes, BMW) access docs repeatedly, but we're not seeing:
- New developers joining from existing customers → no expansion within accounts
- New customers exploring docs → limited pipeline exploration
- Month-over-month growth → stagnant developer ecosystem

**Key Insights:**
- **Documentation as leading indicator:** Low docs traffic = Low API development activity = Limited platform usage expansion
- **Small core teams:** Developer engagement confined to 2-5 developers per customer based on visitor patterns
- **No use case expansion:** Customers aren't building new applications or expanding integrations (aligns with Hella's rollout challenges in Theme 4.2-4.3)

**Strategic Implications:**
- ✅ **Do:** Keep docs running and up to date (critical for existing Mercedes/BMW teams)
- ⚠️ **Don't:** Over-invest in documentation expansion until underlying product gaps (Gap 5.3: docs quality, Gap 5.2: missing features) are addressed
- 🎯 **2026 Focus:** Growing documentation engagement should be a key metric for developer ecosystem health. First address doc quality issues (Gap 5.3), then drive more developers to the site as indicator of actual API usage growth

**Target State:** If documentation and developer experience were strong, we'd expect growing unique visitors month-over-month (new developers discovering platform) and expanding geographic diversity (new customers exploring).

---

## 4. Customer Insights & Feedback Themes

*What we're hearing from comprehensive Internal and Customer Advisory Board sessions (Sales, Presales, Customer Success, Professional Services, VP Sales, Key Accounts + Porsche, Daimler Truck external customers).*

### 4.1 Theme: Integration & Deployment Complexity Blocking Onboarding
*Affects: Integrators/Operators (IT Admins, DevOps Engineers)*

**What Integrators/Operators Say:**

Setting up and deploying instant3Dhub is **too difficult, too time-consuming, and too error-prone**. IT teams are dependent on Threedy for installation, creating bottlenecks. PLM integrations (especially Teamcenter) take months and still fail. Enterprise deployment requirements (Azure, external databases, Single Sign-On (SSO)) are not well-supported, causing project delays and customer dissatisfaction.

**Evidence:**

**Internal Stakeholders:**
- **Sales (Aron, Andreas):** *"Installation processes for Bosch and Grimme are not proceeding as planned, resulting in customer dissatisfaction and delays. Customers are dependent on Threedy for installation, leading to bottlenecks."*
- **Professional Services (Hafedh):** *"Longstanding struggles with integrating PLM/XML data from customers, especially for Teamcenter...Projects extend well beyond budgets and schedules (e.g., Grimmer project still unresolved after multiple attempts and months overdue)."*
- **Customer Success (Hazem):** *"PLM Integration Uncertainty: Difficulty setting customer expectations for what PLM XML structures are supported...Documentation and validation tools are lacking, leading to recurring implementation problems."*
- **Presales (Sascha):** *"Our current presentation in this area [Teamcenter/Windchill connectors] is lacking, leading to a lack of customer confidence that has possibly cost us customers in the past."*
- **Key Account (Bernd):** *"The top issues...not having something like a package solution...and the other one was the deployment time, an installer."*

**External Customers:**
- **Porsche (Vinci):** *"Teamcenter integration: Direct, live integration into Teamcenter ('Active Workspace' etc.) is difficult due to technical hurdles, reliance on intermediary tools, and budget/time constraints."*
- **Hella:** *"It's still challenging to smoothly weave the 3D Viewer into our current system landscape (especially LPDS, Teamcenter, and other PLM tools). Each integration is work-intensive—uniform, robust connectors and reusable code are key gaps for us."* Additionally: *"Frequent product updates or changes in upstream CAD tools can break our integrations. Each update often triggers significant retesting and rework—with thousands of engineering hours lost in worst-case scenarios."*
- **Daimler Truck (Kyle):** *"I've deployed like 10 different Helm charts for various software, and instant3Dhub's is **the most challenging**. Standard expectations (like easily passing a Postgres connection string, auto-creating required DB tables, resizing storage) are not met."*
- **Daimler Truck:** *"PostgreSQL has corrupted itself 2 or 3 times...storage volumes that wouldn't auto-expand caused service outages."*
- **Daimler Truck:** *"The OAuth2 proxy setup for Single Sign-On is insufficient for our Microsoft identity integration, yet updating it is risky due to major chart changes."*

**Why It Matters:**

This is the **#1 barrier to customer acquisition and time-to-value**. Every delayed installation (Bosch, Grimme, Daimler) represents:
- Revenue at risk (stalled onboarding → delayed go-live → churn risk)
- Competitive disadvantage (Daimler compared us unfavorably to "Windmill" which deploys in minutes)
- Resource drain (Customer Success/PS spending unbillable hours firefighting deployments)
- Brand damage (Daimler: *"Lack of customer confidence that has possibly cost us customers"*)

**Business Impact:**
- Multiple deals delayed or at risk (Bosch, Grimme confirmed)
- Lost competitive opportunities (customers evaluate alternatives during long deployments)
- High cost of customer acquisition (CS/PS time not billable)
- Renewals at risk when onboarding experience is poor

---

### 4.2 Theme: Native CAD Data Fidelity Issues → Visualization Not Trusted
*Foundation Layer: If End Users can't trust what they see, nothing else matters*
*Affects: End Users (Engineers, Designers) + PS/CS Teams*

**What End Users & Support Teams Say:**

Incomplete support for CAD format features (flexible components, color overrides, sub-assembly details, PMI structure) causes **inaccurate or incomplete visualizations**. Colors defined in assemblies don't appear, parts render gray by default, hierarchical structures are lost in linked JT files, and PMI presentation doesn't match industry standards (JT2Go). **Result: End Users (engineers) can't trust the visual output for engineering decisions, leading to rework, project delays, and lost credibility.**

**Evidence:**

**Internal Stakeholder:**
- **Professional Services (Hafedh):** *"When you defined the color of your part in the assembly file...it was not there on our side. From our side, everything is visualized gray."*
- **Professional Services (Hafedh):** *"Some features that they use in their data, which we don't support...it's still there [causing issues]."*
- **Presales (Timo, Pasqual):** *"PMI Structure Not Standard/Not 'Schön' (User-Friendly): The way PMIs are handled and visualized is not consistent with industry standards (e.g., JT2Go)."*
- **Presales:** *"Loss of Hierarchical Structure When Baking Linked JT Files: At Bosch, they convert linked JT files into a single monolithic JT. In this process, the original relationships between different JT nodes are lost."*

**External Customer:**
- **Porsche (Vinci):** *"Struggles with incomplete support for CAD format features like flexible components, coloring overrides, and sub-assembly details. This impacts the fidelity and reliability of the visualization seen by clients."*
- **Professional Services (Hafedh):** *"Persistent issues with loading and visualizing 3D data—such as missing or incorrect colors, slow load times for certain file types, and general data fidelity/quality concerns."*

**Why It Matters:**

**If the visualization doesn't match the source CAD, it's not usable for engineering decisions.** Customers in automotive and machinery rely on accurate 3D representations for design reviews, engineering changes, and manufacturing planning. Inaccurate visuals → rework → delays → loss of trust.

**More critically: Data fidelity issues block customer expansion and rollout.** Hella's feedback is telling: they can't onboard new users at scale until visualization reliability improves. This pattern likely affects other customers—successful pilots can't expand to production rollouts because end users don't trust the output. **The gap between "pilot success" and "production adoption" is often data fidelity.**

**This is the foundation problem that Professional Services and Customer Success struggle with constantly.** When CAD data doesn't render correctly, PS/CS teams spend unbillable time troubleshooting why visualizations look wrong, explaining limitations to frustrated customers, and working around data quality issues instead of delivering value.

**Business Impact:**
- **Expansion blocker:** Hella can't rollout to broader user base → pilot stays pilot, revenue expansion stalled
- Project delays (Bosch, Grimme explicitly mentioned)
- PS/CS resource drain on data quality troubleshooting (unbillable hours)
- Customer dissatisfaction and escalations
- Credibility damage (if engineers can't trust the output, they won't use the tool)
- Competitive disadvantage (industry-standard tools like JT2Go set baseline expectations)
- **Land-and-expand failure:** Successful pilots can't scale to production adoption when end users don't trust visualizations

---

### 4.3 Theme: Missing Core Viewer Features → End Users Stick With Legacy Tools
*Interaction Layer: Even if data is perfect, the viewer lacks basic functionality to replace legacy tools*
*Affects: End Users (Engineers, Designers) Using Applications*

**What End Users Say:**

instant3Dhub **lacks essential viewer functionality** that End Users expect from legacy 3D tools (VisMockup, TCViz, Siemens tools). End Users can't perform basic tasks like moving parts with constraints, setting custom rotation centers, using grids/planes for measurements, or viewing models side-by-side. The default UI is minimal (1-2 buttons) and **requires heavy SDK customization to add features that should be built-in**. **Result: End Users prefer legacy tools out of habit**, even if slower, because they offer richer out-of-box functionality.

**The Compounding Problem:** Even when we solve the data fidelity issues (Theme 4.2), End Users still can't switch from legacy tools because the effort required to customize instant3Dhub to match basic legacy tool functionality is too large. Companies expect these features out-of-box, not as custom development projects.

**Evidence:**

**Internal Stakeholders:**
- **Customer Success (Timm):** *"Selling a platform and always losing out against apps."* - Customers expect packaged, feature-rich applications, not minimal viewers requiring extensive customization
- **VP Sales (Marcus):** *"Produktansprache statt 'Lösungs'-Spektrum"* (Product messaging, not solution spectrum) - Customers want concrete, feature-complete solutions, not flexible but bare-bones platforms
- **Presales (Sascha, Timo):** Customers evaluate instant3Dhub against mature legacy tools with decades of accumulated features. When basic functionality (grids, measurements, part manipulation) requires custom development, customers question the value proposition


**External Customer:**
- **Daimler Truck (Daniel, Kyle):** *"Many users still prefer the older Siemens/TC VisMockup tool simply because they are 'used to the UI,' even if it means waiting longer for models to load."*
- **Daimler Truck:** *"In VisMockup, users have handy functions: move parts with incremental snaps, use grid overlays for scaling in photos, set custom rotation points, open two models side-by-side with synced cameras. instant3Dhub is **more limited** in these areas, requiring workarounds or not possible at all."*
- **Daimler Truck:** *"Unit settings default to meters (inconsistent with CAD units), you can't set custom rotation centers, and grid/plane tools are not readily available out-of-the-box."*
- **Daimler Truck (Kyle):** *"The default instant3Dhub UI is very minimal ('only one or two extra buttons') and does not provide rich functionality unless custom-developed."*
- **Daimler Truck:** *"Adding more built-in features through the Software Development Kit (SDK) would make the product **far more competitive and valuable**."*
- **Hella:** Feature gaps are part of the barrier to broader user rollout. End Users accustomed to legacy tools expect out-of-box functionality. Specific issues: *"We can't easily control which geometry data is visible (e.g., toggling hidden/invisible elements, filtering layers, or showing only relevant parts). That means extra manual steps, which slows us down and causes confusion."* Additionally: *"While flexible, building custom apps or adapting for new user groups requires too much engineering effort. We need more templates, app building blocks, and an easier developer experience."*

**Why It Matters:**

**Lack of feature parity with incumbents is a major adoption blocker.** End Users evaluate tools based on "Can I do my job as well or better than before?" When the answer is "No, I have to work around missing features or wait for custom dev," End Users abandon the new tool.

**The "Platform vs. App" Trap:** We position instant3Dhub as a flexible platform, but customers evaluate it as a feature-complete application replacement. When they compare our default UI to legacy tools with rich out-of-box functionality, we lose—even if our underlying platform capabilities are superior. As Timm noted: customers aren't buying platforms, they're buying apps.

**Business Impact:**
- **Adoption fragility:** Daimler Truck usage *"dropped off quite a bit"* after introducing licensing—only 1-2 End Users paid, indicating weak perceived value
- **Expansion blocker:** Hella and others can't rollout broadly when End Users find tool lacking vs. familiar legacy alternatives
- **Lost productivity claims:** Can't sell instant3Dhub on "faster workflows" if basic tasks are harder than legacy tools
- **Competitive vulnerability:** End Users compare us to established tools and find us lacking, reducing win rates
- **"Selling platform, losing to apps":** Sales team consistently loses deals because customers want solutions, not minimal viewers requiring custom development on their side

---

### 4.4 Theme: Collision/Clash Detection Repeatedly Requested, Missing
*Advanced Feature Layer: Missing high-value features that require API and infrastructure changes*
*Affects: End Users (Engineers) Performing Design Validation*

**What End Users Say:**

End Users **consistently request automatic collision detection and clash checks** for engineering reviews. This is critical for design validation (e.g., does this component interfere with others?), assembly planning, and AI-assisted design checks. **Absence of this feature has influenced past project outcomes** and is a recurring pain point across multiple customers (Innio, Claas VR, ÖBB).

**The Strategic Challenge:** Unlike the feature parity issues in Theme 4.3 (which could be addressed through UI/SDK enhancements), collision detection is one of several requested features that requires **deep changes across application, API, and infrastructure layers**. This isn't about customization being too heavy—it's about capabilities that don't exist in the platform at all.

**Evidence:**

**Internal Stakeholder:**
- **Sales (Aron, Andreas, Athanasios):** *"Customer Innio wants AI-based design checks, such as automatic collision alerts and learning from usage, for engineering reviews in instant3Dhub."*
- **Sales:** *"Collision checks also a topic in the past with Claas in VR, also ongoing topic in ÖBB."*
- **Sales:** *"Collision checks are a **recurring customer need and have influenced past project outcomes**; should be considered a key feature."*

**Why It Matters:**

**Engineering Review is the top use case** (per VP Sales), and CoLab is winning in this space. Collision detection is a **table-stakes feature** for engineering review workflows. Without it, we can't compete effectively in our core market.

**Business Impact:**
- Lost deals (Innio explicitly requested, likely not unique)
- Competitive disadvantage vs. CoLab (which offers AI-assisted review)
- Misalignment with stated strategic focus (Engineering Review as killer use case)

---

### 4.5 Theme: Documentation & Developer Self-Service Gaps → High Support Overhead
*Affects: Developers (Frontend Developers, Application Developers) Building with APIs*

**What Developers Say:**

Application Programming Interface (API) documentation is **confusing, incomplete, and lacks practical examples**. Developers spend significant time (5-60 minutes per task, per Daimler) figuring out which APIs to use through trial-and-error. Query API is particularly problematic—Developers regularly ask support for help despite docs being available. BRIX entry point is too technical (repo access), limiting accessibility. **Result: Developers can't self-serve, support overhead remains high, time-to-value is slow.**

**Evidence:**

**Internal Stakeholders:**
- **Professional Services (Sudharsan):** *"The API documentation structure is confusing—hard to find which interfaces or APIs to use for certain functionalities (e.g., introducing a Gizmo), requiring a lot of manual searching."*
- **Professional Services (Hafedh):** *"Customers find documentation hard to use independently, especially for the query API. Even after being provided with documentation links, they regularly reach out with questions, causing support overhead and friction."*
- **Presales (Sascha - on BRIX):** *"The entry point is still technical (repo access), and there's a desire for more accessible onboarding materials."*

**External Customer:**
- **Daimler Truck (Kyle):** *"The API documentation...it kind of almost feels like an **automated dump of all the endpoints** with not enough usage examples. Important details like enumerations and clear descriptions are missing."*
- **Daimler Truck:** *"Better docs could save them **5–60 minutes here and there** in development."*
- **Hella:** *"The tool isn't yet intuitive for our wider user base. If a user can't figure out how to take measurements or use basic features immediately—without deep CAD knowledge—they quickly give up. The learning curve remains too steep for non-engineers."* Additionally: *"We face resistance when rolling out to 1,500+ users. If it takes more than a few minutes of training, adoption drops sharply. Current training materials and in-app guidance need major refinement for us to scale effectively."*

**Why It Matters:**

**Developer experience is product quality.** When developers can't quickly understand how to use the platform, three things happen:
1. **Time-to-value extends** (slower integration → delayed Return on Investment (ROI))
2. **Support burden increases** (questions that should be self-served consume Customer Success (CS) / Professional Services (PS) time)
3. **Developer satisfaction drops** (frustration with trial-and-error reduces advocacy)

Daimler Truck explicitly noted this: docs improvements have *"direct ROI in customer enablement and satisfaction."*

**Business Impact:**
- PS/CS unbillable time answering doc-related questions (Hafedh: *"support overhead and friction"*)
- Slower customer onboarding (every 30-60 min delay per task compounds)
- Developer churn risk (frustrated developers look for alternatives)
- BRIX adoption limited by technical entry barrier

---

### 4.6 Theme: Product Stability Concerns at Scale → Trust Undermined
*Affects: All Personas (Integrators/Operators managing infrastructure, Developers using APIs, End Users experiencing performance)*

**What We're Hearing:**

Database crashes with large datasets, fragment addressing workarounds that have persisted for years, Graphics Processing Unit (GPU) driver bugs causing severe performance drops, and QueryAPI/SpaceAPI/MemberAPI stability concerns undermine confidence in the platform's **enterprise readiness**. Customers have experienced multiple PostgreSQL corruptions (impacting Integrators/Operators), escalation meetings over longstanding issues, and unpredictable performance with "huge assets" (impacting End Users).

**Evidence:**

**Internal Stakeholders:**
- **Presales (Timo):** *"Concerns about database and crash scenarios with large datasets. For customers, crashes strongly undermine perceived stability."*
- **Presales (Sascha):** *"Fragment Addressing...dass dieser workaround 2 Jahre bestehen muss, ist eigentlich...Armutszeugnis...Wir sind bei der dritten Jahreslizenz...Das findet auch Daimler Trucks übrigens nicht geil. Haben wir auch schon mehrere Eskalationsmeetings diesbezüglich gehabt, hat aber alles nichts gelöst."* (Translation: "That this workaround must exist for 2 years is...a disgrace. We're in the third annual license. Daimler Trucks also doesn't find this cool. We've had multiple escalation meetings about this, but nothing has been solved.")
- **Presales (Sascha, Timo):** *"Graphics Processing Unit (GPU) Utilization: Long-standing bug: GPU services sometimes run on software drivers, causing severe performance drops."*
- **Presales (Timo):** *"Timo underlines the need for ongoing investment into Product Stability in topics such as QueryAPI, SpaceAPI, and MemberAPI."*

**External Customer:**
- **Porsche:** *"Performance issues using large/full vehicle models...only sub-assemblies are used, which slows workflows."*
- **Daimler Truck (Kyle):** *"PostgreSQL has **corrupted itself 2 or 3 times**...These incidents required significant troubleshooting."*
- **Daimler Truck:** *"Storage volumes that wouldn't auto-expand caused service outages."*
- **Daimler Truck:** Query filtering *"took over a minute for one truck."*

**Why It Matters:**

**Enterprise customers require predictable, reliable performance.** When systems crash, data corrupts, or performance degrades unpredictably:
- **Trust erodes** (Daimler: multiple escalation meetings)
- **Operational risk increases** (customers fear downtime in production)
- **Renewals at risk** (2+ years of unfixed issues signal lack of commitment)

Porsche's constraint that they can "only use sub-assemblies, not full vehicle models" due to performance issues directly limits the product's value proposition.

**Business Impact:**
- Customer escalations and churn risk (Daimler fragment addressing issue)
- Limited use cases (Porsche can't use full models)
- Competitive disadvantage (reliability is a core strategic pillar we're not consistently delivering)

---

### 4.7 Theme: Roles & Permissions Too Generic → Blocks External Collaboration
*Affects: Integrators/Operators (configuring access controls) + All Personas (limited by generic permissions)*

**What We're Hearing:**

Current role management in 3DSpaces is **too basic ("sticker" roles with no backend logic)** and lacks fine-grained access control needed for external collaborators, offshore teams, or customer-facing scenarios. Integrators/Operators can't configure granular access controls, can't create robust reusable roles for package solutions, and lack proper Role-Based Access Control (RBAC) to meet enterprise security requirements.

**Evidence:**

**Internal Stakeholder:**
- **Customer Success (Timm):** *"Roles and Permissions in 3DSpaces: Urgent need for more robust permission concepts in 3DSpaces as part of package solutions, noting current functionality is too generic ('sticker' roles with no backend logic)."*
- **Customer Success (Timm):** *"He raised the question of when/if robust, reusable role management will be productized so it can be sold as an off-the-shelf module ('customers want to buy features, not infrastructure')."*

**External Customers:**
- **Porsche:** *"There isn't an easy, fine-grained way to control who can access/view sensitive assemblies—especially important for external/offshore contributors. Current role management is basic."*
- **Daimler Truck (Kyle):** *"Lack of robust role-based access control (RBAC) in the app...getting proper RBAC 'figured out' as a **major unsolved issue**."*
- **Daimler Truck:** *"Current OAuth2 proxy setup for Single Sign-On is insufficient for our Microsoft identity integration."*

**Why It Matters:**

**Without proper RBAC, the product is limited to internal-only use cases.** Many high-value scenarios require external collaboration:
- Sharing designs with suppliers (Porsche use case)
- Customer-facing configurators or reviews (Daimler considering but can't due to security)
- Offshore team access with limited permissions

**Business Impact:**
- **Limits addressable use cases** (can't expand to customer-facing or supplier collaboration scenarios)
- **Blocks packaged solutions** (Timm: *"customers want to buy features,"* but we can't sell if permissions aren't robust)
- **Security concerns delay deals** (enterprise IT won't approve without proper access controls)

---

## 5. Top Product Gaps

*The gaps that most limit adoption, retention, and expansion—prioritized by business impact and strategic alignment.*

### Overview: The 7 Critical Product Gaps

Based on comprehensive Internal and Customer Advisory Board feedback, we've identified 7 prioritized product gaps that are blocking growth in 2026. These gaps cluster into three categories: **Onboarding & Integration** (getting customers live), **Core Product Quality** (trust and feature parity), and **Enterprise Readiness** (scale and security).

| # | Gap | Personas Affected | Priority | Impact |
|---|-----|-------------------|----------|--------|
| **5.1** | **Integration & Deployment Complexity** | Integrators/Operators | 🔴 **HIGH** | Blocks every new customer onboarding, delays revenue, competitive disadvantage |
| **5.2** | **Missing Core Viewer Features** | End Users (Engineers, Designers) | 🔴 **HIGH** | End Users stick with legacy tools, fragile adoption, lost productivity claims |
| **5.3** | **Documentation & Developer Self-Service** | Developers | 🔴 **HIGH** | Extended time-to-value, support overhead, BRIX ecosystem blocker |
| **5.4** | **Native CAD Data Fidelity & Quality** | End Users (Engineers, Designers) | 🔴 **HIGH** | Trust erosion, can't use for critical engineering decisions, expansion blocked |
| **5.5** | **Collision/Clash Detection** | End Users (Engineers) | 🟡 **MEDIUM** | Lost deals, competitive gap vs. CoLab, misaligned with Engineering Review focus |
| **5.6** | **Product Stability at Enterprise Scale** | All Personas | 🟡 **MEDIUM** | Churn risk, operational fear, use case limitations (Porsche can't use full models) |
| **5.7** | **Roles & Permissions System** | Integrators/Operators | 🟡 **MEDIUM** | Limits external collaboration use cases, blocks packaged solutions |

**Pattern:** The four 🔴 **HIGH** priority gaps (5.1-5.4) represent **table-stakes capabilities** that customers expect but we're not consistently delivering. These block adoption, trust, and expansion. The three 🟡 **MEDIUM** priority gaps (5.5-5.7) represent **competitive differentiators and enterprise requirements** that limit our addressable market and use case expansion.

**2026 Imperative:** Address all four HIGH priority gaps to convert fragile platform potential into defensible market position. Start with Gap 5.1 (Integration & Deployment) as it affects every new customer.

---

### 5.1 Gap: Integration & Deployment Complexity

**Definition:**

Installing, configuring, and deploying instant3Dhub is too difficult for customers to do independently. Helm charts are overly complex, Azure/cloud-specific guidance is lacking, external database support is incomplete, PLM connectors (especially Teamcenter) require months of troubleshooting, and SSO/auth integration is brittle. Customers are dependent on Threedy for installations, creating resource bottlenecks and project delays.

**Evidence:**

- **Bosch & Grimme installations delayed** (Sales IPAB)
- **Teamcenter integration "months overdue"** for Grimmer project (PS IPAB)
- **Daimler Truck:** Helm chart "most challenging" of 10 deployed, PostgreSQL corruptions 2-3x, no auto-expanding storage, OAuth2 proxy insufficient
- **Porsche:** Teamcenter integration "difficult due to technical hurdles"
- **Customer Success (Hazem):** *"PLM integration uncertainty...documentation and validation tools lacking"*
- **Key Account (Bernd):** *"Top issues: not having a package solution and deployment time/installer"*

**Impact:**

- **Who Is Affected:** Integrators/Operators (IT Admins, DevOps Engineers) at all new enterprise customers, especially those with Teamcenter/PLM environments or Azure/cloud deployments
- **Business Impact:**
  - **Revenue at risk:** Delayed go-lives (Bosch, Grimme) → delayed revenue recognition
  - **Churn risk:** Poor onboarding experience reduces renewal likelihood (Daimler frustration evident)
  - **Resource drain:** CS/PS spending unbillable time on installations instead of value-add work
  - **Competitive losses:** Daimler compared us unfavorably to "Windmill" which deploys in minutes
  - **Deal velocity:** Long deployment cycles slow sales pipeline conversion

**Priority:** 🔴 **HIGH**

**Rationale:**
- Affects **every new enterprise customer** (not niche)
- Directly impacts **time-to-value** (longer deployment = later ROI)
- **Competitive disadvantage** (Daimler explicitly compared us unfavorably)
- **Strategic misalignment:** "Developer Experience First" pillar requires easy onboarding; current state is opposite

**Notes / Dependencies:**
- Requires: Helm chart refactoring, Azure-specific deployment docs, external DB support (managed Postgres, etc.), storage auto-scaling, SSO/auth templates for common identity providers
- Could unlock: Self-service onboarding (reduces CS/PS load), faster sales cycles, better competitive positioning
- Related to: Documentation gap (deployment guides), PLM connector maturity

---

### 5.2 Gap: Missing Core Viewer Features (Feature Parity with Legacy Tools)

**Definition:**

instant3Dhub lacks essential viewer functionality that End Users expect from legacy 3D tools: incremental part movement with snapping/constraints, custom rotation centers, grid/plane overlays for measurement, side-by-side model comparison with synced cameras, unit setting control (defaults to meters regardless of CAD units). Default UI is minimal (1-2 buttons) and requires heavy SDK customization to add basic features. End Users prefer legacy tools (VisMockup, TCViz) because they offer richer out-of-box functionality.

**Evidence:**

- **Daimler Truck (extensive feedback):**
  - *"Users still prefer the older Siemens/TC VisMockup tool simply because they are 'used to the UI'"*
  - *"VisMockup has: move parts with incremental snaps, grid overlays for scaling, custom rotation points, side-by-side views with synced cameras. instant3Dhub is more limited...requiring workarounds or not possible at all."*
  - *"Unit settings default to meters (inconsistent with CAD units), can't set custom rotation centers, grid/plane tools not available out-of-box."*
  - *"Default UI very minimal ('only 1-2 extra buttons')...Adding more built-in features would make product far more competitive."*
- **Daimler Truck adoption drop:** Usage "dropped off quite a bit" after licensing introduced—only 1-2 users paid, indicating weak perceived value

**Impact:**

- **Who Is Affected:** End Users (Engineers, Designers) evaluating instant3Dhub vs. legacy tools they're accustomed to
- **Business Impact:**
  - **Adoption blocker:** End Users won't switch if new tool makes daily tasks harder
  - **Fragile value perception:** Daimler usage collapsed when fees introduced (perceived value < cost)
  - **Lost productivity claims:** Can't sell on "faster workflows" if basic tasks are missing/harder
  - **Competitive vulnerability:** Incumbents win on familiarity + feature richness

**Priority:** 🔴 **HIGH**

**Rationale:**
- **End User adoption is fragile** (Daimler proof point: fees killed usage)
- **Low switching cost back to legacy tools** if we don't provide equivalent value
- **Table-stakes features** for engineering workflows (grids, measurements, part movement are basics, not advanced)
- **Strategic alignment:** "Developer Experience First" means making common tasks easy; failing here undermines strategy

**Notes / Dependencies:**
- Requires: UI/UX work to expose features, SDK enhancements (if not core), measurement tool improvements, multi-view synchronization
- Quick wins possible: Grid overlays, unit settings, rotation center control are bounded features
- Related to: Developer platform richness, out-of-box value

---

### 5.3 Gap: Documentation & Developer Self-Service

**Definition:**

API documentation is confusing, incomplete, and lacks practical examples. Developers can't quickly find which APIs/interfaces to use for common tasks (e.g., adding a Gizmo, using Query API), requiring trial-and-error that costs 5-60 minutes per task. Query API documentation particularly problematic—customers regularly contact support despite docs existing. BRIX entry point too technical (repo access). Overall developer experience is friction-filled, extending time-to-value and increasing support burden.

**Evidence:**

- **PS (Sudharsan):** *"API documentation structure confusing—hard to find which interfaces or APIs to use, requiring a lot of manual searching."*
- **PS (Hafedh):** *"Customers find documentation hard to use independently, especially for Query API. Even after being provided with documentation links, they regularly reach out with questions, causing support overhead."*
- **Daimler Truck (Kyle):** *"API documentation...feels like an automated dump of all the endpoints with not enough usage examples. Important details like enumerations and clear descriptions are missing."*
- **Daimler Truck:** *"Better docs could save 5–60 minutes here and there in development."*
- **Presales (Sascha - BRIX):** *"Entry point still technical (repo access), desire for more accessible onboarding materials."*

**Impact:**

- **Who Is Affected:** Developers integrating instant3Dhub, customer IT teams building on platform, internal PS/CS teams supporting customers
- **Business Impact:**
  - **Extended time-to-value:** Every 30-60 min delay per task compounds across integration
  - **Support overhead:** PS/CS answering questions that should be self-served (unbillable time)
  - **Developer churn risk:** Frustrated developers look for alternatives (Daimler: competitor docs better)
  - **BRIX adoption limited:** Technical entry barrier prevents broader developer base from trying

**Priority:** 🔴 **HIGH**

**Rationale:**
- **Developer experience = product quality** (strategic pillar)
- **High ROI fix:** Better docs directly reduce support burden and speed customer enablement (Daimler: "direct ROI")
- **Competitive gap:** Daimler explicitly compared docs unfavorably to alternatives
- **Ecosystem blocker:** BRIX can't drive ecosystem growth if entry barrier is too high

**Notes / Dependencies:**
- Requires: Docs restructure (task-based, not endpoint-dump), code samples/tutorials, Query API deep-dive guide, BRIX onboarding flow (non-repo entry)
- Could unlock: Self-service integrations, lower CS/PS load, faster BRIX adoption
- Related to: Developer platform strategy, onboarding/integration complexity

---

### 5.4 Gap: Native CAD Data Fidelity & Quality

**Definition:**

Incomplete support for CAD format features (flexible components, color overrides, sub-assembly details, PMI structure, hierarchical relationships in linked JT files) causes inaccurate or incomplete visualizations. Colors defined in assemblies don't appear (everything gray by default), PMI presentation doesn't match industry standards (JT2Go), and hierarchical structure is lost when baking linked JTs. Result: customers can't trust the visual output for engineering decisions.

**Evidence:**

- **PS (Hafedh):** *"When you defined the color of your part in the assembly file...it was not there on our side. From our side, everything is visualized gray."*
- **PS (Hafedh):** *"Some features that they use in their data, which we don't support...it's still there [causing issues]."*
- **Presales (Timo, Pasqual):** *"PMI Structure Not Standard/Not 'Schön': The way PMIs are handled and visualized is not consistent with industry standards (e.g., JT2Go)."*
- **Presales:** *"Loss of Hierarchical Structure When Baking Linked JT Files at Bosch...original relationships between different JT nodes are lost."*
- **Porsche:** *"Incomplete support for CAD format features like flexible components, coloring overrides, and sub-assembly details impacts fidelity and reliability of visualization."*
- **PS (Hafedh):** *"Persistent issues with missing or incorrect colors, slow load times for certain file types, general data fidelity/quality concerns."*

**Impact:**

- **Who Is Affected:** End Users (Engineers, Designers) at all customers relying on accurate CAD visualization for engineering reviews, design decisions, manufacturing planning
- **Business Impact:**
  - **Project delays:** Bosch, Grimme cited; rework required when visualizations don't match source
  - **Trust erosion:** If End Users (Engineers) can't trust output, they won't use the tool
  - **Competitive disadvantage:** Industry-standard tools (JT2Go) set baseline; we fall short
  - **Use case limitations:** Can't confidently use for critical engineering decisions if accuracy questionable

**Priority:** 🔴 **HIGH**

**Rationale:**
- **Core value proposition at risk:** If visualizations aren't accurate, product loses primary utility
- **Customer dissatisfaction and escalations** (Bosch hierarchical structure issues)
- **Industry expectations:** Automotive/machinery customers compare to JT2Go, expect parity
- **Strategic alignment:** "Enterprise-Grade Reliability" requires data fidelity

**Notes / Dependencies:**
- Requires: CAD loader improvements, DataKit vendor coordination, PMI rendering overhaul, flexible parts support, hierarchical reference handling
- Related to: Data quality testing, loader performance

---

### 5.5 Gap: Collision/Clash Detection

**Definition:**

No automatic collision detection or clash checking capability for engineering reviews. Customers want AI-based design checks (e.g., "Does this component interfere with others?") for assembly validation, interference detection, and design optimization. This feature is critical for Engineering Review use case (identified as top market opportunity) and has been requested by multiple customers (Innio, Claas VR, ÖBB).

**Evidence:**

- **Sales (Aron, Andreas, Athanasios):** *"Customer Innio wants AI-based design checks, such as automatic collision alerts and learning from usage, for engineering reviews."*
- **Sales:** *"Collision checks also a topic in the past with Claas in VR, also ongoing topic in ÖBB."*
- **Sales:** *"Collision checks are a recurring customer need and have influenced past project outcomes; should be considered a key feature."*
- **VP Sales:** Engineering Review identified as "Killer-Thema" (killer use case) with "sehr hoher Bedarf im Markt" (very high market demand)

**Impact:**

- **Who Is Affected:** End Users (Engineers) in automotive, machinery, manufacturing doing design reviews and assembly planning
- **Business Impact:**
  - **Lost deals:** Innio explicitly requested (likely not unique)
  - **Competitive disadvantage:** CoLab winning with AI-assisted review features
  - **Misalignment with strategy:** VP Sales identified Engineering Review as top use case; we lack key feature for it

**Priority:** 🟡 **HIGH**

**Rationale:**
- **Recurring customer request** (3+ customers mentioned: Innio, Claas, ÖBB)
- **Has influenced past project outcomes** (Sales quote: lost opportunities)
- **Strategic importance:** Engineering Review is our target use case; this is table-stakes
- **Competitive gap:** CoLab offers AI-based review; we don't

**Notes / Dependencies:**
- Requires: Collision detection algorithm, UI for highlighting clashes, potentially AI/ML for learning patterns
- Could unlock: Engineering Review market segment, differentiation vs. CoLab
- Related to: AI roadmap, rendering capabilities

---

### 5.6 Gap: Product Stability at Enterprise Scale

**Definition:**

Database crashes with large datasets, multi-year unfixed issues (fragment addressing workaround), GPU driver bugs causing performance drops, QueryAPI/SpaceAPI/MemberAPI stability concerns, and lack of support for enterprise infrastructure (external managed databases, auto-scaling storage) undermine confidence in platform's enterprise readiness. Customers have experienced PostgreSQL corruptions, service outages, escalation meetings over longstanding bugs, and unpredictable performance with large assemblies.

**Evidence:**

- **Presales (Timo):** *"Database and crash scenarios with large datasets. For customers, crashes strongly undermine perceived stability."*
- **Presales (Sascha):** *"Fragment Addressing: workaround 2 Jahre bestehen muss, ist eigentlich...Armutszeugnis...Daimler Trucks...mehrere Eskalationsmeetings...hat aber alles nichts gelöst."* (2-year workaround is a disgrace, Daimler escalations, nothing solved)
- **Presales:** *"GPU Utilization bug: GPU services sometimes run on software drivers, causing severe performance drops."*
- **Daimler Truck (Kyle):** *"PostgreSQL has corrupted itself 2 or 3 times."*
- **Daimler Truck:** *"Storage volumes that wouldn't auto-expand caused service outages."*
- **Daimler Truck:** Query filtering *"took over a minute for one truck."*
- **Porsche:** *"Performance issues using large/full vehicle models...only sub-assemblies are used."*

**Impact:**

- **Who Is Affected:** All personas at enterprise customers with large datasets: Integrators/Operators (database/infrastructure stability), Developers (API stability), End Users (performance with large assemblies)
- **Business Impact:**
  - **Churn risk:** Multi-year unfixed issues (fragment addressing) → customer frustration, renewals at risk
  - **Limited use cases:** Porsche can't use full models, only sub-assemblies (reduces value)
  - **Operational risk:** Database corruptions, service outages create fear of production deployment
  - **Brand damage:** "Escalation meetings" signal relationship strain (Daimler)

**Priority:** 🟡 **HIGH**

**Rationale:**
- **Trust erosion:** Reliability is a strategic pillar; failing here undermines entire positioning
- **Enterprise blocker:** Companies won't deploy mission-critical if stability questionable
- **Long-term relationship risk:** Multi-year unfixed issues signal lack of commitment (Sascha: "disgrace")
- **Use case limitations:** Performance issues restrict what customers can do (Porsche)

**Notes / Dependencies:**
- Requires: Database architecture review, external DB support (managed Postgres), storage auto-scaling, GPU driver debugging, fragment addressing permanent fix, QueryAPI performance optimization
- Related to: Infrastructure/DevOps work, testing with large datasets, Service Level Agreement (SLA) commitments

---

### 5.7 Gap: Roles & Permissions System

**Definition:**

Current role management in 3DSpaces is too generic ("sticker" roles with no backend logic) and lacks fine-grained, robust access control. Cannot create reusable, productized role templates for package solutions. Insufficient RBAC to control who sees sensitive assemblies, especially for external collaborators, offshore teams, or customer-facing scenarios. SSO/auth integration (OAuth2, Microsoft AD) is basic and doesn't meet enterprise identity management needs.

**Evidence:**

- **Customer Success (Timm):** *"Urgent need for more robust permission concepts in 3DSpaces...current functionality too generic ('sticker' roles with no backend logic)."*
- **Customer Success (Timm):** *"When/if robust, reusable role management will be productized so it can be sold as an off-the-shelf module ('customers want to buy features, not infrastructure')."*
- **Porsche:** *"Not an easy, fine-grained way to control who can access/view sensitive assemblies—especially important for external/offshore contributors."*
- **Daimler Truck (Kyle):** *"Lack of robust role-based access control (RBAC)...getting proper RBAC 'figured out' as a major unsolved issue."*
- **Daimler Truck:** *"OAuth2 proxy setup for Single Sign-On is insufficient for our Microsoft identity integration."*

**Impact:**

- **Who Is Affected:** Integrators/Operators configuring access controls, particularly at customers wanting to share 3D content externally (suppliers, customers, offshore teams)
- **Business Impact:**
  - **Limits addressable use cases:** Can't confidently use for external collaboration or customer-facing scenarios
  - **Blocks packaged solutions:** Timm: can't sell features without robust, reusable roles
  - **Security concerns delay deals:** Enterprise IT won't approve without proper access controls
  - **Competitive gap:** Collaboration features being developed by competitors include robust permissions

**Priority:** 🟡 **HIGH**

**Rationale:**
- **Blocks external collaboration use cases** (high-value expansion opportunities)
- **Package solution blocker:** Timm explicitly said customers want to buy this as a feature
- **Enterprise IT requirement:** Proper RBAC is table-stakes for enterprise software
- **Strategic opportunity:** Enabling external collaboration opens new markets (supplier portals, customer configurators)

**Notes / Dependencies:**
- Requires: RBAC system design, role templates, permission inheritance, SSO/identity provider integrations (Microsoft AD, Okta, etc.)
- Could unlock: External collaboration use cases, packaged solutions, enterprise IT approval
- Related to: 3DSpaces strategy, security/compliance requirements

---

### 5.8 Gap: ERP/SAP & PLM Connector Maturity

**Definition:**

SAP PLM connector is "strategically vital" but "too specialized and not robust enough—needs further productization, not just project-specific fix." Teamcenter and Windchill connector presentation is "lacking, leading to lack of customer confidence." Integrating ERP data (article numbers, prices) into 3D models for spare parts catalogs and package solutions is increasingly requested but not well-supported. Current connectors are project-specific "U-Boot" (submarine) projects rather than productized offerings.

**Evidence:**

- **Sales (Aron, Andreas):** *"Integrating ERP data such as article numbers and prices into 3D models is highly relevant for package solutions, especially for spare parts catalogs. Customers increasingly request this capability."*
- **Presales (Sascha):** *"SAP PLM Connector: Strategically vital for making progress in the SAP/PLM market, but current feature set too specialized and not robust enough—needs further productization."*
- **Presales (Sascha):** *"Urges for this topic to be less of a 'U-Boat' project as it is essential for the SAP World."*
- **Presales (Sascha):** *"Teamcenter and Windchill Connectors: Our current presentation in this area is lacking, leading to a lack of customer confidence that has possibly cost us customers in the past."*
- **Porsche:** *"Teamcenter integration...difficult due to technical hurdles, reliance on intermediary tools."*

**Impact:**

- **Who Is Affected:** Customers in SAP/PLM ecosystems (automotive, machinery Original Equipment Manufacturers (OEMs)), spare parts catalog use cases
- **Business Impact:**
  - **Strategic market blocked:** Can't effectively penetrate SAP/PLM accounts without robust connectors
  - **Lost customer confidence:** Presentation lacks credibility (Sascha: "possibly cost us customers")
  - **Project risk:** Relying on project-specific integrations rather than productized solutions increases delivery risk
  - **BorgWarner opportunity at risk:** New deal focused on "replacing Siemens tools" requires strong PLM story

**Priority:** 🟡 **MEDIUM-HIGH**

**Rationale:**
- **Strategic market access:** SAP/PLM is large addressable market (automotive, manufacturing)
- **Confidence gap:** Current state undermines sales credibility
- **Competitive context:** BorgWarner evaluating us vs. Siemens consolidation play
- **Package solution enabler:** ERP integration needed for spare parts catalog use case

**Notes / Dependencies:**
- Requires: Productization of SAP PLM connector, Teamcenter/Windchill connector hardening, ERP endpoint integration (article numbers, pricing), sales collateral/demos for PLM story
- Related to: Integration/deployment complexity, customer onboarding

---

### 5.9 Gap: Product Packaging & Positioning (Go-to-Market)

**Definition:**

Positioning is "too broad" ("Spektrum und eine Lösung"), making it unclear what we solve for whom. "Platform vs. Apps" comparison is unfavorable—customers want to buy solutions, we sell infrastructure. No Marketing Qualified Leads (MQLs) generated, forcing Sales into unsustainable cold outreach. Lack of packaged, out-of-box solutions and compelling demos for specific use cases (Engineering Review, Documentation, etc.). Onboarding perceived as complex, requiring "too much resources to get up and running."

**Evidence:**

- **VP Sales:** *"Größtes Problem: Qualifizierte Leads fehlen komplett...Sales erhält keine Marketing Qualified Leads (MQLs)."* (Biggest problem: Qualified leads completely missing. Sales receives no Marketing Qualified Leads (MQLs). Only cold outreach, requires enormous research, unscalable, generates hardly usable pipeline.)
- **VP Sales:** *"Unsere Positionierung ist zu allgemein ('Spektrum und eine Lösung'). Dadurch ist schwer vermittelbar, was genau wir für wen lösen."* (Positioning too general. Hard to communicate what exactly we solve for whom.)
- **VP Sales:** *"Wunsch: Produktansprache statt 'Lösungs'-Spektrum. Klar definierter Ideal Customer Profile (ICP)."* (Want: Product messaging instead of "solution" spectrum. Clearly defined Ideal Customer Profile (ICP). Narrowly defined use case. Less platform story.)
- **Customer Success (Timm):** *"Selling a platform and always losing out against apps. Pressure to offer more 'complete' experiences that are easier to sell."*
- **Key Account (Bernd):** *"instant3Dhub is relatively complex...the amount of resources required to get it up and running from our side is too much."*

**Impact:**

- **Who Is Affected:** Sales team (can't generate pipeline), Marketing (no clear target), potential customers (don't understand value prop)
- **Business Impact:**
  - **Sales pipeline stalled:** No inbound leads, only unsustainable cold outreach
  - **Long sales cycles:** Unclear positioning = harder to communicate value = longer education period
  - **Lost deals:** "Platform vs. Apps" comparison is unfavorable (we lose)
  - **Resource inefficiency:** Sales doing heavy research per prospect instead of qualifying warm leads

**Priority:** 🟠 **MEDIUM-HIGH**

**Rationale:**
- **Sales can't scale without leads** (VP Sales: "biggest problem")
- **Positioning clarity needed:** Broad "platform" story doesn't resonate vs. focused "app" competitors
- **Strategic decision required:** Do we narrow to specific use case (Engineering Review?) or broaden packaging?
- **Not purely product gap:** Requires GTM/Marketing work, but product packaging impacts (out-of-box demos, solutions)

**Notes / Dependencies:**
- Requires: GTM strategy (ICP, use case focus), Marketing lead-gen investment, packaged solution development (pre-configured for Engineering Review, Documentation, etc.), compelling vertical-specific demos
- Could unlock: Inbound pipeline, faster sales cycles, clearer competitive positioning
- Related to: Missing viewer features (demos need rich functionality), documentation (onboarding complexity)

---

### 5.10 Gap: Vendor Responsiveness & Iteration Speed

**Definition:**

Customer perception that Threedy is **slow to fix issues and release improvements** compared to competitors. Daimler Truck explicitly compared us unfavorably to "Windmill" (fixes in 24-48 hours, deployed immediately) vs. instant3Dhub where "fixes take days or weeks." Multi-year unfixed issues (fragment addressing) reinforce perception of slow iteration. This impacts customer confidence, renewal risk, and competitive positioning.

**Evidence:**

- **Daimler Truck (Kyle):** *"With Windmill, a bug fix or feature request is addressed in 24–48 hours and deployed immediately, which has been a good experience. In contrast, their experience with instant3Dhub is that fixes take days or weeks to fix and updates are cumbersome to deploy."*
- **Presales (Sascha - fragment addressing):** *"Workaround 2 Jahre bestehen muss..."* (2-year workaround exists) → signals slow resolution

**Impact:**

- **Who Is Affected:** All customers, especially those with urgent issues or evaluating against competitors
- **Business Impact:**
  - **Competitive disadvantage:** Direct comparison to faster competitors (Windmill) damages win rates
  - **Customer trust erosion:** Slow fixes signal lack of responsiveness, reduces confidence in partnership
  - **Churn risk:** Customers may evaluate alternatives if responsiveness doesn't improve
  - **Brand perception:** Seen as "slower, less agile" than competitors

**Priority:** 🟠 **MEDIUM**

**Rationale:**
- **Competitive context:** Direct customer comparison to faster competitor
- **Perception vs. reality:** May be deployment friction (customer can't easily upgrade) rather than pure dev speed, but perception matters
- **Not purely product gap:** Requires process/org changes (release frequency, support SLAs, deployment ease)
- **Amplifies other gaps:** Slow fixes make other issues (stability, features) more painful

**Notes / Dependencies:**
- Requires: Faster release cadence, hotfix process, easier deployment/upgrade path (relates to Gap 5.1), SLA commitments for critical issues
- Could unlock: Customer confidence, competitive positioning improvement, renewal security
- Related to: Deployment complexity (easier upgrades = faster value delivery)

---

## 6. Market & Competitive Signals

*Relevant external signals that influence our 2026 priorities.*

### Industry Trends

**1. Cloud Adoption Accelerating in Engineering**
- **Trend:** Engineering companies increasingly open to SaaS solutions vs. on-premise requirements. Privacy concerns that dominated past years are reducing.
- **Evidence:** Competitor CoLab being adopted by US and German customers, signaling shifting attitudes toward cloud solutions.
- **Implication:** **Opportunity** to position instant3Dhub as cloud-native 3D solution, but **threat** if we don't capitalize—CoLab is already winning in this space.

**2. 3D-in-Web Becoming Standard, Not Novel**
- **Trend:** More 3D tools providing web-based functionality. Platforms like NX and 3D Experience (traditionally desktop) now offering web tooling. Expectation shifting from "3D in browser is cool" to "3D in browser is expected."
- **Implication:** **Commoditization risk.** Being "3D in the web" is no longer a differentiator. We must compete on ease-of-use, integration, and specific use case excellence (not just "it works in a browser").

**3. Catena-X Advancing But Slow Practical Adoption**
- **Trend:** Industry consortia (ZF, BMW, Mercedes, Bosch) contributing to Catena-X standard, but practical business impact unclear. Slow adoption with "open questions if this will result in possible business in the next year."
- **Evidence:** Presales (Sascha) skeptical: "no immediate benefit, skeptical regarding practical impact in next 12-24 months."
- **Implication:** **Strategic but not urgent.** Maintain standards compliance but don't over-invest in Catena-X as near-term growth driver. 12-24 month horizon, not 2026 priority.

**4. AI Expectations Rising Across Tools**
- **Trend:** Users increasingly expect AI-assisted features in all software (ChatGPT effect). CoLab positioning "AI Engineering Review" as differentiator.
- **Evidence:** Customer inquiries about AI for part recommendations, automated measurements, design prototyping (Daimler, Porsche mentioned).
- **Implication:** **Competitive pressure.** CoLab using AI as market messaging. We need AI roadmap (collision detection with learning, smart search, automated analysis) or risk being perceived as "behind the curve."

---

### Observed Competitor Improvements

**CoLab (Primary Threat - High)**
- **Profile:** AI-powered engineering review and collaboration platform
- **What They Did:** Launched "AI Engineering Review" positioning, winning customers in US and Germany (including some we compete with).
- **Threat Level:** 🔴 **HIGH** - Direct competitor in Engineering Review use case (VP Sales identified as "Killer-Thema")
- **Their Strengths:**
  - AI-native features and modern user experience
  - Strong marketing messaging around "AI Engineering Review"
  - Benefiting from industry shift to cloud/SaaS adoption (trend #1)
  - Functional advantages: collision detection, AI-assisted features we currently lack
- **Our Advantages:**
  - Broader platform capabilities beyond review workflows
  - Multi-SDK support (TypeScript, Java, Unreal)
  - Industry standards support (Catena-X, USD)
  - Enterprise-grade infrastructure
- **Our Response Needed:** Must deliver on Engineering Review use case with feature parity (collision detection, Gap 5.5) and define AI roadmap to neutralize their messaging advantage.

**Platform Incumbents: Siemens/NX & 3D Experience (Dassault Systèmes) - Medium-High Threat**
- **Profile:** Traditional CAD/PLM vendors expanding to web-based visualization
- **What They Did:** Adding web-based tooling to traditionally desktop platforms. Siemens Active Workspace becoming front-end for Teamcenter. 3D Experience growing web capabilities.
- **Threat Level:** 🟡 **MEDIUM-HIGH** - Strong enterprise relationships but slower to innovate
- **Their Strengths:**
  - Established customer base with deep enterprise relationships
  - Comprehensive PLM ecosystems (bundling advantage)
  - Integration threat: Can bundle 3D viewing with PLM, reducing willingness to pay for standalone viewer
  - BorgWarner example: Evaluating "which Siemens tools can be replaced"
- **Our Advantages:**
  - API-first, integration platform approach vs. monolithic suites
  - Modern web-native architecture vs. retrofitted web tooling
  - Faster innovation cycles (once we fix deployment friction)
  - Positioning opportunity: "Consolidation" play (replace multiple Siemens licenses with instant3Dhub)
- **Our Response Needed:** Prioritize Teamcenter/Active Workspace integration (Gap 5.1, 5.8), strengthen PLM connector story, position as cost-reduction alternative to expensive incumbent licensing.

**Legacy Desktop Tools: Vis/Mockup, TCViz - Medium Threat**
- **Profile:** Traditional desktop 3D visualization tools
- **Threat Level:** 🟡 **MEDIUM** - Customer habit and familiarity create switching resistance
- **Their Strengths:**
  - Engineering teams comfortable with existing workflows ("used to the UI" - Daimler)
  - Feature richness accumulated over years (grids, measurements, part movement, snapping)
  - Zero switching cost to stay (inertia favors incumbents)
- **Our Advantages:**
  - Modern web-based architecture enables collaboration (desktop tools can't)
  - Enterprise integration capabilities (legacy tools isolated)
  - Cloud-native scalability
- **Our Response Needed:** Close feature parity gaps (Gap 5.2: viewer features) to eliminate "legacy tool is more functional" objection. Emphasize collaboration and integration benefits legacy tools can't provide.

**Windmill - Medium Threat (Agility Benchmark)**
- **Profile:** Agile 3D visualization competitor
- **What They Did:** Unknown product details, but Daimler Truck used as benchmark for responsiveness: "Fixes in 24-48 hours, deployed immediately."
- **Threat Level:** 🟡 **MEDIUM** - Perception threat on iteration speed and deployment ease
- **Their Strengths:**
  - Fast iteration and feature development (24-48hr bug fix cycles)
  - Deployment ease: "Deploys in minutes" (Daimler context)
  - Agility perception advantage
- **Our Advantages:**
  - Enterprise-grade infrastructure and scalability
  - Industry standards support (Catena-X, USD)
  - Multi-SDK platform approach
  - Fortune 500 customer validation
- **Our Response Needed:** Improve perceived and actual responsiveness—faster release cycles, easier upgrades (Gap 5.1), SLA commitments. Close deployment friction gap to neutralize "deploys in minutes" comparison.

---

### Shifts in User Expectations

**From "Impressive Tech" to "Ease-of-Use Requirement"**
- **Shift:** Customers no longer impressed by "3D in browser" alone. Now expect:
  - **Fast, easy onboarding** (tolerance for multi-hour setup dropping to minutes)
  - **Feature parity with legacy tools** (not willing to sacrifice functionality for "cloud" benefit)
  - **Out-of-box value** (don't want to build everything themselves via SDK)
- **Evidence:**
  - Daimler: Users prefer legacy tool "because I'm used to the UI"—not switching unless new tool is clearly better, not just different
  - Key Account (Bernd): Customers expect "one-day turnaround" deployment, not weeks
- **Implication:** We're being compared to mature, feature-rich incumbent tools. "Platform with potential" story doesn't sell—we need **polished, complete solutions** for specific use cases.

**From Custom Development to Packaged Solutions**
- **Shift:** Customers increasingly want to "buy features, not infrastructure" (Timm quote).
- **Evidence:**
  - Customer Success (Timm): *"Selling a platform and always losing out against apps."*
  - VP Sales: *"Produktansprache statt 'Lösungs'-Spektrum"* (Product messaging, not solution spectrum)
- **Implication:** Must develop **packaged, vertical-specific solutions** (Engineering Review package, Documentation package, Spare Parts Catalog package) rather than just offering flexible platform.

---

### Strategic Partnership Developments

**BorgWarner - Siemens Replacement Opportunity**
- **Development:** BorgWarner evaluating "Harmonisierung von Engineering-Lösungen über die Zentrale IT. Welche Siemens-Tools können durch uns ersetzt werden?" (Harmonization of engineering solutions via central IT. Which Siemens tools can we replace?)
- **Opportunity:** Positioning as consolidation/cost-reduction play (replace multiple Siemens licenses with instant3Dhub).
- **Requirements:** Must have strong PLM connector story, demonstrate cost savings, and offer feature parity with tools being replaced.

**Daimler Truck - Active Workspace Migration**
- **Development:** Moving to Siemens Active Workspace as PLM front-end. Need to "see what it takes to integrate instant3Dhub" into AW.
- **Risk:** If we don't integrate, default Siemens viewer replaces us.
- **Opportunity:** If we integrate well, become embedded in their PLM workflow (increased stickiness).

---

### Implications for Our Strategy

**1. Engineering Review Must Be Our Sharpest Spear**
- VP Sales identified it as top use case, CoLab is winning here, and collision detection is a recurring customer request.
- **Action:** Prioritize collision/clash detection (Gap 5.5), position aggressively against CoLab with AI roadmap messaging.

**2. Ease-of-Use is Now Table-Stakes, Not Differentiator**
- Users won't tolerate complex onboarding, missing basic features, or poor docs just because we're "innovative."
- **Action:** Address Gaps 5.1 (deployment complexity), 5.2 (missing viewer features), 5.3 (documentation) as hygiene factors—without these, we can't compete.

**3. Platform Story Isn't Selling—Need Packaged Solutions**
- "Selling a platform and always losing out against apps" (Timm), "Positionierung ist zu allgemein" (VP Sales).
- **Action:** Develop vertical packages (Engineering Review Package, Documentation Package) with pre-configured features, clear ICP, and easier onboarding. Less "build your own," more "buy this specific solution."

**4. PLM/ERP Integration is Strategic Moat Opportunity**
- BorgWarner (Siemens replacement), Daimler (Active Workspace), multiple customers citing Teamcenter struggles.
- **Action:** Productize PLM connectors (Gap 5.8), invest in Teamcenter/Windchill/SAP PLM maturity, position as "consolidation" and cost-reduction vs. incumbents.

**5. AI Roadmap Needed to Neutralize CoLab Messaging**
- CoLab using "AI Engineering Review" as hook, customers asking about AI features.
- **Action:** Define AI roadmap (collision detection with learning, smart search, automated design checks) and communicate it. Don't need to ship everything in 2026, but need credible story.

**6. Catena-X is Strategic, But Don't Over-Prioritize in 2026**
- Industry moving slowly, practical business impact 12-24 months out.
- **Action:** Maintain compliance, participate in consortia, but don't bet 2026 roadmap on Catena-X driving revenue. Hygiene factor, not growth driver (yet).

---

## 7. Prioritized Opportunities for 2026

*Translate product gaps and market signals into actionable opportunities, grouped by timeframe.*

### Structure: Now (Q1-Q2 2026) / Next (Q3-Q4 2026) / Later (2027+)

---

### 7.1 NOW (Q1-Q2 2026)
*Immediate focus - highest impact, clearest path, resources committed.*

---

#### Opportunity 1: Deployment & Integration Overhaul

**What It Unlocks:**

Directly addresses **Gap 5.1 (Integration & Deployment Complexity)**, the #1 barrier to customer onboarding. Eliminates installation bottlenecks (Bosch, Grimme delays), reduces dependency on Threedy for setup, and enables self-service deployment for enterprise customers. Addresses Daimler Truck's "most challenging Helm chart" pain and PostgreSQL reliability issues. Improves competitive positioning vs. faster competitors (Windmill).

**Expected Impact:**

- **Metric Impact:**
  - Time-to-first-value: Weeks → Days (target: self-service deployment in <1 day for standard configs)
  - CS/PS utilization: -30-50% time spent on installation firefighting (redeploy to value-add work)
  - Deployment success rate: Measure % of customers successfully deploying without Threedy intervention (target: 70%+ self-serve)

- **Business Impact:**
  - **Unlock stalled deals:** Bosch, Grimme delays resolved → revenue recognition accelerated
  - **Improve win rates:** Faster deployment = competitive advantage vs. slow incumbents
  - **Reduce churn risk:** Better onboarding experience → higher renewal likelihood (Daimler frustration mitigated)
  - **Scale sales capacity:** Less CS/PS per-customer → can onboard more customers with same resources

- **Strategic Impact:**
  - Delivers on "Developer Experience First" pillar (easy onboarding is prerequisite)
  - Removes perception of "too complex" (Bernd: "too much resources to get up and running")
  - Enables self-service motion (reduces dependencies, scales better)

**Confidence Level:** High

**Reasoning:**
- **Clear problem with strong evidence:** Multiple customers (Daimler, Porsche, Bosch/Grimme) and internal stakeholders (Sales, CS, PS) all cite this
- **Bounded scope:** Helm chart refactoring, Azure docs, external DB support are engineering-heavy but well-defined
- **Competitive benchmark:** Daimler explicitly compared us unfavorably—fixing this directly improves positioning
- **Fast feedback loop:** Will know within weeks of release if deployments improve (track deployment time, support tickets, customer satisfaction)

---

#### Opportunity 2: Core Viewer Feature Parity (Movement, Grids, Units, Multi-View)

**What It Unlocks:**

Addresses **Gap 5.2 (Missing Core Viewer Features)**, the primary reason users stick with legacy tools (VisMockup, TCViz) out of habit. Adds essential functionality: incremental part movement with snapping, custom rotation centers, grid/plane overlays for measurements, side-by-side view with synced cameras, unit setting control. Removes adoption blocker that caused Daimler usage to "drop off quite a bit" after licensing introduced.

**Expected Impact:**

- **Metric Impact:**
  - User adoption/retention: Measure usage after fees introduced (Daimler baseline: collapsed to 1-2 users; target: maintain 70%+ of users when licensing applied)
  - Feature utilization: Track usage of new features (grids, multi-view, part movement) as proxy for value
  - User satisfaction: Developer NPS improvement (target: +15 points from post-feature-parity survey)

- **Business Impact:**
  - **Reduce "legacy tool preference" churn:** Users less likely to revert to VisMockup if feature parity achieved
  - **Strengthen value perception:** Can justify pricing when product is clearly better (or equivalent + faster) vs. incumbents
  - **Competitive differentiation:** Combine legacy tool features + modern platform (cloud, APIs) = best of both worlds

- **Strategic Impact:**
  - Delivers on "Developer Experience First" (daily tools must be easy and complete)
  - Enables "easier and faster" positioning (faster load times + full features = clear upgrade)
  - Reduces switching cost back to legacy tools (once users adopt our richer features, harder to leave)

**Confidence Level:** High

**Reasoning:**
- **User validation:** Daimler provided detailed list of exact features missing (grids, movement, multi-view) based on real workflows
- **Quick wins possible:** Many features (grids, unit settings, rotation center) are bounded UI/UX work, not architectural overhauls
- **Direct adoption impact:** Daimler case study shows adoption fragility when value isn't perceived; fixing this mitigates
- **Low technical risk:** These are established patterns in 3D viewers, not novel R&D

---

#### Opportunity 3: Documentation & Developer Self-Service Overhaul

**What It Unlocks:**

Addresses **Gap 5.3 (Documentation & Developer Self-Service)**, which causes support overhead, extends time-to-value, and frustrates developers. Restructures API docs from "endpoint dump" to task-based guides with code samples. Creates deep-dive guides for Query API (biggest pain point). Redesigns BRIX onboarding to remove technical entry barrier (repo access). Enables developers to self-serve, reducing CS/PS load and speeding integrations.

**Expected Impact:**

- **Metric Impact:**
  - Time-to-integration: Measure time from account creation to first API call / first 3D scene rendered (target: -40%, from hours to minutes for common tasks)
  - Support ticket reduction: Track docs-related tickets (target: -50% for Query API and BRIX onboarding questions)
  - Developer activation: % of developers who successfully complete onboarding without support intervention (target: 70%+)
  - BRIX adoption: Remove repo access barrier → measure sign-ups and active BRIX users (target: 2x growth in Q2)

- **Business Impact:**
  - **CS/PS cost savings:** Daimler: "5-60 minutes per task" saved → CS/PS redeploy to value-add work (estimated 10-15 hours/week across team)
  - **Faster customer enablement:** Shorter integration cycles → faster time-to-value → earlier revenue recognition
  - **BRIX ecosystem unlock:** Lower entry barrier → more developers try BRIX → ecosystem growth (strategic pillar)
  - **Competitive positioning:** Better docs = better developer experience = higher retention vs. competitors

- **Strategic Impact:**
  - Core to "Developer Experience First" and "Ecosystem-Powered Growth" pillars
  - Enables self-service motion (scales better than high-touch support)
  - Improves developer sentiment (Daimler: "direct ROI" comment shows customer awareness of value)

**Confidence Level:** High

**Reasoning:**
- **Clear problem with internal + external validation:** PS (Sudharsan, Hafedh), Daimler all cited docs as major friction
- **High ROI for effort:** Docs improvements don't require deep engineering, mainly technical writing + UX
- **Daimler benchmark:** They explicitly said better docs would save them time—this is customer-validated value
- **Fast feedback:** Can measure impact within weeks via support ticket trends and user onboarding metrics

---

#### Opportunity 4: Product Stability & Scale Investments (Database, Fragment Addressing, GPU)

**What It Unlocks:**

Addresses **Gap 5.6 (Product Stability at Enterprise Scale)**, which undermines trust and limits use cases. Fixes multi-year issues (fragment addressing), resolves database corruption risks (PostgreSQL, external DB support, auto-scaling storage), debugs GPU driver performance bug, and optimizes QueryAPI performance for large datasets. Restores confidence in "Enterprise-Grade Reliability" strategic pillar.

**Expected Impact:**

- **Metric Impact:**
  - Reliability SLA: Track uptime, database incidents, performance regressions (target: 0 PostgreSQL corruptions in Q2, 99.9% uptime)
  - Query performance: Measure time for complex filters on large assemblies (Daimler baseline: "over a minute"; target: <10 seconds for 90th percentile)
  - Large dataset support: Track % of customers using full assemblies vs. sub-assemblies (Porsche currently limited; target: enable full model usage)

- **Business Impact:**
  - **Churn risk mitigation:** Daimler escalation meetings resolved → relationship stabilizes
  - **Expand use cases:** Porsche can use full vehicle models (not just sub-assemblies) → increases value per customer
  - **Enable mission-critical deployments:** Enterprise customers more willing to deploy in production if stability proven
  - **Brand repair:** Multi-year issues fixed signals commitment and responsiveness

- **Strategic Impact:**
  - Restores credibility of "Enterprise-Grade Reliability" pillar (currently undermined by Daimler/Porsche experiences)
  - Prerequisite for enterprise expansion (can't sell at scale if stability questioned)
  - Reduces operational risk for customers (less fear of downtime)

**Confidence Level:** Medium-High

**Reasoning:**
- **Critical for trust:** Reliability issues erode confidence faster than features build it
- **Clear evidence:** Multiple incidents (Daimler PostgreSQL corruption 2-3x, Porsche performance issues, fragment addressing escalations)
- **Some uncertainty on root causes:** Database and GPU bugs may require deeper investigation (complexity risk)
- **Long-term payoff:** Stability is harder to "sell" than features, but foundational for retention and enterprise motion

---

### 7.2 NEXT (Q3-Q4 2026)
*Near-term pipeline - medium confidence, strong business case, ready when Now completes.*

---

#### Opportunity 5: Collision/Clash Detection for Engineering Review

**What It Unlocks:**

Addresses **Gap 5.5 (Collision/Clash Detection)**, a recurring customer request (Innio, Claas VR, ÖBB) and key feature for Engineering Review use case (identified by VP Sales as "Killer-Thema"). Enables automatic interference detection, assembly validation, and AI-based design checks. Directly competitive with CoLab's "AI Engineering Review" positioning.

**Expected Impact:**

- **Metric Impact:**
  - Feature adoption: Track usage of collision detection in engineering review workflows (target: 60%+ of engineering review customers use it within 3 months of launch)
  - Win rate in Engineering Review deals: Measure close rate for opportunities where Engineering Review is primary use case (current baseline unknown; target: improve vs. Q1-Q2 baseline)

- **Business Impact:**
  - **Unlock stalled deals:** Innio and similar prospects waiting for this feature (estimated 3-5 deals in pipeline)
  - **Competitive differentiation vs. CoLab:** Neutralize their "AI Engineering Review" positioning by offering similar capability
  - **Expand use cases:** Enables design validation, assembly planning, pre-manufacturing clash detection (high-value workflows)

- **Strategic Impact:**
  - Aligns with top market opportunity (Engineering Review)
  - Positions us in AI/automation trend (supports future "smart design assistant" roadmap)
  - Validates "Ecosystem-Powered Growth" (enables partners to build review workflows on platform)

**Confidence Level:** Medium

**Reasoning:**
- **Strong customer demand:** 3+ customers explicitly requested (Innio, Claas, ÖBB), Sales identified as "recurring need"
- **Strategic alignment:** VP Sales named Engineering Review as top use case; this is key feature for it
- **Technical complexity uncertainty:** Collision detection algorithm, 3D geometry analysis, UI for results—moderate R&D effort
- **Competitive timing:** CoLab already has AI review positioning; we're catching up, not leading (but still valuable)

---

#### Opportunity 6: Roles & Permissions System for External Collaboration

**What It Unlocks:**

Addresses **Gap 5.7 (Roles & Permissions System)**, enabling fine-grained access control for external collaborators (suppliers, customers), offshore teams, and packaged solutions. Makes 3DSpaces secure enough for customer-facing and supplier-facing scenarios. Enables productized role templates that can be sold as "feature, not infrastructure" (Timm's request).

**Expected Impact:**

- **Metric Impact:**
  - External collaboration usage: Track % of 3DSpaces with external participants (currently minimal; target: 30% of active spaces include external users by Q4 2026)
  - Packaged solution sales: Measure adoption of pre-configured role templates (target: 3-5 package solutions sold using RBAC features)

- **Business Impact:**
  - **Expand addressable use cases:** Unlock supplier collaboration, customer configurators, offshore team access (new revenue streams)
  - **Package solution enabler:** Timm: customers want to buy robust roles as a feature → can now sell this
  - **Enterprise IT approval:** Proper RBAC removes security blocker for cautious IT departments (faster deal cycles)
  - **Reduce custom dev per customer:** Reusable role templates mean less project-specific role customization (PS efficiency)

- **Strategic Impact:**
  - Enables external collaboration (expands market beyond internal-only use cases)
  - Supports packaged solution strategy (need robust permissions for productized offerings)
  - Aligns with enterprise requirements (RBAC is table-stakes for enterprise software)

**Confidence Level:** Medium

**Reasoning:**
- **Clear customer need:** Porsche (external/offshore access), Daimler (RBAC "major unsolved issue"), Timm (productization request)
- **Moderate complexity:** RBAC system design, permission inheritance, SSO integrations require careful architecture but well-understood patterns
- **Depends on 3DSpaces adoption:** If 3DSpaces usage doesn't grow, RBAC investment has limited impact (chicken-and-egg risk)
- **Unlock timing:** Needs to be ready before pushing external collaboration use cases (sequencing matters)

---

#### Opportunity 7: PLM Connector Productization (Teamcenter, Windchill, SAP PLM)

**What It Unlocks:**

Addresses **Gap 5.8 (ERP/SAP & PLM Connector Maturity)**, making Teamcenter, Windchill, and SAP PLM integrations robust, documented, and productized (not project-specific "U-Boat" solutions). Enables BorgWarner opportunity (Siemens replacement), improves credibility with automotive/machinery OEMs, and supports Daimler Truck's Active Workspace integration need.

**Expected Impact:**

- **Metric Impact:**
  - PLM integration success rate: Track % of Teamcenter/Windchill integrations completing on-time and on-budget (current baseline: Grimmer "months overdue"; target: 90% on-time by Q4)
  - Connector adoption: Measure # of customers using productized connectors vs. custom integrations (target: 70% use standard connector by end of 2026)

- **Business Impact:**
  - **Strategic market access:** BorgWarner (Siemens replacement), Daimler (Active Workspace), automotive/machinery OEMs (SAP PLM)
  - **Confidence gap closed:** Presales (Sascha): "current presentation lacking"—productized connectors with demos/docs restore credibility
  - **PS efficiency:** Less custom integration work per project → more scalable delivery model
  - **Competitive positioning:** Position as "consolidation" play vs. Siemens/incumbents (replace multiple tools with instant3Dhub)

- **Strategic Impact:**
  - Unlocks SAP/PLM market segment (large addressable market in automotive, manufacturing)
  - Supports BorgWarner strategic opportunity (cost reduction, tool consolidation)
  - Reduces integration complexity (ties to Gap 5.1)

**Confidence Level:** Medium

**Reasoning:**
- **High strategic value:** Automotive/machinery OEMs are high-value customers; SAP/PLM access is key
- **BorgWarner timing:** Active opportunity requiring strong PLM story (near-term forcing function)
- **Technical complexity:** Productizing connectors (vs. project-specific) requires robust testing, documentation, support—moderate effort
- **Depends on partnerships:** May need deeper DataKit, Siemens, SAP relationships to accelerate (external dependencies)

---

### 7.3 LATER (2027+)
*Longer-term opportunities - lower confidence, strategic bets, important but not urgent.*

---

#### Opportunity 8: AI-Powered Design Assistant (Collision Learning, Smart Search, Automated Analysis)

**What It Unlocks:**

Positions instant3Dhub in AI/automation trend, neutralizing CoLab's "AI Engineering Review" messaging and supporting future "smart design workflows." Includes collision detection that learns from usage patterns, AI-driven part recommendations (Daimler: "find a larger fuel tank automatically"), intelligent search across 3D assemblies, and automated impact analysis of design changes (Porsche request).

**Expected Impact:**

- **Metric Impact:**
  - AI feature usage: Track adoption of AI-assisted features (smart search, automated recommendations, learning collision detection)
  - Engineering efficiency gains: Measure time savings for common tasks (e.g., "find replacement part") using AI vs. manual search

- **Business Impact:**
  - **Competitive differentiation:** Neutralize CoLab's AI positioning by offering similar/better AI capabilities
  - **Premium pricing justification:** AI features can command higher pricing tier (market expectation: AI = premium)
  - **Customer stickiness:** AI that learns from customer's specific data creates lock-in (customized value)

- **Strategic Impact:**
  - Future-proofs platform against AI expectations (users expect AI in all tools post-ChatGPT)
  - Enables "smart engineering assistant" vision (long-term product direction)
  - Positions as innovation leader (not follower catching up to CoLab)

**Confidence Level:** Low-Medium

**Reasoning:**
- **Market trend validation:** Customers asking about AI (Daimler, Porsche), CoLab using AI as hook
- **High technical uncertainty:** AI/ML capabilities require R&D, data science expertise, training data—significant investment
- **Unclear customer willingness to pay:** AI is "cool" but ROI needs validation (vs. must-have features like collision detection)
- **Long development cycle:** AI features typically require iteration, training, refinement—not quick wins
- **Strategic placeholder:** Important to have on roadmap for competitive messaging, but execution is 2027+ (not 2026 priority)

---

#### Opportunity 9: Product Packaging & Go-to-Market Realignment

**What It Unlocks:**

Addresses **Gap 5.9 (Product Packaging & Positioning)** by narrowing positioning from "platform for everything" to **focused use case packages** (Engineering Review Package, Documentation Package, Spare Parts Catalog Package). Develops clear ICP, invests in Marketing lead-gen to generate MQLs (solving VP Sales's "biggest problem"), and creates out-of-box demos/solutions that are "easier to sell" (Timm's request).

**Expected Impact:**

- **Metric Impact:**
  - Marketing Qualified Leads (MQLs): Measure inbound lead volume (current: 0; target: 50+ MQLs per quarter by end of 2026)
  - Sales cycle length: Track time from first contact to closed deal (target: -30% reduction with clearer positioning and warm leads)
  - Win rate: Measure close rate for opportunities with clear ICP fit vs. broad positioning (target: improve from baseline)

- **Business Impact:**
  - **Sales pipeline growth:** VP Sales: "no MQLs" is biggest problem—fixing this unlocks scalable pipeline
  - **Sales efficiency:** Warm leads replace cold outreach → less research per prospect, more time selling
  - **Faster deal cycles:** Clear "Product for Use Case X" story reduces education period, speeds decisions
  - **Competitive differentiation:** "Apps" beat "platforms" in buying decisions—packaged solutions level playing field

- **Strategic Impact:**
  - Solves foundational GTM problem (can't scale sales without inbound leads)
  - Aligns product with market demand (Timm: customers want to buy solutions, not infrastructure)
  - Enables vertical expansion (different packages for different industries/use cases)

**Confidence Level:** Medium

**Reasoning:**
- **Critical business problem:** VP Sales identified MQL gap as "biggest problem"—high urgency
- **Not purely product work:** Requires Marketing investment (lead-gen campaigns), GTM strategy (ICP definition, messaging), Sales alignment—cross-functional complexity
- **Packaging depends on product maturity:** Hard to sell "Engineering Review Package" if core features (collision detection, viewer parity) aren't solid yet (sequencing: Now/Next opportunities enable this)
- **Market validation uncertainty:** Will narrower positioning (less "platform") actually improve win rates? Hypothesis, not proven
- **2026-2027 timeline:** Start in late 2026 (after core product gaps closed), fully execute in 2027

---

#### Opportunity 10: Remote Rendering & Photorealism for Customer-Facing Use Cases

**What It Unlocks:**

Addresses external collaboration security concerns (Daimler: can't share raw CAD with customers without NDA) and photorealism gap (Porsche: lack of "car configurator-level rendering"). Enables remote rendering (server-side rendering, client receives video stream) for IP protection and photorealistic rendering for marketing/customer-facing scenarios (configurators, sales tools).

**Expected Impact:**

- **Metric Impact:**
  - External sharing usage: Track # of 3D sessions shared externally with remote rendering (security-conscious customers can now share)
  - Photorealism feature adoption: Measure usage of high-fidelity rendering for marketing/sales use cases

- **Business Impact:**
  - **Expand use cases:** Unlock customer-facing scenarios (configurators, supplier portals, sales demos) currently blocked by IP concerns
  - **Premium use case access:** Marketing/sales teams willing to pay for photorealistic rendering (higher-value customer segments)
  - **Competitive differentiation:** Photorealism + remote rendering = unique combination (most competitors offer one or the other, not both)

- **Strategic Impact:**
  - Enables customer-facing product line (new market segment beyond internal engineering use)
  - Addresses security constraint (remote rendering = IP stays on server)
  - Supports premium positioning (photorealism commands higher pricing)

**Confidence Level:** Low

**Reasoning:**
- **Niche use case:** Remote rendering primarily for high-IP-sensitivity customers; photorealism for marketing/sales (not engineering core)
- **High technical complexity:** Remote rendering requires infrastructure (rendering servers, video streaming, latency optimization), photorealism requires advanced rendering pipeline—both significant R&D
- **Unclear customer willingness to pay:** Daimler mentioned remote rendering as *"don't completely shut the door"* (interest, not urgency); Porsche mentioned photorealism (desire, not deal-blocker)
- **Sequencing:** Only valuable after core engineering use cases are solid (can't sell premium marketing tool if engineering tool is incomplete)
- **2027+ timeline:** Strategic option to explore once foundational product gaps are closed and market pull is validated

---

## Summary: 2026 Opportunity Prioritization

**Now (Q1-Q2 2026) - Must Do:**
1. Deployment & Integration Overhaul (Gap 5.1)
2. Core Viewer Feature Parity (Gap 5.2)
3. Documentation & Developer Self-Service Overhaul (Gap 5.3)
4. Product Stability & Scale Investments (Gap 5.6)

**Next (Q3-Q4 2026) - High Value:**
5. Collision/Clash Detection for Engineering Review (Gap 5.5)
6. Roles & Permissions System (Gap 5.7)
7. PLM Connector Productization (Gap 5.8)

**Later (2027+) - Strategic Bets:**
8. AI-Powered Design Assistant
9. Product Packaging & Go-to-Market Realignment (Gap 5.9)
10. Remote Rendering & Photorealism

**Rationale for Prioritization:**
- **Now:** Foundation-fixing. Without easy deployment, core features, good docs, and stability, we can't compete. These are prerequisites for growth.
- **Next:** Differentiation. Collision detection, RBAC, and PLM connectors unlock specific high-value use cases and markets. Build on Now foundation.
- **Later:** Innovation & expansion. AI, GTM overhaul, and premium use cases (remote rendering) are valuable but require foundational product to be solid first.

---

*End of State Of The Product Report - Q4 2025*
