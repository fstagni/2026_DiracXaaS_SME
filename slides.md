---
colorSchema: light
favicon: /public/images/diracx-logo-square.svg
color: diracx-light
layout: cover
routerMode: hash
title: DiracX as a Service for SMEs?
theme: neversink
neversink_string: "DiracGrid @ CERN IT-SME"
download: true
transition: slide-left
---

# DiracX as a Service for SMEs?
## Would you use it? And in which form?

<img src="/public/images/diracx-logo-square.svg" class="h-24 mx-auto my-4">

**Federico Stagni** <Email v="federico.stagni@cern.ch" />

DiracGrid Technical Coordinator, CERN

<br>

CERN IT-SME Coordination Meeting, November 2026

<a href="https://indico.cern.ch/event/1745440/" class="ns-c-iconlink"><mdi-open-in-new />indico.cern.ch/event/1745440</a>

---
layout: top-title-two-cols
color: diracx-light
align: cm-lm-lm
title: diracgrid
columns: is-8
class: cols-split
---

:: title ::

# What is DiracGrid, actually?

:: left ::

An "**interware**" (a tool for doing distributed computing), started within LHCb 25 years ago (!).

Today used by a few dozens communities, for managing **jobs** (via pilots), **data**, **productions**, **dataset transfers**, ...

<br>

ATM the DiracGrid project develops and maintains 2 whole software stacks:
- [DIRAC](https://github.com/DIRACGrid/DIRAC) (the "legacy" workhorse) (+Web)
- [DiracX](https://github.com/DIRACGrid/diracx) (DIRAC's cloud-native rethink+rewrite)

<div class="flex justify-center items-center gap-8 mt-4">
  <img src="/public/images/DIRAC-logo-extended.png" class="h-14">
  <span class="text-3xl">→</span>
  <img src="/public/images/diracx-logo-full.svg" class="h-14 diracx-logo">
</div>

:: right ::

## Community

<br>

<AdmonitionType type=info>
Apart from the regular zoom meetings, we meet at <strong>3 hackathons per year</strong>, plus one <strong>workshop</strong> (the <a href="https://indico.cern.ch/event/1588323/">12th Dirac(X) Users' Workshop</a> was in Prague, October 2026)
</AdmonitionType>

<br>

Open source (Apache-2.0), developed in the open at [github.com/DIRACGrid](https://github.com/DIRACGrid)

---
layout: top-title
color: diracx-light
align: cm
title: story
---

:: title ::

# The shortened Dirac's story

:: content ::

```mermaid
%%{init: {'theme': 'base', 'timeline': {'disableMulticolor': true}}}%%
timeline
        section LHCb software
          around 2000 : MC production system: bash scripts running at production sites
          2002 : DIRAC2 <br> Rewritten in Python, using xml-rpc, interfacing to EDG
          Data Challenge 04 : First successful grid usage ever.
                            : First use of pilot jobs based WMS
        section Open sourced, wider adoption
          2008 : Large-ish reshuffling to become multi-VO
          2011 : France-Grilles is the first multi-VO DIRAC installation
          2012 : Belle2, BES3, CTA adopt DIRAC
        section The DiracX era
          2023 : First DiracX prototype
          2025 : LHCb puts DiracX in production
          2026 : CMS and FCC join the effort
```

---
layout: top-title
color: gray-light
align: c
title: core-functionalities
clicks: 4
---

:: title ::

## Core functionalities and tools (enormous simplification)

:: content ::

<v-switch>
<template #0>

### **Core functionalities**

<br>

```mermaid
%%{init: { 'theme': 'default' }}%%
flowchart LR
    WMS["`**WMS**
    Workload Management System`"]
    DMS["`**DMS**
    Data Management`"]
    MD["`**Metadata and provenance**`"]
    PROD["`**Production Management**
    Workflow Orchestration`"]
    IS["`**Information System**
    Resources & Status`"]
    DIRAC(["`**DIRAC / DiracX**`"])

    style WMS fill:#bbf,stroke:#88c
    style DMS fill:#bfb,stroke:#8c8,stroke-width:2px
    style MD fill:#aaa,stroke:#aaa,stroke-width:2px
    style PROD fill:#eef,stroke:#8ec
    style IS fill:#fff,stroke:#000
    style DIRAC fill:#f90,color:#000,stroke:#c60,stroke-width:3px

    PROD -->|submits jobs to| WMS
    PROD -->|gets data from| MD
    PROD -->|gets info from| IS
    WMS -->|gets info from| IS
    DMS -->|gets info from| IS
    PROD -->|gets data loc from| DMS
    WMS -->|gets data loc from| DMS
    DMS -->|gets data from| MD
```

</template>
<template #1>

# **JUNO**, **GridPP**
Small-medium installations that want an all-in-one system

```mermaid
%%{init: { 'theme': 'default' }}%%
flowchart TD
    WMS["`**WMS**
    Workload Management System`"]
    DMS["`**DMS**
    Data Management`"]
    PROD["`**Production Management**
    Workflow Orchestration`"]
    IS["`**Information System**
    Resources & Status`"]
    MD["`**Metadata and provenance**`"]
    DIRAC(["`**DIRAC / DiracX**`"])

    style WMS fill:#bbf,stroke:#88c
    style DMS fill:#bfb,stroke:#8c8,stroke-width:2px
    style PROD fill:#eef,stroke:#8ec
    style IS fill:#fff,stroke:#000
    style MD fill:#aaa,stroke:#aaa,stroke-width:2px
    style DIRAC fill:#f90,color:#000,stroke:#c60,stroke-width:3px

    WMS -->|implemented by| DIRAC
    DMS -->|implemented by| DIRAC
    PROD -->|implemented by| DIRAC
    IS -->|implemented by| DIRAC
    MD -->|implemented by| DIRAC
```

Old DIRAC was largely monolithic. DiracX emphasizes modularity and well-defined APIs.

</template>
<template #2>

# **LHCb**
Not a small installation, but the oldest and carrying legacy.

```mermaid
%%{init: { 'theme': 'default' }}%%
flowchart TD
    WMS["`**WMS**
    Workload Management System`"]
    DMS["`**DMS**
    Data Management`"]
    PROD["`**Production Management**
    Workflow Orchestration`"]
    IS["`**Information System**
    Resources & Status`"]
    MD["`**Metadata and provenance**`"]
    DIRAC(["`**DIRAC / DiracX**`"])
    BKK(["`**LHCb Bookkeeping**`"])

    style WMS fill:#bbf,stroke:#88c
    style DMS fill:#bfb,stroke:#8c8,stroke-width:2px
    style PROD fill:#eef,stroke:#8ec
    style IS fill:#fff,stroke:#000
    style MD fill:#aaa,stroke:#aaa,stroke-width:2px
    style DIRAC fill:#f90,color:#000,stroke:#c60,stroke-width:3px
    style BKK fill:#aa1,color:#002,stroke:#eee,stroke-width:3px

    WMS -->|implemented by| DIRAC
    DMS -->|implemented by| DIRAC
    PROD -->|implemented by| DIRAC
    IS -->|implemented by| DIRAC
    MD -->|implemented by| BKK
```

</template>
<template #3>

# **Belle2**, **CTAO**, and **FCC**
The need for modularity comes also from existing DIRAC installations

```mermaid
%%{init: { 'theme': 'default' }}%%
flowchart TD
    WMS["`**WMS**
    Workload Management System`"]
    DMS["`**DMS**
    Data Management`"]
    PROD["`**Production Management**
    Workflow Orchestration`"]
    MD["`**Metadata and provenance**`"]
    IS["`**Information System**
    Resources & Status`"]
    DIRAC(["`**DIRAC / DiracX**`"])
    RUCIO(["`**Rucio**`"])

    style WMS fill:#bbf,stroke:#88c
    style DMS fill:#bfb,stroke:#8c8,stroke-width:2px
    style PROD fill:#eef,stroke:#8ec
    style IS fill:#fff,stroke:#000
    style MD fill:#aaa,stroke:#aaa,stroke-width:2px
    style DIRAC fill:#f90,color:#000,stroke:#c60,stroke-width:3px
    style RUCIO fill:#4a9,color:#fff,stroke:#276,stroke-width:3px

    WMS -->|implemented by| DIRAC
    DMS -->|implemented by| RUCIO
    PROD -->|implemented by| DIRAC
    IS -->|implemented by| DIRAC
    MD -->|implemented by| RUCIO
```

</template>
<template #4>

# **CMS**
For CMS, modularity is a must.

```mermaid
%%{init: { 'theme': 'default' }}%%
flowchart TD
    WMS["`**WMS**
    Workload Management System`"]
    DMS["`**DMS**
    Data Management`"]
    PROD["`**Production Management**
    Workflow Orchestration`"]
    IS["`**Information System**
    Resources & Status`"]
    MD["`**Metadata and provenance**`"]
    RUCIO(["`**Rucio**`"])
    GLIDE(["`**GlideInWMS+HTCondor**`"])
    CRIC(["`**CRIC**`"])
    WM(["`**WMAgent**`"])
    DBS(["`**DBS**`"])
    DIRAC(["`**DiracX**`"])

    style RUCIO fill:#4a9,color:#fff,stroke:#276,stroke-width:3px
    style GLIDE fill:#56b,color:#fff,stroke:#235,stroke-width:3px
    style CRIC fill:#19b,color:#000,stroke:#239,stroke-width:3px
    style WM fill:#ee1,color:#003,stroke:#eee,stroke-width:3px
    style MD fill:#aaa,stroke:#aaa,stroke-width:2px
    style DBS fill:#0a1,color:#002,stroke:#eee,stroke-width:3px
    style DIRAC fill:#f90,color:#000,stroke:#c60,stroke-width:3px

    WMS -->|implemented by| GLIDE
    DMS -->|implemented by| RUCIO
    MD -->|implemented by| DBS
    PROD -->|implemented by| WM -->|replaced by| DIRAC
    IS -->|implemented by| CRIC
```

</template>
</v-switch>

---
layout: top-title
color: diracx-light
align: cm
title: users
---

:: title ::

# Who uses it, today

:: content ::

A few dozens communities, of very different sizes:

- **Big** (and carrying legacy): **LHCb**, **Belle II** (KEK/BNL), **CTAO**, **CMS** (joining 2026)
- **Small-medium installations that want an all-in-one system**: **JUNO**, **GridPP**, **BES III**, **FCC** (joining 2026), ...
- Plus several **national/provincial cloud** installations and smaller experiments

<br>

<AdmonitionType type='info' >
Several of these are, in CERN terms, exactly "SMEs": they have the same data/production challenges as the big ones, with a fraction of the people
</AdmonitionType>

<br>

What they all got for granted: **pilots to Grid/HPC/cloud**, productions, data management, a Web UI, a CLI, and an API

---
layout: top-title-two-cols
color: diracx-light
align: cm-lm-lm
title: diracx
columns: is-8
---

:: title ::

# <img src="/public/images/diracx-logo-full.svg" class="h-10 inline-block align-middle diracx-logo"> Not a port: a **reimplementation**

:: left ::

**Cloud-native by design**
- Kubernetes-based deployments
- **OAuth2 / JWT tokens** (no x509 proxies), REST APIs everywhere
- Modular services, well-defined APIs
- **Multi-VO** as a first-class citizen

**New data model**
- The spine: **workgraph**, **transformations**, **parcels**
- Pluggable **compute backends**: pilots, HPC push, **HTCondor**, legacy DIRAC, ...

:: right ::

<AdmonitionType type='important' >
DIRAC is only **patched** meanwhile: all new developments happen in DiracX
</AdmonitionType>

- You move **one component at a time**, DIRAC and DiracX run in parallel
- LHCb has been in **production** on DiracX since 2025
- CMS and FCC joined the effort in 2026

<span class="stamp">From "DiracGrid software stacks" · <a href="https://indico.cern.ch/event/1628935/">RCW26</a> and <a href="https://indico.cern.ch/event/1588323/">DUW12</a></span>

---
layout: top-title
color: diracx-light
align: cm
title: status
---

:: title ::

# DiracX, status (late 2026)

:: content ::

- **New development process** since January 2026: SCRUM, 2-week sprints, monthly `DOps` with community representatives
- **ADRs for everything**: transparent, reviewable, community-driven design ([DX-ADR series](https://diracx.diracgrid.org/en/latest/adr/))
- The **Transformation System** (productions, the new heart) is being implemented, with scenario tests and a [playground](https://diracx.diracgrid.org/en/latest/playground/)
- **36 contributors**, **634 PRs** merged across DIRACGrid repositories since the last workshop, from **9 communities**

<br>

<AdmonitionType type='tip' >
Everything is public: roadmap, ADRs, [docs](https://diracx.diracgrid.org/), playground
</AdmonitionType>

<span class="stamp">From "DiracGrid software stacks" · <a href="https://indico.cern.ch/event/1628935/">RCW26</a></span>

---
layout: section
color: diracx
title: raas
---

# The blueprint: "Rucio as a Service" at CERN IT

---
layout: top-title-two-cols
color: diracx-light
align: cm-lm-lm
title: raas-what
columns: is-8
---

:: title ::

# RaaS: what CERN IT does for Rucio

:: left ::

**Rucio-as-a-Service**: a centrally managed, ready-to-use Rucio data management service for Small and Medium Experiments.

- **One cluster per community**, run by the Rucio IT team; each community's admins own their data and policies
- Next to the other CERN IT services: **EOS, CTA, FTS, CVMFS, PostgreSQL**
- A prototype in 2025, **in production today**

:: right ::

## Communities on board

<br>

**AMS-02**, **SHiP**, **n_TOF**, **FCC**, **NA62**, EOSC, RI-SCALE, RBAC, ...

<br>

<AdmonitionType type='info' >
"Same data challenges, but smaller teams": now one team runs Rucio for them all
</AdmonitionType>

<span class="stamp">From "Update on RaaS at CERN" · H. Gonzalez Labrador · <a href="https://indico.cern.ch/event/1628935/contributions/7313407/">RCW26</a></span>

---
layout: top-title-two-cols
color: diracx-light
align: cm-lm-lm
title: raas-numbers
columns: is-6
---

:: title ::

# RaaS: some numbers

:: left ::

<div class="grid grid-cols-3 gap-4 text-center my-4">
  <div class="border rounded-lg p-3"><div class="text-4xl font-bold diracx-accent">9</div><div class="text-sm">Rucio clusters</div></div>
  <div class="border rounded-lg p-3"><div class="text-4xl font-bold diracx-accent">20.3</div><div class="text-sm">petabytes</div></div>
  <div class="border rounded-lg p-3"><div class="text-4xl font-bold diracx-accent">33.7</div><div class="text-sm">million files</div></div>
  <div class="border rounded-lg p-3"><div class="text-4xl font-bold diracx-accent">46</div><div class="text-sm">RSEs</div></div>
  <div class="border rounded-lg p-3"><div class="text-4xl font-bold diracx-accent">13</div><div class="text-sm">countries</div></div>
  <div class="border rounded-lg p-3"><div class="text-4xl font-bold diracx-accent">770K</div><div class="text-sm">API requests/day</div></div>
</div>

99% of the data at CERN, but RSEs as far as MIT

:: right ::

**Simple and stupid, by design:**

- One k8s (OpenStack Magnum) cluster per community, **not** multi-VO Rucio
- GitOps: state in Git, synced by **Argo CD**, secrets from **Vault**, self-healing
- Reuse services maintained by someone else (PostgreSQL, OpenStack, FTS, Vault)

<AdmonitionType type='tip' >
"Our job is to keep the backbone simple, reliable and cheap to run"
</AdmonitionType>

<span class="stamp">From "Update on RaaS at CERN" · H. Gonzalez Labrador · <a href="https://indico.cern.ch/event/1628935/contributions/7313407/">RCW26</a></span>

---
layout: top-title
color: diracx-light
align: cm
title: raas-why
---

:: title ::

# Why RaaS works for SMEs

:: content ::

- **Low barrier to adoption**: experiments write data into a designated disk pool; archiving, replication and policy enforcement happen automatically (an "illusion of an HSM")
- SMEs are **shielded from underlying technology changes** (x509→tokens, Tape REST API, TPC, ...)
- Support is streamlined: **from N×M discussions to N×1**
- SMEs declaratively set **what** they want to do with the data, not **how**
- A **blueprint for new experiments**: a production-grade DM environment from day one (e.g. SHiP)

<span class="stamp">From "Enabling SMEs with Rucio-as-a-Service" · H. Gonzalez Labrador · <a href="https://indico.cern.ch/event/1545309/contributions/6717953/">RCW25</a></span>

---
layout: section
color: diracx
title: question
---

# The question

---
layout: top-title
color: diracx-light
align: cm
title: the-question
---

:: title ::

# The question

:: content ::

<div class="flex items-center justify-center my-8">
<div class="border-2 rounded-xl p-8 text-center" style="border-color: var(--diracx-primary); background: rgba(0,175,202,0.06);">

### If CERN-IT would host a **DiracX-as-a-Service** instance for SMEs,
### in a fashion similar to what Rucio-as-a-Service is for data management...

<br>

# ...would SMEs be interested?

# And in which forms?

</div>
</div>

---
layout: top-title
color: diracx-light
align: cm
title: shape
---

:: title ::

# What it would look like (the shape)

:: content ::

Same philosophy as RaaS, different domain:

|  | **RaaS** (Rucio) | **DiracXaaS** (DiracX) |
|---|---|---|
| Domain | data management | **workload & production management** (+data management) |
| Deployment | one k8s cluster per community | one **DiracX deployment per community** |
| Run by | CERN IT Rucio team | CERN IT **DiracGrid** team |
| Backbone | EOS, CTA, FTS, PostgreSQL, Vault | CERN batch / LCG / HPC pilots, PostgreSQL, Vault |
| Onboarding | write data, define declarative rules | describe productions/jobs; the **Transformation System** runs them |
| Interface | CLI, Web UI, API | CLI, Web UI, API (same) |

<AdmonitionType type='important' >
SMEs would get production-grade WMS+productions, with no servers to run and no operators to hire
</AdmonitionType>

---
layout: top-title
color: diracx-light
align: cm
title: what-you-get
---

:: title ::

# What an SME would get

:: content ::

- **Workload management**: user jobs and productions dispatched via pilots to Grid (WLCG), HPC and cloud resources
- **Productions**: the DiracX Transformation System (workgraphs of transformations), the same machinery used by LHCb, CMS and FCC
- **Data management**, two options (not mutually exclusive):
  - DIRAC-style: file catalog (DFC), Storage Elements, transfers
  - or glued to **RaaS Rucio**: the Transformation System drives Rucio rules (the pattern already used by Belle II, CTAO, FCC, CMS)
- **Interfaces**: Web UI, CLI, API; **OAuth2** tokens; multi-VO
- **Monitoring, accounting, analytics** for your community

<AdmonitionType type='info' >
In short: what big experiments have, without operating it
</AdmonitionType>

---
layout: top-title
color: diracx-light
align: cm
title: why-diracx
---

:: title ::

# Why DiracX, and not DIRAC?

:: content ::

<AdmonitionType type='important' >
A hosted, shared service can only be built on **DiracX**.
</AdmonitionType>

- A service for many communities must be **cloud-native**: Kubernetes, REST APIs, OAuth2/tokens, multi-VO → that's exactly what DiracX is, and legacy DIRAC is not
- **DIRAC is in maintenance mode**: security patches and performance fixes, but all new developments happen in DiracX
- Starting an SME on DIRAC today would mean asking them to **migrate tomorrow**
- The new features SMEs care about (Transformation System, new compute backends, ...) **only land in DiracX**

<br>

<AdmonitionType type='tip' >
"DIRAC or DiracX?" is a fair question -- the answer is: **only DiracX**
</AdmonitionType>

---
layout: top-title
color: diracx-light
align: cm
title: forms
---

:: title ::

# "In which forms?" -- questions for you

:: content ::

- **Scope**: full WMS + productions? Analysis jobs only? With or without data management?
- **Compute resources**: which ones should be in scope? CERN batch, WLCG sites, HPC centres, cloud?
- **Data**: where would it live? EOS/CTA at CERN, RSEs at your sites, RaaS Rucio?
- **Deployment model**: one deployment per community (RaaS style)? Or a single multi-VO DiracX instance?
- **Support & cost**: what level of service do you expect? What is a sustainable model?
- **Onboarding**: would your data/production workflows fit the Transformation System model?

<br>

<AdmonitionType type='info' >
The answer to these questions defines the service: your input is needed!
</AdmonitionType>

---
layout: top-title
color: diracx-light
align: cm
title: synergy
---

:: title ::

# Synergy with RaaS: a one-stop shop

:: content ::

The DiracX--Rucio interplay is already a working pattern for the big communities:

- **Belle II**: Rucio as file catalog + DDM; DIRAC jobs read/write via the `RucioFileCatalog` plugin
- **CTAO**: Dirac(X) for WMS/TS and **Rucio for data management**, in the same k8s deployment
- **FCC** and **CMS**: Rucio as the DMS, DiracX taking over workflow management

<br>

For SMEs, CERN IT could offer both:

<AdmonitionType type='tip' >
**DiracXaaS for jobs and productions + RaaS for data** = the full stack, operated by the same IT department
</AdmonitionType>

<span class="stamp">From "DiracGrid software stacks" · <a href="https://indico.cern.ch/event/1628935/">RCW26</a></span>

---
layout: top-title-two-cols
align: cm-cm-lm
color: diracx-light
columns: is-4
title: summary
---
:: title ::

# Summary

:: left ::

<img id="DiracX" src="/public/images/diracx-logo-square.svg" class="mx-auto w-4/5"> </img>

:: right ::

<ul class="text-base">
  <li>DiracGrid provides DIRAC and DiracX: distributed computing for a few dozens communities, from SME-like installations to the big LHC ones.
    <ul class="text-sm">
      <li>DiracX is the future: cloud-native, modular, multi-VO; DIRAC only patched meanwhile</li>
    </ul>
  </li>
  <li>CERN IT already runs Rucio-as-a-Service for SMEs: production-grade data management with no operational overhead.
    <ul class="text-sm">
      <li>The same model could work for workload and production management</li>
    </ul>
  </li>
  <li>The question: would a <strong>DiracX-as-a-Service</strong> for SMEs be useful? In which form?
    <ul class="text-sm">
      <li>Only DiracX-based, of course 😉</li>
      <li>Your input defines the scope: jobs, productions, data, resources, support model</li>
    </ul>
  </li>
</ul>

---
layout: section
color: diracx
title: Questions
---

# Questions? / Discussion

---
layout: section
color: diracx
title: backup
---

# Backup

---
layout: top-title-two-cols
color: diracx-light
align: cm-lm-lm
title: raas-ops
columns: is-6
---

:: title ::

# Backup: RaaS operations

:: left ::

**Infrastructure (Oct. 2026):**

- 9 Rucio clusters + 1 for Argo CD, 78 nodes/VMs
- 464 CPU cores (3% used), 833 GiB RAM (30% used)
- 1,345 running pods; 105 namespaces, only 129 Rucio daemon pods

**Operations:**

- 41 Argo CD applications, synced from Git, self-healing
- 770K API requests a day, 14.5M log lines a day
- Logs in Loki (30 days) and on file (1 year), 10.5 GB/day
- Monitoring: Prometheus + Grafana, 4 linked dashboards; scripts and AI condense signals and apply actions

:: right ::

<AdmonitionType type='info' >
Mostly operations: the RaaS team also contributes to upstream Rucio development
</AdmonitionType>

One Rucio cluster per community keeps things **simple**: one conf file per cluster, standard deployment (`rucio-<deployment>`), all under `*.rucioit.cern.ch`

<span class="stamp">From "Update on RaaS at CERN" · H. Gonzalez Labrador · <a href="https://indico.cern.ch/event/1628935/contributions/7313407/">RCW26</a></span>

---
layout: top-title
color: diracx-light
align: cm
title: roadmap
---

:: title ::

# Backup: the DiracX roadmap

:: content ::

<img src="/public/images/duw12/directions/roadmap.png" class="w-4/5 mx-auto">

<AdmonitionType type='important' >
Priorities, not commitments. New requirements can reorder this page, and the team writes the detailed plan.
</AdmonitionType>

<span class="stamp">From "DiracX developments: directions" · A. Boyer · <a href="https://indico.cern.ch/event/1588323/contributions/7301774/">DUW12</a></span>

---
layout: top-title
color: diracx-light
align: cm
title: ts-usecases
---

:: title ::

# Backup: the Transformation System, in one slide

:: content ::

> A **workgraph** is a directed acyclic graph of **transformations**. Each transformation maintains a pool of **inputs**: a **feeder** tops up the pool, a **packer** groups pooled inputs into **parcels**, and a **dispatcher** hands each parcel to a compute or data **backend**, which executes it as a job or a request. -- DX-ADR-002

- Everything **composes**: each use case changes only the shape of the graph, and which feeder, packer and actions are plugged in
- **Compute backends** are pluggable: native pilots, push to HPC, HTCondor, legacy DIRAC, ...
- User jobs take the same path as productions

<span class="stamp">From "The DiracX Transformation System" · C. Burr · <a href="https://indico.cern.ch/event/1588323/contributions/7264643/">DUW12</a></span>
