# Hi, I'm Christian Santiago 👋

**Go developer building and operating AI infrastructure on AWS.**

I'm a former business intelligence and data engineer. These days I focus on the engineering behind machine learning: sound system design plus the serving, scaling, and observability layer that turns a model call into something you can actually run in production. The system design matters to me as much as the ML does. I work mostly in Go, and reach for Python or TypeScript when they fit. I provision with Terraform and lean on solid system design (decoupled architectures, least-privilege IAM, observability and monitoring, and FinOps cost optimization) to build services that hold up under real traffic. Alongside the engineering, I'm working through Math Academy's [Mathematics for Machine Learning](https://www.mathacademy.com/courses/mathematics-for-machine-learning) to go deeper into ML, and enjoying it.

I came up through data. My first role was BI and data engineering in a hybrid-cloud manufacturing environment, where the data sat siloed across systems that were never meant to talk to each other. Pulling it together into something that answered a real business question is the work that got me hooked. From there I went deeper into software: freelance web and BI work for small and mid-sized businesses, an immersive at Codesmith, and 9 months at the AWS Cloud Institute learning cloud engineering directly from working Amazon engineers.

---

## 🚀 Featured projects

I built these two as one arc: build the AI capability first, then operate it like a production engineer.

### [inference-gateway](https://github.com/Go-Santiago-Go/inference-gateway) — LLM inference gateway (Go, AWS Bedrock)
A production-shaped gateway that adds the operational layer raw Bedrock lacks. It handles SSE token streaming, per-key API-key auth, per-key rate limiting, retries with backoff and jitter, and per-request cost accounting, all observable through structured logs. It's deployed on ECS Fargate with Terraform, and comes with a React and TypeScript client that makes every feature visible in the browser.

### [rag-api](https://github.com/Go-Santiago-Go/rag-api) — Retrieval-Augmented Generation service (Go, pgvector, AWS)
A full RAG pipeline over HTTP: chunking, Bedrock Titan v2 embeddings, pgvector similarity search, and grounded generation. It answers with citations back to the source (`{ answer, sources[] }`). Everything is infrastructure as code, with a multi-tier VPC in Terraform, keyless CI/CD to ECR over GitHub OIDC, and a distroless container on ECS Fargate.

> The two connect. The rag-api generation call is designed to sit behind inference-gateway, so the same Bedrock traffic gets rate-limited, retried, and cost-metered by the gateway.

---

## 🛠️ What I work with

**Languages:** Go, TypeScript, SQL, Python

**Cloud and infra:** AWS, serverless-first (ECS/Fargate, S3, CloudFront, RDS, Bedrock, Secrets Manager, SSM, ECR, CloudWatch, VPC, IAM), decoupled architectures, Terraform, Docker

**Practices:** CI/CD (GitHub Actions, OIDC), microservices, observability, infrastructure as code

**Data and AI:** data pipelines, RAG, vector search (pgvector), LLM serving, cost and token accounting

---

## 📚 Experience and credentials

- 🏭 BI and data engineering in a hybrid-cloud manufacturing environment
- 🧑‍💻 Freelance web development and business intelligence for small and mid-sized businesses
- 💻 [Codesmith](https://www.codesmith.io/): software engineering immersive
- 🏫 AWS Cloud Institute: 9 months of cloud engineering taught by working Amazon engineers
- ☁️ AWS Certified Developer
- 🎓 Studied Computer Science at Vanderbilt University

## 🌱 What I'm up to (July 2026)

- 💊 Building an AI document-intelligence prototype (OCR, LLMs, and RAG in Python) in Pfizer's [Advanced AI-Powered Document Intelligence Externship](https://www.extern.com/externships/pfizer-advanced-ai-powered-document-intelligence-externship-may-2026) on Extern
- 🧮 Sharpening the math with Math Academy's [Mathematics for Machine Learning](https://www.mathacademy.com/courses/mathematics-for-machine-learning) track
- 🧪 Working through the DataCamp [Machine Learning Scientist](https://www.datacamp.com/tracks/machine-learning-scientist-with-python) track and applying it to personal projects
- 📜 Studying for the [AWS Certified Generative AI Developer, Professional](https://aws.amazon.com/certification/certified-generative-ai-developer-professional/) (AIP-C01)

---

## 📫 Connect

- 💼 LinkedIn: [christian-santiago-dev](https://www.linkedin.com/in/christian-santiago-dev/), where I post about what I'm learning
