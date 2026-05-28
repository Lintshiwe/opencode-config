---
name: architecture-diagrams
description: Generate professional system architecture diagrams with real tech icons (AWS, databases, languages, containers, K8s) using the Python diagrams library. Use when the user asks for architecture diagrams, system design visuals, infrastructure maps, or component relationship charts with real provider icons.
---

# Architecture Diagrams with Real Tech Icons

Generate professional PNG architecture diagrams using the [Python `diagrams` library](https://diagrams.mingrammer.com/). Each node gets a real provider icon (PostgreSQL elephant, AWS Lambda, Docker whale, etc.).

## Installation & Prerequisites

```bash
pip3 install diagrams
# Requires graphviz (usually pre-installed): dot -V
```

## How It Works

```python
from diagrams import Diagram, Cluster, Edge
from diagrams.aws.compute import EC2          # AWS EC2 icon
from diagrams.onprem.database import PostgreSQL # PostgreSQL elephant icon
from diagrams.programming.language import Go    # Go gopher icon

with Diagram("My Architecture", show=False, direction="LR", outformat="png"):
    with Cluster("Backend"):
        api = EC2("API Server")
        db = PostgreSQL("Database")
    api >> Edge(label="query") >> db
```

Run: `python3 diagram.py` → produces `my_architecture.png`

## Icon Mapping — Which Icon Class to Use

### Databases
| Technology | Import | Class |
|---|---|---|
| PostgreSQL | `diagrams.onprem.database` | `PostgreSQL` |
| MySQL | `diagrams.onprem.database` | `MySQL` |
| MongoDB | `diagrams.onprem.database` | `MongoDB` |
| Cassandra | `diagrams.onprem.database` | `Cassandra` |
| Redis | `diagrams.onprem.database` | *(use Elasticache)* `diagrams.aws.database.ElastiCache` |
| SQLite / Generic | `diagrams.generic.database` | `SQL` |
| DynamoDB | `diagrams.aws.database` | `Dynamodb` |
| RDS | `diagrams.aws.database` | `RDS` |
| Aurora | `diagrams.aws.database` | `Aurora` |
| Elasticsearch | `diagrams.elastic.elasticsearch` | `Elasticsearch` |
| Neo4j | `diagrams.onprem.database` | `Neo4J` |
| CockroachDB | `diagrams.onprem.database` | `CockroachDB` |

### Programming Languages & Runtimes
| Technology | Import | Class |
|---|---|---|
| Go | `diagrams.programming.language` | `Go` |
| Python | `diagrams.programming.language` | `Python` |
| JavaScript | `diagrams.programming.language` | `Javascript` or `JavaScript` |
| TypeScript | `diagrams.programming.language` | `Typescript` or `TypeScript` |
| Node.js | `diagrams.programming.language` | `NodeJS` or `Nodejs` |
| Rust | `diagrams.programming.language` | `Rust` |
| Java | `diagrams.programming.language` | `Java` |
| Kotlin | `diagrams.programming.language` | `Kotlin` |
| Ruby | `diagrams.programming.language` | `Ruby` |
| PHP | `diagrams.programming.language` | `PHP` or `Php` |
| C/C++ | `diagrams.programming.language` | `C` / `Cpp` |
| C# | `diagrams.programming.language` | `Csharp` |
| Swift | `diagrams.programming.language` | `Swift` |
| Dart | `diagrams.programming.language` | `Dart` |
| Bash | `diagrams.programming.language` | `Bash` |
| Scala | `diagrams.programming.language` | `Scala` |
| R | `diagrams.programming.language` | `R` |

### Compute / Containers / Orchestration
| Technology | Import | Class |
|---|---|---|
| Docker | `diagrams.onprem.container` | `Docker` |
| Kubernetes Pod | `diagrams.k8s.compute` | `Pod` |
| K8s Deployment | `diagrams.k8s.compute` | `Deploy` or `Deployment` |
| K8s StatefulSet | `diagrams.k8s.compute` | `STS` or `StatefulSet` |
| K8s DaemonSet | `diagrams.k8s.compute` | `DS` or `DaemonSet` |
| K8s CronJob | `diagrams.k8s.compute` | `Cronjob` |
| Helm | `diagrams.k8s.ecosystem` | `Helm` |
| Kustomize | `diagrams.k8s.ecosystem` | `Kustomize` |
| Containerd | `diagrams.onprem.container` | `Containerd` |
| Nomad | `diagrams.onprem.container` | `Nomad` |
| Generic Server | `diagrams.onprem.compute` | `Server` |
| Generic Compute | `diagrams.generic.compute` | `Rack` |

### AWS (selected key icons)
| Service | Import | Class |
|---|---|---|
| EC2 | `diagrams.aws.compute` | `EC2` |
| Lambda | `diagrams.aws.compute` | `Lambda` |
| ECS | `diagrams.aws.compute` | `ECS` |
| EKS | `diagrams.aws.compute` | `EKS` |
| Fargate | `diagrams.aws.compute` | `Fargate` |
| S3 (use generic storage) | `diagrams.generic.storage` | `Storage` |
| CloudFront (CDN) | `diagrams.aws.network` | `CloudFront` |
| API Gateway | `diagrams.aws.network` | `APIGateway` |
| ELB/ALB | `diagrams.aws.network` | `ELB` |
| Route53 | `diagrams.aws.network` | `Route53` |
| VPC | `diagrams.aws.network` | `VPC` |
| SQS | `diagrams.aws.integration` | `SQS` |
| SNS | `diagrams.aws.integration` | `SNS` |
| EventBridge | `diagrams.aws.integration` | `Eventbridge` |
| Step Functions | `diagrams.aws.integration` | `StepFunctions` |
| Cognito | `diagrams.aws.security` | `Cognito` |
| IAM | `diagrams.aws.security` | `IAM` |
| KMS | `diagrams.aws.security` | `KMS` |
| Secrets Manager | `diagrams.aws.security` | `SecretsManager` |
| CloudWatch | `diagrams.aws.management` | `Cloudwatch` |

### CI/CD & DevOps
| Technology | Import | Class |
|---|---|---|
| GitHub Actions | `diagrams.onprem.ci` | `GithubActions` |
| GitLab CI | `diagrams.onprem.ci` | `GitlabCI` |
| Jenkins | `diagrams.onprem.ci` | `Jenkins` |
| CircleCI | `diagrams.onprem.ci` | `CircleCI` |
| ArgoCD | `diagrams.onprem.gitops` | `Argocd` |
| Flux | `diagrams.onprem.gitops` | `Flux` |
| Terraform | `diagrams.onprem.iac` | `Terraform` |
| Ansible | `diagrams.onprem.iac` | `Ansible` |
| Puppet | `diagrams.onprem.iac` | `Puppet` |

### Monitoring & Logging
| Technology | Import | Class |
|---|---|---|
| Grafana | `diagrams.onprem.monitoring` | `Grafana` |
| Prometheus | `diagrams.onprem.monitoring` | `Prometheus` |
| Datadog | `diagrams.onprem.monitoring` | `Datadog` |
| Sentry | `diagrams.onprem.monitoring` | `Sentry` |
| Splunk | `diagrams.onprem.monitoring` | `Splunk` |
| New Relic | `diagrams.onprem.monitoring` | `Newrelic` |
| ELK (Elastic) | `diagrams.elastic.elasticsearch` | See elastic category |

### Messaging & Streaming
| Technology | Import | Class |
|---|---|---|
| Kafka | `diagrams.onprem.queue` | `Kafka` |
| RabbitMQ | `diagrams.onprem.queue` | `RabbitMQ` or `Rabbitmq` |
| NATS | `diagrams.onprem.queue` | `Nats` |
| Celery | `diagrams.onprem.queue` | `Celery` |
| ZeroMQ | `diagrams.onprem.queue` | `ZeroMQ` |

### API & Networking
| Technology | Import | Class |
|---|---|---|
| Nginx | `diagrams.onprem.network` | `Nginx` |
| Apache | `diagrams.onprem.network` | `Apache` |
| HAProxy | `diagrams.onprem.network` | `HAProxy` or `Haproxy` |
| Envoy | `diagrams.onprem.network` | `Envoy` |
| Traefik | `diagrams.onprem.network` | `Traefik` |
| Kong | `diagrams.onprem.network` | `Kong` |
| Istio | `diagrams.onprem.network` | `Istio` |
| Consul | `diagrams.onprem.network` | `Consul` |
| etcd | `diagrams.onprem.network` | `ETCD` or `Etcd` |

### SaaS & External
| Technology | Import | Class |
|---|---|---|
| GitHub | `diagrams.saas.social` | `Github` |
| GitLab | `diagrams.saas.social` | `Gitlab` |
| Slack | `diagrams.saas.chat` | `Slack` |
| Discord | `diagrams.saas.chat` | `Discord` |
| Auth0 | `diagrams.saas.identity` | `Auth0` |
| Okta | `diagrams.saas.identity` | `Okta` |
| Cloudflare | `diagrams.saas.cdn` | `Cloudflare` |
| Snowflake | `diagrams.saas.analytics` | `Snowflake` |

### Generic (fallback when specific icon unavailable)
| Concept | Import | Class |
|---|---|---|
| User/Client | `diagrams.onprem.client` | `User` / `Users` |
| Database | `diagrams.generic.database` | `SQL` |
| Storage | `diagrams.generic.storage` | `Storage` |
| Compute | `diagrams.generic.compute` | `Rack` |
| Mobile Device | `diagrams.generic.device` | `Mobile` |
| Tablet | `diagrams.generic.device` | `Tablet` |
| Firewall | `diagrams.generic.network` | `Firewall` |
| Router | `diagrams.generic.network` | `Router` |
| VPN | `diagrams.generic.network` | `VPN` |

## Styling Best Practices

### Dark Theme (recommended for presentations)
```python
graph_attr = {
    "fontsize": "22", "bgcolor": "#0D1117",
    "splines": "spline", "pad": "1.0",
    "nodesep": "0.8", "ranksep": "1.2",
}
node_attr = {
    "fontsize": "12", "fontcolor": "#E6EDF3",
    "penwidth": "2.5",
}
edge_attr = {
    "color": "#58A6FF", "fontcolor": "#8B949E",
    "fontsize": "9", "penwidth": "1.5",
}
```

### Edge Colors for Meaning
```python
# Success flow
api >> Edge(color="#3FB950", style="bold") >> db
# Async / batch
job >> Edge(color="#D2A8FF", style="dashed") >> queue
# Read path
cache >> Edge(color="#79C0FF") >> api
# Error / warning
svc >> Edge(color="#F85149", style="dotted") >> alert
```

## Layout Strategies

| Direction | Best for |
|---|---|
| `LR` (left-right) | Request flow, data pipelines, layered architecture |
| `TB` (top-bottom) | Infrastructure, deployment views, multi-tier |
| `RL` (right-left) | Mirror of LR for RTL contexts |
| `BT` (bottom-up) | Data flow upward, event sourcing |

### Using Clusters for Grouping
```python
with Cluster("Frontend Layer"):
    web = Javascript("Next.js")
    mobile = Swift("iOS App")

with Cluster("Backend Layer"):
    api = Go("API Gateway")
    workers = Python("Workers")

with Cluster("Data Layer"):
    primary = PostgreSQL("Primary DB")
    cache = Elasticache("Redis Cache")

web >> api >> primary
api >> cache
```

## Template: Generate Diagram for Any Project

```python
from diagrams import Diagram, Cluster, Edge
# Add project-specific imports here

graph_attr = {"fontsize": "22", "bgcolor": "#0D1117", "splines": "spline"}
node_attr = {"fontsize": "12", "fontcolor": "#E6EDF3", "penwidth": "2.5"}
edge_attr = {"color": "#58A6FF", "fontcolor": "#8B949E", "penwidth": "1.5"}

with Diagram(
    "Project Architecture",
    filename="architecture",
    show=False,
    direction="LR",
    graph_attr=graph_attr,
    node_attr=node_attr,
    edge_attr=edge_attr,
    outformat="png",
):
    user = User("User/Client")

    with Cluster("Application"):
        # Add components here
        pass

    with Cluster("Data"):
        # Add databases here
        pass

    with Cluster("Infrastructure"):
        # Add infra here
        pass

    # Add edges
    # component_a >> Edge(label="explanation") >> component_b

print("Saved: architecture.png")
```

## Verification

After generating, check:
```bash
file architecture.png    # Should show: PNG image data, ...
ls -lh architecture.png  # If >2MB, reduce complexity or DPI
```

If image won't render in viewer:
- Reduce cluster nesting depth
- Use `direction="LR"` instead of `TB` for wide layouts  
- Keep total nodes under ~25
- Omit unnecessary edges
- Use 72 DPI if needed: add `"dpi": "72"` to graph_attr

## Anti-Patterns

- Don't use `Custom()` with file paths unless icon exists on disk
- Don't nest more than 3 levels of Clusters
- Don't connect nodes inside Cluster via list indices — use direct node references
- Don't forget to call `print()` at end to confirm completion
- Don't import from modules without checking exact class names first (`GithubAction` vs `GithubActions`)
