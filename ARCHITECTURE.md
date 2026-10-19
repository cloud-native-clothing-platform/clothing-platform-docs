# Architecture and deployment notes

## Request flow
Browser → frontend → product catalog → order API → inventory reservation → payment adapter → shipment creation. These repositories define service boundaries; distributed orchestration and compensation still need implementation.

## AWS baseline
- ECR: immutable, scan-on-push service repositories
- EKS: Kubernetes runtime; cluster provisioning is intentionally separate from the starter Terraform resources
- Private S3: frontend artifact storage; use CloudFront with Origin Access Control for production delivery
- Terraform: repeatable, reviewable infrastructure
- GitHub Actions: CI and delivery workflows
- Helm: Kubernetes service releases

## Production checklist
- RDS/Aurora and schema migrations
- Secrets Manager/Parameter Store; never commit secrets
- OIDC trust scoped to repository and environment
- TLS, CDN/WAF, rate limits, authentication and authorization
- Metrics, logs, traces and actionable alerts
- HPA, PodDisruptionBudgets, topology spread and resource budgets
- Backup/restore tests, runbooks, rollback and disaster recovery drills
- Security scans and SBOM/provenance checks
