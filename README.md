# argo-rollouts-demo

Example manifest demonstrating [Argo Rollouts](https://argoproj.github.io/argo-rollouts/) with Nginx Ingress Controller and Metric Analysis via Prometheus Service endpoint

## Deployment Strategies

1. **Canary Deployment**: Gradually shifts traffic from stable to new version
2. **Blue/Green Deployment**: Deploys new version alongside old version, then switches traffic
3. **Analysis with Prometheus**: Uses metrics to automatically validate deployments

## Project Structure

```
.
├── README.md
├── apps/                       # Application manifests
│   ├── rollouts-poc/           # Demo application with Ingress
├── argo-manifest               # Argo App resource
├── loadtest                    # K6 test scripts

```

### Managing Rollouts

#### Trigger a Rollout

```bash
# Update application image to trigger rollout
kubectl argo rollouts set image rollouts-poc-stable rollouts-demo=argoproj/rollouts-demo:green

# Watch rollout progress
kubectl argo rollouts get rollout rollouts-demo --watch
```

#### Promote a Rollout

```bash
# After verification, promote the rollout
kubectl argo rollouts promote rollouts-demo
```

## Important Notes

- **Please change the Ingress Host parameter and configmap in k6_dep.yaml file to target the Ingress endpoint in your cluster**
- **Analysis templates uses the Prometheus svc endpoint available inside your kubernetes cluster**
- **Pending Task**: Convert the manifest into Helm chart
