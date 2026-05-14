# 🚀 Teams-Operator

A template for plattform container-practices

## Deployment of the operator

# Apply the operator manifests (creates RBAC, namespace, and deployment)

```shell
kubectl apply -f operator-deployment.yaml
```

# Verify the operator pod is running

```shell
kubectl get pods -n engineering-platform -l app=teams-operator
```

# Expected output

```shell
# NAME                              READY   STATUS    RESTARTS   AGE
# teams-operator-xxxxxxxxxx-xxxxx   1/1     Running   0          30s
```

# Watch the operator logs to see it polling and reconciling

```shell
kubectl logs -f deployment/teams-operator -n engineering-platform
```

# Now create a team via the API (in a separate terminal)

```shell
curl -X POST "<http://localhost:8080/teams>" \
  -H "Content-Type: application/json" \
  -d '{"name": "Platform Team"}'
```

# After the next poll cycle (up to 30 seconds), the operator log should show

```shell
# ✅ Created namespace 'team-platform-team' for team 'Platform Team'
```

# Verify the namespace was created

```shell
kubectl get namespace team-platform-team --show-labels
```
