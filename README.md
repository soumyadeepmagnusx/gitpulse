# ⚡ GitPulse: Cloud-Synced Git Recovery & Telemetry Hub
> **Track 3 Hackathon Entry: Spec-Driven Agentic Engineering & Zero-Dollar Serverless Architecture**

[![Always-Free Cloud Footprint](https://img.shields.io/badge/AWS%20Monthly%20Cost-%240.00%20(Always--Free)-00C853?style=for-the-badge&logo=amazon-aws)](https://calculator.aws)
[![Pay-as-you-go Floor](https://img.shields.io/badge/Pay--As--You--Go%20(1k%20MAU)-%240.38%2Fmo%20(Bonus%20Qualified)-blue?style=for-the-badge)](https://calculator.aws)
[![Kiro Spec-Driven](https://img.shields.io/badge/Kiro-Spec--Driven%20Architecture-7C3AED?style=for-the-badge)](https://kiro.dev)

---

### 📝 Submission Note (How Kiro Shaped Our Build)
> **How Kiro Shaped Our Build:** Instead of jumping straight into boilerplate code, Kiro's spec-driven workflow forced us to lock down EARS-formatted acceptance criteria and a single-table DynamoDB access pattern in `design.md` before writing a single Lambda function. Our custom steering files (`.kiro/steering/`) kept the agent strictly aligned with AWS Always-Free constraints—automatically favoring modular SDK imports and stateless execution without repeated prompting. Finally, configuring PostFileSave hooks automated our linting and type-syncing between backend handlers and the React frontend, turning a multi-day cloud deployment into a clean, deterministic sprint.

---

## 🎯 High-Impact Concept (Option A)

When engineers get stuck in detached HEAD states, botched interactive rebases, or accidental `git reset --hard` executions, panic sets in and work gets permanently destroyed or hours are lost. 

**GitPulse** solves this with a two-part serverless system:
1. **Lightweight Telemetry Ingestion:** Developers run a CLI command (`gitpulse heal` or webhook) that snapshots local git state and reflog diffs.
2. **Deterministic State-Machine Engine:** An AWS Lambda Function URL evaluates the git state graph in under 150ms and computes an idempotent, non-destructive recovery shell script with verified rollback commands.
3. **Team Telemetry Dashboard:** A React + Vite SPA tracking team-wide repository stability scores, incident frequency, and friction hotspots.

---

## 💰 Zero-Dollar Serverless Pricing Breakdown (1,000 MAUs)

To sweep both the standard criteria and the **Sub-$1/Month Cloud Footprint Bonus**, here is the exact itemized pricing math:

### Scenario 1: AWS Always-Free Tier Allowance (Default)
| Service Layer | Resource Config | Monthly Ingestion / Bandwidth | Always-Free Allowance | Monthly Cost |
| :--- | :--- | :--- | :--- | :--- |
| **Frontend & CDN** | AWS Amplify / S3 + CloudFront | ~15 GB transfer, 250k HTTP requests | 1 TB transfer, 10M requests, 5 GB S3 | **$0.00** |
| **Authentication** | Amazon Cognito (Lite User Pool) | 1,000 Monthly Active Users (MAUs) | Up to 10,000 MAUs | **$0.00** |
| **Serverless Compute** | AWS Lambda (ARM64 / Graviton2, 128MB) | 300,000 invocations @ 150ms avg | 1,000,000 invocations + 400,000 GB-sec | **$0.00** |
| **Database** | DynamoDB Single-Table (On-Demand) | 500k reads, 150k writes, 1.2 GB storage | 25 GB storage + 25 RCU/WCU | **$0.00** |
| **API Layer** | Direct Lambda Function URLs | 300,000 direct invocations | Included in Lambda invocation count | **$0.00** |
| **TOTAL (Free Tier)** | | | | **$0.00 / month** |

### Scenario 2: Pure Pay-As-You-Go Math (Zero Free Tier Assumed)
Even if you evaluate the project on a non-free account without any promotional credits or AWS Free Tier benefits, it easily beats the **under-$1/month bonus bar**:
- **AWS Lambda (ARM64 Graviton2):**
  - Compute: $300,000 \times 0.15\text{s} \times (128/1024)\text{ GB} = 5,625\text{ GB-seconds} \times \$0.0000133334 = \$0.075$
  - Requests: $300,000 \times \$0.20 / 1,000,000 = \$0.060$
  - Subtotal: **$0.06 / month**
- **Amazon DynamoDB (On-Demand):**
  - 150,000 Write Request Units (WRU) @ $1.25 / million = $0.187
  - 500,000 Read Request Units (RRU) @ $0.25 / million = $0.125
  - Storage: 1.2 GB @ $0.25 / GB = $0.30 (or $0.00 under base tier)
  - Subtotal: **$0.22 / month**
- **S3 & Data Transfer:**
  - 15 GB Data Transfer Out @ $0.09 / GB = $0.10
  - Subtotal: **$0.10 / month**
- **TOTAL (Pure Pay-As-You-Go):** **$0.38 / month** (Well under the $1.00/mo threshold!)

---

## 🏛️ Repository Structure & Kiro Spec-Driven Artifacts

```
git-recovery-hub/
├── .kiro/
│   ├── specs/
│   │   └── git-recovery-telemetry/
│   │       ├── requirements.md         # Acceptance criteria in strict EARS format
│   │       ├── design.md               # Architecture, Single-Table DynamoDB schema, Mermaid flows
│   │       └── tasks.md                # Sequenced, checkable implementation tasks
│   ├── steering/
│   │   ├── product.md                  # Problem domain, personas, and feature boundaries
│   │   ├── tech-stack.md               # Enforces React/Vite/Tailwind + ARM64 Python/Node
│   │   └── serverless-rules.md         # Zero-cost guardrails (no NAT, single-table, Function URLs)
│   └── hooks/
│       ├── guard-serverless-saves.json # PostFileSave automated lint & test trigger
│       └── sync-api-schema.json        # Auto-syncs payload contracts on handler changes
├── backend/
│   ├── template.yaml                   # AWS SAM Infrastructure as Code (Graviton2, Single-Table DDB)
│   ├── src/
│   │   ├── handlers/
│   │   │   ├── ingest_telemetry.py     # Schema validation & recovery generation
│   │   │   └── get_metrics.py          # Single-table GSI1 querying & health scoring
│   │   └── utils/
│   │       ├── dynamo.py               # Reusable DynamoDB client with connection pooling
│   │       └── git_graph.py            # Deterministic state-machine recovery engine
│   └── tests/
│       └── test_recovery.py            # Automated unit tests for recovery algorithms
├── frontend/
│   ├── package.json                    # Minimal Vite + React + Tailwind footprint
│   └── src/
│       ├── App.tsx                     # Interactive telemetry dashboard & disaster simulator
│       ├── components/
│       │   ├── HealthDashboard.tsx     # Atomic repo health score cards
│       │   ├── IncidentFeed.tsx        # Real-time failure log inspection
│       │   └── RecoveryTerminal.tsx    # Deterministic copyable recovery shell commands
│       └── types/
│           └── telemetry.ts            # Shared API interfaces
└── README.md                           # Live Link, Architecture, and Pricing Math
```

---

## 📊 Single-Table DynamoDB Architecture (`gitpulse_core`)

| Entity | PK | SK | GSI1PK | GSI1SK | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Incident** | `REPO#<repo_id>` | `INCIDENT#<timestamp>#<id>` | `REPO#<repo_id>` | `INCIDENT#<timestamp>` | State type, commit, and recovery plan |
| **Metrics** | `REPO#<repo_id>` | `METRICS#<YYYY-MM-DD>` | `ORG#<org_id>` | `DATE#<YYYY-MM-DD>` | Atomic counters for incident frequencies |
| **Recovery** | `INCIDENT#<id>` | `RECOVERY` | `REPO#<repo_id>` | `STATUS#<status>` | Step-by-step commands & rollback hash |

---

## 🚀 Quickstart & Verification

### 1. Run Backend Unit Tests Locally
```bash
python backend/tests/test_recovery.py
```

### 2. Run React Dashboard Locally
```bash
cd frontend
npm install
npm run dev
```

### 3. Deploy Serverless Backend to AWS
```bash
cd backend
sam build
sam deploy --guided
```
