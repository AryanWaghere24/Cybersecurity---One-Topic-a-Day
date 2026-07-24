# Day 55 - Container Security (Docker/Kubernetes)

## What It Is
Container Security covers the attack surface introduced by containerized application deployments — primarily Docker containers and Kubernetes orchestration. Containers have become the standard way to deploy cloud applications, and their unique architecture introduces specific security risks: container escapes, misconfigured Kubernetes clusters, exposed Docker APIs, and privilege escalation paths that differ significantly from traditional virtual machine security. A single misconfigured container can give an attacker access to the underlying host, to other containers, or to the entire Kubernetes cluster.

## How It Works
Containers share the host OS kernel — unlike virtual machines which have fully isolated kernels. This shared kernel model creates unique attack paths that don't exist in traditional virtualization.

```
Key container attack vectors:

1. Privileged Container Escape
Running a container with --privileged flag gives it full host access
Container can mount the host filesystem and escape entirely

# Privileged container escape example
docker run --privileged -it ubuntu bash
# Inside the privileged container:
mount /dev/sda1 /mnt    # mount host disk
chroot /mnt             # change root to host filesystem
# Now operating directly on the host OS

2. Exposed Docker Socket
If /var/run/docker.sock is mounted inside a container
The container can control the Docker daemon directly
Can create new privileged containers to escape to host

# Exploiting mounted Docker socket
ls /var/run/docker.sock  # check if socket is mounted
docker -H unix:///var/run/docker.sock run --privileged \
  -v /:/host ubuntu chroot /host

3. Kubernetes Misconfiguration
Default service account tokens mounted in every pod
If a pod is compromised, attacker uses the token to query Kubernetes API
Can list secrets, create privileged pods, or access other namespaces

# Check if pod has API access
curl -k https://kubernetes.default.svc/api \
  -H "Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)"

4. Exposed Kubernetes Dashboard
kubectl proxy running without authentication
Dashboard accessible publicly without login
Attacker can deploy containers, read secrets, and control the cluster

5. Secrets in Environment Variables
Sensitive values (API keys, passwords) passed as environment variables
Accessible to any process inside the container
Exposed in Docker inspect output, Kubernetes pod specs, and logs
```

## Real-World Example
In 2018 Tesla's Kubernetes infrastructure was compromised through a misconfigured Kubernetes dashboard that was exposed to the internet without authentication. Attackers accessed the dashboard, found AWS credentials stored in Kubernetes secrets, and used those credentials to access Tesla's AWS environment. They then deployed cryptocurrency mining software across Tesla's cloud infrastructure — running their mining operation on Tesla's compute budget. The entry point was a single Kubernetes dashboard exposed without a password, a misconfiguration that took minutes to exploit and gave access to an entire cloud environment.

## Why It Matters
From an attacker's side, containers are often deployed with excessive privileges or misconfigurations that make escaping to the host or accessing cluster-wide resources straightforward. Kubernetes clusters with exposed APIs or dashboards are actively scanned and attacked — automated tools continuously probe for exposed Kubernetes instances.

From a defender's side, never run containers with --privileged unless absolutely necessary. Never mount the Docker socket inside containers. Use Kubernetes RBAC (Role Based Access Control) to limit what service accounts can do. Disable automounting of service account tokens in pods that don't need API access. Run containers as non-root users. Use Pod Security Standards to enforce security policies across the cluster. Regularly scan container images for vulnerabilities using tools like Trivy.

## Key Terms
- Container Escape: breaking out of a container's isolation to access the underlying host OS or other containers
- Privileged Container: a Docker container running with --privileged flag giving it full access to the host's devices and capabilities
- Docker Socket: the Unix socket used to communicate with the Docker daemon — mounting it inside a container gives container-to-host control
- Kubernetes RBAC: Role Based Access Control system controlling what actions service accounts and users can perform in a Kubernetes cluster
- Pod Security Standards: Kubernetes policies enforcing security requirements on pods — restricting privileged containers, host mounts, and dangerous capabilities

## One Tip / Tool

Tool: `Trivy` for container image scanning and `kube-bench` for Kubernetes security auditing

```bash
# Trivy - scan a container image for vulnerabilities and misconfigurations
trivy image ubuntu:latest
trivy image --severity HIGH,CRITICAL nginx:1.21

# kube-bench - check Kubernetes cluster against CIS benchmarks
kubectl apply -f https://raw.githubusercontent.com/aquasecurity/kube-bench/main/job.yaml
kubectl logs job/kube-bench

# check for privileged containers running in your cluster
kubectl get pods --all-namespaces -o json | \
  jq '.items[] | select(.spec.containers[].securityContext.privileged==true) | .metadata.name'

# check for pods with Docker socket mounted
kubectl get pods --all-namespaces -o json | \
  jq '.items[] | select(.spec.volumes[]?.hostPath.path=="/var/run/docker.sock") | .metadata.name'

# Falco - runtime security tool that detects container escape attempts in real time
# alerts when a container tries to access host paths, spawn shells, or modify system files
```

Practice container security on **KubeGoat** — a deliberately vulnerable Kubernetes environment with realistic attack scenarios including container escapes, RBAC misconfigurations, and exposed secrets, designed specifically for learning Kubernetes security in a legal lab environment.
