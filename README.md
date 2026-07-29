# Christian Santiago

**Cloud and software engineer focused on AWS infrastructure, data pipelines, cost efficiency, and
service reliability.**

I came up through infrastructure monitoring, incident response, and the data engineering around it,
working directly with the clients and stakeholders who depended on the output, at scales from
enterprise down to small and mid-sized businesses. Lately I have been building AWS infrastructure in
Go, Python, and Terraform for generative AI and machine learning workloads, and MLOps is where I am
headed.

[christiansantiago.dev](https://christiansantiago.dev) ·
[Resume](https://christiansantiago.dev/resume.pdf) ·
[LinkedIn](https://www.linkedin.com/in/christian-santiago-dev/)

---

## What I am building

Four projects, each one a different seam of running a model in production: getting the context in,
serving the inference, training the next version, and the infrastructure practice underneath all of
it.

### [go-rag-api](https://github.com/Go-Santiago-Go/go-rag-api) · retrieval

A retrieval service in Go that makes documents searchable and answers questions against them. Text
is chunked and embedded with Bedrock Titan v2, vectors are stored in pgvector, and a query runs a
cosine similarity search for the nearest chunks before a model writes the answer. The platform half
is the point as much as the pipeline: a three-tier VPC with the database in a private subnet and no
public endpoint, a distroless container on ECS Fargate, and keyless CI to ECR over GitHub OIDC.
Storage and model calls sit behind Go interfaces, so the pipeline unit tests with no cloud access.

RDS is single-AZ on purpose. The network design is multi-AZ, and paying for a standby on a portfolio
workload buys resilience the project does not need. That tradeoff is the interesting part of the
decision, not an oversight.

**Stack:** Go · Bedrock · pgvector on RDS Postgres · ECS Fargate · Terraform · GitHub Actions

**Status:** deployed and verified end to end, torn down between sessions rather than left idle.

### [inference-gateway](https://github.com/Go-Santiago-Go/inference-gateway) · serving

A gateway in Go that sits in front of Bedrock and adds the operations layer raw Bedrock does not
have: token streaming over Server-Sent Events, per-key authentication and rate limiting, retries with
backoff and jitter, and per-request token and cost accounting in structured `slog` output. Every
cross-cutting concern is its own middleware, so each one tests in isolation and the handler stays
thin orchestration.

The request context threads from the handler through the Bedrock call, so a client disconnect cancels
the in-flight request instead of paying for tokens nobody reads. A React and TypeScript client
streams from it in the browser, which puts each of those behaviours on screen rather than only in a
log line.

**Stack:** Go · Bedrock ConverseStream · SSE · React and TypeScript · ECS Fargate · CloudFront ·
Terraform

**Status:** deployed and verified end to end. Streaming, cancellation, `401` on a bad key, and `429`
with an accurate `Retry-After` all confirmed against the live URLs.

### [retrain-pipeline](https://github.com/Go-Santiago-Go/retrain-pipeline) · training and governance

A continuous training loop for a scikit-learn model where bad data cannot merge and no model promotes
without a human reading the evaluation. New labeled data arrives as a pull request carrying a DVC
pointer rather than the data itself. Great Expectations validates it as a required check. On merge, a
Go CLI submits a SageMaker training job tagged with the dataset hash and the Git SHA, then registers
the result as `PendingManualApproval` with its metrics and lineage attached.

Data and code both enter through Git, validation gates the merge, and the registry gates promotion.
The trigger is CI-driven by design: there is no queue and no event bus, because nothing here needs
one.

**Stack:** Go · Python · scikit-learn · SageMaker · DVC · Great Expectations · Terraform · GitHub
Actions

**Status:** loop closed and demonstrated live. A failing batch was blocked at the gate, a passing
batch trained and registered as version 1, and a human approved it against the lineage.

### [christiansantiago.dev](https://github.com/Go-Santiago-Go/christiansantiago.dev) · this site

My personal site, built the Cloud Resume Challenge way. Static files on a private S3 bucket that
CloudFront reaches through Origin Access Control, every AWS resource in Terraform, and deploys that
happen by pushing to `main` with no long-lived AWS credentials anywhere. The visitor counter is a Go
Lambda on `provided.al2023` and arm64, writing to DynamoDB through a single `UpdateItem` with an
atomic `ADD`.

The atomicity is the whole design. Under 500 concurrent callers the atomic add recorded 500 of 500
visits, while a read-then-write version of the same fake recorded 2 and lost 498, silently, with no
error and a number that still went up. Init measures 91 ms and warm invocations return at a p50 of
5 ms, which puts the Go runtime at under 7% of the cold path.

**Stack:** Go · Lambda · DynamoDB · API Gateway · CloudFront · S3 · Route 53 · Terraform · GitHub
Actions with OIDC

**Status:** live, with the counter integration and CI hardening in progress.

---

## Background

Four years in an enterprise environment on infrastructure monitoring and incident response, and the
data engineering around it: thresholds and event-driven alert routing on the detection side,
telemetry pipelines and dimensional models on the side that turned resolved incidents into failure
patterns. All of it through a hybrid on-premise to AWS migration. Since then, systems integration,
ETL pipelines, BI reporting for leadership, and freelance application development.

The through line is system design. Good architecture has less to do with knowing services than with
asking what tradeoffs a decision is making, and being able to answer for them. Reliability against
cost, simplicity against flexibility, shipping now against unwinding it later. I reach for the
smallest thing that meets the requirement rather than the largest thing that impresses, treat those
decisions as revisable, and let telemetry rather than my own opinion say when one needs revisiting.
That habit came from presenting technical decisions to leadership and non-technical stakeholders,
who were never going to accept "because it is best practice" as an answer.

## Tools

- **Languages:** Go, Python, SQL, JavaScript and TypeScript
- **AWS:** Lambda, API Gateway, DynamoDB, S3, CloudFront, Route 53, ECS Fargate, RDS, SageMaker,
  Bedrock, IAM, CloudWatch
- **Infrastructure:** Terraform, Docker, GitHub Actions, OIDC federation

## Credentials

AWS Certified Developer, currently working toward AWS Certified Generative AI Developer
Professional. Studied computer science at Vanderbilt University and cloud engineering through the AWS
Cloud Institute. Sharpening the math through Math Academy's Mathematics for Machine Learning track,
alongside DataCamp and deeplearning.ai.

## Reach me

If your team is shipping generative AI or machine learning work and needs the systems around it
built and operated on AWS, that is the work I want.

[santiagothedeveloper@gmail.com](mailto:santiagothedeveloper@gmail.com) ·
[LinkedIn](https://www.linkedin.com/in/christian-santiago-dev/) ·
[christiansantiago.dev](https://christiansantiago.dev)
