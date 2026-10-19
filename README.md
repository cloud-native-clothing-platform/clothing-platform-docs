# Cloud-Native Clothing Platform

AWS-oriented clothing storefront using Python/FastAPI, Docker, GitHub Actions, Terraform, Amazon ECR, Amazon EKS, and Helm.

## Repositories
- `clothing-web-frontend`: static storefront starter
- `clothing-product-service`, `clothing-user-service`, `clothing-order-service`, `clothing-payment-service`, `clothing-inventory-service`, `clothing-shipping-service`: service APIs
- `clothing-infra-terraform`: ECR repositories and private frontend bucket baseline
- `clothing-helm-charts`: reusable Kubernetes service chart

## Local development
Run a FastAPI service with `pip install -r requirements.txt && uvicorn src.main:app --reload`. Build with `docker build -t clothing-service:dev .`. API docs are at `/docs`; health endpoint is `/health`.

## Delivery guardrails
1. Feature branches and reviewed PRs; promote develop to main after validation.
2. Prefer GitHub OIDC to AWS rather than long-lived access keys.
3. Run tests, dependency/image scans, and image builds before deploy.
4. Use immutable image tags, protected environments, health checks, and rollout verification.
5. Review `terraform plan` before applying infrastructure. Do not auto-apply production changes from unreviewed PRs.

## Known starter limitations
Service state is in memory and is not production persistence. Authentication, authorization, durable database storage, schema migrations, idempotency, cross-service orchestration, payment-provider integration, and end-to-end tests still need implementation. The storefront is a UI starter; checkout is not connected.
