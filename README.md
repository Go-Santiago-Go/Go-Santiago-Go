# Christian Santiago

**Cloud and software engineer focused on AWS infrastructure, data pipelines, cost efficiency, and
service reliability.**

Lately I have been building AWS infrastructure in Go, Python, and Terraform for generative AI and
machine learning workloads. I build the operational layer around GenAI
systems and adopt changes on measured results rather than intuition.

[christiansantiago.dev](https://christiansantiago.dev) ·
[Resume](https://christiansantiago.dev/resume.pdf) ·
[LinkedIn](https://www.linkedin.com/in/christian-santiago-dev/) ·
[santiagothedeveloper@gmail.com](mailto:santiagothedeveloper@gmail.com)

🚧 Currently building **[grant-fit](https://github.com/Go-Santiago-Go/grant-fit)**: an autonomous tool-using agent on Amazon Bedrock and AWS Strands that researches federal grant eligibility, cites the span of text behind every verdict, and declines when the evidence is not there. Three reasoning architectures (chain-of-thought, ReAct, tree-of-thoughts) behind one interface, measured against each other on accuracy, latency, and cost.

To stay up to date with applied AI and solve tangible industry problems, my current professional development includes building document intelligence pipelines in the [Pfizer Advanced AI-Powered Document Intelligence](https://www.extern.com/externships/pfizer-advanced-ai-powered-document-intelligence-externship-jul-2026) externship.

## Projects

Each of these is deployed and verified end to end, provisioned entirely in Terraform, and shipped by
GitHub Actions over OIDC with no long-lived AWS keys. The numbers below are measured, and each repo
documents its own trade-offs, results, and limitations.

| Project | What it is | Stack |
|---|---|---|
| **[retrain-pipeline](https://github.com/Go-Santiago-Go/retrain-pipeline)**<br>training and governance | CI-driven continuous training where bad data cannot merge and no model promotes without a human reading the evaluation. Great Expectations gates the pull request, the dataset's content hash becomes the model's identity, and a Go CLI drives SageMaker over OIDC. Promotion is enforced by a **missing IAM action**, not a policy: CI can propose a model and structurally cannot promote one. Demonstrated end to end, merge to registered in under 4 minutes. | Go · Python · SageMaker · DVC · Great Expectations · Terraform |
| **[inference-gateway](https://github.com/Go-Santiago-Go/inference-gateway)**<br>serving | The production ops layer in front of LLM inference: SSE token streaming, per-key auth and rate limiting, retries with backoff and jitter, and **multi-provider failover with per-backend circuit breakers**, all composed behind one Go interface. A client disconnect cancels the in-flight Bedrock call instead of paying for unread tokens. ~4.6 µs/request overhead under concurrency; 8.6 MB distroless image. | Go · Bedrock · SSE · React · TypeScript · ECS Fargate · Terraform |
| **[rag-api](https://github.com/Go-Santiago-Go/rag-api)**<br>retrieval | Grounded answers with structured citations, where the passages that built the prompt are the passages returned. Two-stage retrieval (pgvector shortlist, cross-encoder rerank) lifted passage **recall@5 from 57.1% to 77.1%**, each change measured before adoption. An LLM-as-judge harness, validated against deliberately broken answers, graded **zero unfaithful answers across 70 responses**. | Go · Bedrock · pgvector · ECS Fargate · Terraform |
| **[drift-sentinel](https://github.com/Go-Santiago-Go/drift-sentinel)**<br>🚧 drift detection · building | **Work in progress, not yet running.** Phase 0 is complete: the infrastructure layer plus a hash-sealed frozen holdout with CI enforcing its invariants. The serving, monitoring, and training loop above it is not built yet, so there are no results to show. The design wires a drift score to an action rather than a dashboard, so a threshold breach will fire retraining and an automated champion challenger gate. | Python · PyTorch · MLflow · Airflow · Feast · Evidently |
| **[christiansantiago.dev](https://github.com/Go-Santiago-Go/christiansantiago.dev)**<br>cloud resume challenge | Private S3 origin behind CloudFront OAC, same-origin routing that designs CORS out, and a visitor counter that is one atomic DynamoDB `ADD`: **500 of 500 visits recorded under 500 concurrent callers**, where read-then-write lost 498 silently. Deployed by push, gated by a Playwright test against production. | Go · Lambda · DynamoDB · CloudFront · Terraform · OIDC |

## Background

Four years in an enterprise environment on infrastructure monitoring and incident response, and the
data engineering around it, working directly with the clients and stakeholders who depended on the
output, through a hybrid on-premise to AWS migration. Since then, systems integration, ETL pipelines,
BI reporting for leadership, and freelance application development. I reach for the smallest thing
that meets the requirement rather than the largest thing that impresses.

AWS Certified Developer, working toward AWS Certified Generative AI Developer Professional. Studied
computer science at Vanderbilt University and cloud engineering through the AWS Cloud Institute. Currently
reinforcing my math foundations through [Math Academy's Math for Machine Learning track](https://www.mathacademy.com/courses/mathematics-for-machine-learning)
