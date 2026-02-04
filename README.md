### 🚀 Career CI/CD Pipeline

```mermaid
graph LR
    %% Define Nodes
    Source(Source: Learning) --> Build(Build: Projects)
    Build --> Test{Certifications}
    
    %% Decision Points
    Test -- Passed --> Deploy[Deploy: Experience]
    Test -- Failed --> Debug(Debug: Re-Learn)
    Debug --> Build
    
    %% Deploy Stage splits into roles
    Deploy --> Ops[Role: SysAdmin]
    Deploy --> DevOps[Role: DevOps Engineer]
    
    %% Current Status
    DevOps --> Monitor((Monitor: Current State))

    %% Styling
    style Source fill:#1f2020,stroke:#64ffda,stroke-width:2px,color:#fff
    style Build fill:#1f2020,stroke:#64ffda,stroke-width:2px,color:#fff
    style Test fill:#1f2020,stroke:#e06c75,stroke-width:2px,color:#fff
    style Debug fill:#1f2020,stroke:#e06c75,stroke-dasharray: 5 5,color:#fff
    style Deploy fill:#1f2020,stroke:#c678dd,stroke-width:2px,color:#fff
    style DevOps fill:#64ffda,stroke:#333,stroke-width:2px,color:#000
    style Monitor fill:#e06c75,stroke:#333,stroke-width:4px,color:#fff

### 🛠️ My DevOps Workflow

```mermaid
flowchart TD
    %% Nodes
    Dev[Developer] -->|Git Push| Repo[GitHub / GitLab]
    Repo -->|Webhook| CI[CI Server: Jenkins/Actions]
    
    subgraph CI_Process [Continuous Integration]
    CI -->|Build| Docker[Docker Image]
    CI -->|Test| Sonar[SonarQube]
    end
    
    subgraph CD_Process [Continuous Deployment]
    Docker -->|Push| Registry[Docker Hub/ECR]
    Registry -->|Pull| K8s[Kubernetes Cluster]
    end
    
    K8s -->|Monitor| Grafana[Grafana / Prometheus]
    Grafana -->|Alert| Dev
    
    %% Styling
    classDef plain fill:#fff,stroke:#333,stroke-width:1px,color:#000;
    classDef k8s fill:#326ce5,stroke:#fff,stroke-width:2px,color:#fff;
    classDef ci fill:#e06c75,stroke:#333,stroke-width:2px,color:#fff;
    
    class K8s k8s;
    class CI,Docker,Sonar ci;
    class Dev,Repo,Registry,Grafana plain;


