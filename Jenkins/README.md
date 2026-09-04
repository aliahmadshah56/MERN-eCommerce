# Jenkins CI/CD Pipeline

This repository uses **Jenkins CI/CD pipelines** to automate Docker image build, push, and Kubernetes manifest updates.

## Pipeline Flow

```text
Developer
   ↓
GitHub
   ↓
Jenkins CI Pipeline
   ↓
Build Docker Images
   ↓
Push Images to Docker Hub
   ↓
Trigger Jenkins CD Pipeline
   ↓
Update Kubernetes Image Tags
   ↓
Commit & Push Changes to GitHub
   ↓
ArgoCD / Kubernetes
```

## Jenkins Shared Library

The CI pipeline uses a Jenkins Shared Library:

```groovy
@Library('Shared') _
```

The shared library contains reusable functions such as:

* `gitclone()`
* `docker_build()`
* `docker_push()`

Example:

```groovy
docker_build(
    imageName: "aliahmadshah/mern-ecommerce-backend",
    imageTag: params.BACKEND_DOCKER_TAG,
    dockerfile: "backend/Dockerfile",
    context: "."
)
```

### Configure Shared Library

In Jenkins:

```text
Manage Jenkins
→ System
→ Global Pipeline Libraries
→ Add
```

Configure:

```text
Name: Shared
Default Version: main
Retrieval Method: Modern SCM
Source Code Management: Git
Repository URL: <Your Shared Library Repository>
```

## Jenkins Credentials

Create the following credentials:

```text
Manage Jenkins
→ Credentials
→ System
→ Global Credentials
→ Add Credentials
```

| Credential ID     | Type                        | Purpose                  |
| ----------------- | --------------------------- | ------------------------ |
| `github-creds`    | Username & Password / Token | GitHub repository access |
| `dockerhub-creds` | Username & Password         | Docker Hub login         |

Use the same Credential ID in your Jenkins pipeline.

Example:

```groovy
withCredentials([
    usernamePassword(
        credentialsId: 'github-creds',
        usernameVariable: 'GITHUB_USERNAME',
        passwordVariable: 'GITHUB_TOKEN'
    )
]) {
    // GitHub authentication
}
```

## CI Pipeline

The CI pipeline:

1. Validates Docker image tags.
2. Cleans the Jenkins workspace.
3. Clones the GitHub repository.
4. Builds backend and frontend Docker images.
5. Pushes images to Docker Hub.
6. Triggers the CD pipeline.

Required parameters:

```text
FRONTEND_DOCKER_TAG
BACKEND_DOCKER_TAG
```

## CD Pipeline

The CD pipeline:

1. Validates Docker image tags.
2. Cleans the workspace.
3. Checks out the GitHub repository.
4. Updates backend Kubernetes image tag.
5. Updates frontend Kubernetes image tag.
6. Commits the changes.
7. Pushes the updated manifests to GitHub.

## Jenkins Jobs

```text
g-mern-ci
    ↓
g-mern-cd
```

The CI pipeline automatically triggers the CD pipeline after a successful Docker image build and push.

## Author

**Ali Ahmad Shah**
DevOps & Cloud Enthusiast
# Jenkins CI/CD Pipeline

This repository uses **Jenkins CI/CD pipelines** to automate Docker image build, push, and Kubernetes manifest updates.

## Pipeline Flow

```text
Developer
   ↓
GitHub
   ↓
Jenkins CI Pipeline
   ↓
Build Docker Images
   ↓
Push Images to Docker Hub
   ↓
Trigger Jenkins CD Pipeline
   ↓
Update Kubernetes Image Tags
   ↓
Commit & Push Changes to GitHub
   ↓
ArgoCD / Kubernetes
```

## Jenkins Shared Library

The CI pipeline uses a Jenkins Shared Library:

```groovy
@Library('Shared') _
```

The shared library contains reusable functions such as:

* `gitclone()`
* `docker_build()`
* `docker_push()`

Example:

```groovy
docker_build(
    imageName: "aliahmadshah/mern-ecommerce-backend",
    imageTag: params.BACKEND_DOCKER_TAG,
    dockerfile: "backend/Dockerfile",
    context: "."
)
```

### Configure Shared Library

In Jenkins:

```text
Manage Jenkins
→ System
→ Global Pipeline Libraries
→ Add
```

Configure:

```text
Name: Shared
Default Version: main
Retrieval Method: Modern SCM
Source Code Management: Git
Repository URL: <Your Shared Library Repository>
```

## Jenkins Credentials

Create the following credentials:

```text
Manage Jenkins
→ Credentials
→ System
→ Global Credentials
→ Add Credentials
```

| Credential ID     | Type                        | Purpose                  |
| ----------------- | --------------------------- | ------------------------ |
| `github-creds`    | Username & Password / Token | GitHub repository access |
| `dockerhub-creds` | Username & Password         | Docker Hub login         |

Use the same Credential ID in your Jenkins pipeline.

Example:

```groovy
withCredentials([
    usernamePassword(
        credentialsId: 'github-creds',
        usernameVariable: 'GITHUB_USERNAME',
        passwordVariable: 'GITHUB_TOKEN'
    )
]) {
    // GitHub authentication
}
```

## CI Pipeline

The CI pipeline:

1. Validates Docker image tags.
2. Cleans the Jenkins workspace.
3. Clones the GitHub repository.
4. Builds backend and frontend Docker images.
5. Pushes images to Docker Hub.
6. Triggers the CD pipeline.

Required parameters:

```text
FRONTEND_DOCKER_TAG
BACKEND_DOCKER_TAG
```

## CD Pipeline

The CD pipeline:

1. Validates Docker image tags.
2. Cleans the workspace.
3. Checks out the GitHub repository.
4. Updates backend Kubernetes image tag.
5. Updates frontend Kubernetes image tag.
6. Commits the changes.
7. Pushes the updated manifests to GitHub.

## Jenkins Jobs

```text
g-mern-ci
    ↓
g-mern-cd
```

The CI pipeline automatically triggers the CD pipeline after a successful Docker image build and push.


