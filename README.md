# DevOps AI Prompt Pack by MCPForge

> **8 battle-tested system prompts that turn any LLM into a senior DevOps engineer.** Complete with few-shot examples and structured output schemas for Claude, GPT-4, Cursor, VS Code Copilot, and any OpenAI-compatible API.
>
> *Part of the [MCPForge](https://mcpforge.dev) AI tooling collection.*

---

## What's Inside

| # | Prompt | What It Does |
|---|--------|-------------|
| 1 | **IaC Generator** | Generates production-ready Terraform & Pulumi configs with modules, variables, outputs, and security defaults |
| 2 | **K8s Debugger** | Systematically diagnoses Kubernetes issues with exact kubectl commands and remediation steps |
| 3 | **CI/CD Designer** | Designs GitHub Actions pipelines with caching, secrets management, matrix testing, and deployment gates |
| 4 | **Cloud Cost Optimizer** | Analyzes AWS/GCP/Azure spending and produces prioritized savings recommendations with dollar estimates |
| 5 | **Incident Response Commander** | Guides teams through SEV1-SEV4 incidents with structured communication, mitigation, and post-mortems |
| 6 | **Container Architecture Planner** | Creates Dockerfiles, Compose configs, and orchestration strategies for any application stack |
| 7 | **Infrastructure Security Auditor** | Audits IAM policies, security groups, CI/CD pipelines, and configs against CIS Benchmarks and NIST |
| 8 | **Monitoring & Observability Architect** | Designs monitoring stacks with SLOs, golden signals, alert rules, dashboards, and on-call policies |

### What Makes These Different from Free Prompts

- **200+ words each** — These are comprehensive system prompts with role definitions, behavioral constraints, output format specifications, and edge case handling. Not one-liner instructions.
- **Real few-shot examples** — Each prompt includes 3-5 realistic input/output pairs with actual Terraform code, kubectl commands, YAML manifests, and dollar-amount cost analyses.
- **Structured output schemas** — JSON Schema files for every prompt, ready to use with OpenAI's structured output, Claude's tool use, or any JSON-mode API. Parse AI responses programmatically.
- **Edge case coverage** — Each prompt handles the hard cases: multi-cloud setups, monorepo CI/CD, security incidents with legal implications, GPU workload cost optimization, and more.

---

## Quick Start

### With Claude (Anthropic)

1. Copy the system prompt from `system-prompts/01-iac-generator.md`
2. Paste it as the `system` message in the Claude API or Claude.ai custom instructions
3. Start prompting:

```
Create a production VPC in AWS us-east-1 with public/private subnets, NAT gateways, and VPC flow logs.
```

### With GPT-4 / ChatGPT

1. Open ChatGPT → Settings → Custom Instructions → System Prompt
2. Paste the system prompt content
3. For structured output, use the schemas in `output-schemas/` with the `response_format` parameter:

```python
from openai import OpenAI
import json

client = OpenAI()

# Load system prompt
with open("system-prompts/01-iac-generator.md") as f:
    system_prompt = f.read()

# Load output schema
with open("output-schemas/01-iac-generator-schema.json") as f:
    schema = json.load(f)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": system_prompt},
        {"role": "user", "content": "Create an S3 bucket with versioning, encryption, and lifecycle policies"}
    ],
    response_format={
        "type": "json_schema",
        "json_schema": {
            "name": "iac_output",
            "schema": schema
        }
    }
)
```

### With Cursor / VS Code Copilot

1. Create a `.cursorrules` or `.github/copilot-instructions.md` file in your project root
2. Paste the relevant system prompt
3. The AI assistant will now respond with DevOps-specific expertise in your editor context

### With Claude Code / Aider / Any CLI Tool

```bash
# Use as a system prompt file
claude --system-prompt system-prompts/02-k8s-debugger.md

# Or pipe it
cat system-prompts/05-incident-response.md | your-ai-tool --system-prompt -
```

### Programmatic Usage (Build into Your App)

```typescript
import { readFileSync } from 'fs';

// Load prompt + schema for structured output
const systemPrompt = readFileSync('system-prompts/04-cloud-cost-optimizer.md', 'utf-8');
const outputSchema = JSON.parse(readFileSync('output-schemas/04-cloud-cost-optimizer-schema.json', 'utf-8'));

// Load few-shot examples for better accuracy
const examples = JSON.parse(readFileSync('few-shot-examples/04-cloud-cost-optimizer-examples.json', 'utf-8'));

// Build messages array with few-shot examples
const messages = [
  { role: 'system', content: systemPrompt },
  // Add few-shot examples as conversation history
  ...examples.examples.flatMap(ex => [
    { role: 'user', content: ex.input },
    { role: 'assistant', content: JSON.stringify(ex.output) }
  ]),
  // Actual user query
  { role: 'user', content: 'Our AWS bill is $25,000/month. Here is the breakdown...' }
];
```

---

## File Structure

```
devops-ai-prompt-pack/
├── system-prompts/           # 8 expert system prompts (Markdown)
│   ├── 01-iac-generator.md
│   ├── 02-k8s-debugger.md
│   ├── 03-cicd-designer.md
│   ├── 04-cloud-cost-optimizer.md
│   ├── 05-incident-response.md
│   ├── 06-container-planner.md
│   ├── 07-security-audit.md
│   └── 08-monitoring-setup.md
│
├── few-shot-examples/        # Realistic input/output pairs (JSON)
│   ├── 01-iac-generator-examples.json
│   ├── 02-k8s-debugger-examples.json
│   ├── 03-cicd-designer-examples.json
│   ├── 04-cloud-cost-optimizer-examples.json
│   ├── 05-incident-response-examples.json
│   ├── 06-container-planner-examples.json
│   ├── 07-security-audit-examples.json
│   └── 08-monitoring-setup-examples.json
│
├── output-schemas/           # JSON Schema for structured output (JSON)
│   ├── 01-iac-generator-schema.json
│   ├── 02-k8s-debugger-schema.json
│   ├── 03-cicd-designer-schema.json
│   ├── 04-cloud-cost-optimizer-schema.json
│   ├── 05-incident-response-schema.json
│   ├── 06-container-planner-schema.json
│   ├── 07-security-audit-schema.json
│   └── 08-monitoring-setup-schema.json
│
├── README.md
├── LICENSE
└── CHANGELOG.md
```

---

## Before & After

### Without This Pack

```
You: "Help me set up monitoring"
AI: "You should use Prometheus and Grafana. Set up some dashboards and alerts."
```

*Generic advice. No specifics. No implementation.*

### With This Pack

```
You: "Design monitoring for our 12-service K8s app. Team of 8, startup budget."
AI: [Returns complete monitoring architecture with:]
- Stack selection with cost justification (Prometheus + Grafana + Loki = $0 software)
- SLO definitions with error budgets and burn rate alerts
- 5 production-ready PromQL alert rules with severity levels and runbook links
- Alertmanager configuration with inhibition rules
- Structured log schema with correlation IDs
- Dashboard hierarchy from overview to debug drill-down
- Step-by-step installation commands (Helm charts)
```

*Specific, actionable, production-ready output that saves hours of research.*

---

## Who This Is For

- **DevOps / Platform Engineers** — Get expert-level system prompts without writing them yourself
- **SREs** — Incident response and monitoring prompts based on Google SRE best practices
- **Engineering Managers** — Give your team AI tools that produce consistent, high-quality infrastructure
- **Consultants** — Use as templates for client engagements, accelerate delivery
- **AI/LLM App Builders** — Embed these prompts in your DevOps AI products with the structured output schemas

---

## Compatibility

| Platform | System Prompt | Few-Shot Examples | Structured Output |
|----------|:---:|:---:|:---:|
| Claude (Anthropic) | ✅ | ✅ | ✅ (tool_use) |
| GPT-4o / GPT-4 (OpenAI) | ✅ | ✅ | ✅ (json_schema) |
| Claude Code | ✅ | ✅ | ✅ |
| Cursor | ✅ | ✅ | — |
| VS Code Copilot | ✅ | ✅ | — |
| Aider | ✅ | ✅ | — |
| Ollama / Local LLMs | ✅ | ✅ | ⚠️ (model-dependent) |
| LangChain / LlamaIndex | ✅ | ✅ | ✅ |
| Any OpenAI-compatible API | ✅ | ✅ | ✅ |

---

## License

MIT License — use in personal projects, commercial products, SaaS apps, consulting engagements. See [LICENSE](LICENSE) for details.

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.

---

## Prompt Chaining Recipes

Combine prompts for end-to-end DevOps workflows:

### Infrastructure Pipeline
```
IaC Generator → CI/CD Designer → Monitoring Setup
```
1. Generate the Terraform modules for your infrastructure
2. Feed the repo structure to the CI/CD Designer to create deploy pipelines
3. Use the Monitoring Setup prompt to design observability for the deployed infra

### Incident-to-Prevention Pipeline
```
Incident Response → K8s Debugger → Monitoring Setup
```
1. Use Incident Response to structure the active incident
2. Feed symptoms to the K8s Debugger for systematic diagnosis
3. After resolution, use Monitoring Setup to create alerts that catch this class of issue earlier

### Security Hardening Pipeline
```
Security Audit → IaC Generator → CI/CD Designer
```
1. Audit existing infrastructure configs with the Security Auditor
2. Feed the remediation recommendations to the IaC Generator to produce corrected Terraform
3. Use CI/CD Designer to add security scanning gates (Trivy, tfsec, checkov) to your pipeline

### Containerization Pipeline
```
Container Planner → CI/CD Designer → Cloud Cost Optimizer
```
1. Design the container architecture with Dockerfiles and Compose
2. Create the CI/CD pipeline for building, scanning, and deploying images
3. Analyze the container infrastructure costs and optimize instance types, spot usage, and scaling

---

**Built by [MCPForge](https://mcpforge.dev) — engineers who've been on-call at 3 AM.** These prompts encode the patterns we wish we'd had when we started.
