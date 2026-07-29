# Christian Santiago

**Cloud and software engineer focused on AWS infrastructure, data pipelines, cost efficiency, and
service reliability.**

Lately I have been building AWS infrastructure in Go, Python, and Terraform for generative AI and
machine learning workloads, and MLOps is where I am headed.

[christiansantiago.dev](https://christiansantiago.dev) ·
[Resume](https://christiansantiago.dev/resume.pdf) ·
[LinkedIn](https://www.linkedin.com/in/christian-santiago-dev/) ·
[santiagothedeveloper@gmail.com](mailto:santiagothedeveloper@gmail.com)

## Projects

| Project | What it is | Stack |
|---|---|---|
| **[retrain-pipeline](https://github.com/Go-Santiago-Go/retrain-pipeline)**<br>training and governance | Bad data cannot merge and no model promotes without a human reading the evaluation. Great Expectations gates the pull request, a Go CLI submits a SageMaker job tagged with the dataset hash and Git SHA. | Go · Python · SageMaker · DVC · Terraform |
| **[inference-gateway](https://github.com/Go-Santiago-Go/inference-gateway)**<br>serving | Fronts Bedrock with SSE token streaming, per-key auth and rate limiting, retries with jitter, and per-request cost accounting. A client disconnect cancels the in-flight call instead of paying for unread tokens. | Go · Bedrock · SSE · React · ECS Fargate · Terraform |
| **[go-rag-api](https://github.com/Go-Santiago-Go/go-rag-api)**<br>retrieval | Chunks and embeds documents with Bedrock Titan v2, searches them by cosine similarity in pgvector. Database in a private subnet, distroless container on Fargate, CI to ECR over OIDC. Deployed and verified end to end. | Go · Bedrock · pgvector · ECS Fargate · Terraform |
| **[drift-sentinel](https://github.com/Go-Santiago-Go/drift-sentinel)**<br>🚧 drift detection · building | **Work in progress, not yet running.** Phase 0 is complete: the infrastructure layer plus a hash-sealed frozen holdout with CI enforcing its invariants. The serving, monitoring, and training loop above it is not built yet, so there are no results to show. The design wires a drift score to an action rather than a dashboard, so a threshold breach will fire retraining and an automated champion challenger gate. | Python · PyTorch · MLflow · Airflow · Feast · Evidently |
| **[christiansantiago.dev](https://github.com/Go-Santiago-Go/christiansantiago.dev)**<br> | Private S3 bucket behind CloudFront OAC, all Terraform, deployed by push with no long-lived keys. The counter is one atomic `ADD`: 500 of 500 visits under concurrency, where read-then-write lost 498 silently. | Go · Lambda · DynamoDB · CloudFront · Terraform · OIDC |

## Background

Four years in an enterprise environment on infrastructure monitoring and incident response, and the
data engineering around it, working directly with the clients and stakeholders who depended on the
output, through a hybrid on-premise to AWS migration. Since then, systems integration, ETL pipelines,
BI reporting for leadership, and freelance application development. I reach for the smallest thing
that meets the requirement rather than the largest thing that impresses.

AWS Certified Developer, working toward AWS Certified Generative AI Developer Professional. Studied
computer science at Vanderbilt University and cloud engineering through the AWS Cloud Institute.
