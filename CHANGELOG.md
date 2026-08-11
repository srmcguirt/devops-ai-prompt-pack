# Changelog

All notable changes to the DevOps AI Prompt Pack will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.0.0] - 2026-08-10

### Added

- **8 System Prompts** — Production-quality system prompts for DevOps AI workflows:
  - IaC Generator (Terraform/Pulumi) — modular, secure, multi-cloud infrastructure code generation
  - Kubernetes Debugger — systematic diagnosis with exact kubectl commands and remediation
  - CI/CD Pipeline Designer — GitHub Actions workflows with caching, secrets, and deployment gates
  - Cloud Cost Optimizer — FinOps analysis with quantified savings and implementation roadmaps
  - Incident Response Commander — structured incident management from detection through post-mortem
  - Container Architecture Planner — Dockerfiles, Compose configs, and orchestration strategies
  - Infrastructure Security Auditor — CIS Benchmark and NIST-aligned security analysis
  - Monitoring & Observability Architect — SLO-based alerting, golden signals, and stack design

- **24 Few-Shot Examples** — 3 realistic input/output pairs per prompt with actual code, commands, and configurations

- **8 JSON Schemas** — Structured output schemas for every prompt, compatible with OpenAI's `response_format`, Claude's tool use, and any JSON-mode API

- **Comprehensive README** — Installation, usage examples for Claude/GPT/Cursor/VS Code, before/after comparison, compatibility matrix

- **MIT License** — Full commercial use permitted
