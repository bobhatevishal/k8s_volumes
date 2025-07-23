# Kubernetes PVC + Liveness + Rolling Update Demo 🚀

This project demonstrates how to:
- Use Persistent Volume and Persistent Volume Claim (PV & PVC)
- Mount PVC into a Deployment using `initContainers` and shared storage
- Configure **liveness** and **readiness** probes in containers
- Perform **rolling updates** and **manual rollback**
- Scale pods manually using `kubectl scale`

---

## 🏗️ Kubernetes Resources Used

| Resource              | Purpose                                |
|-----------------------|----------------------------------------|
| PersistentVolume      | Static 1Gi volume on hostPath          |
| PersistentVolumeClaim | Claims the volume for deployment       |
| Deployment            | Runs Nginx containers with shared PVC  |
| InitContainer         | Writes a message to PVC before app runs|
| Liveness Probe        | Auto-restarts failed pods              |
| Readiness Probe       | Ensures pod is ready before traffic    |

---

## 📁 File Structure

```bash
.
├── pv.yml           # Static hostPath PersistentVolume
├── pvc.yml          # Claim for the PV
├── deployment.yml   # Main Deployment using PVC, probes
# Apply PV and PVC
kubectl apply -f pv.yml
kubectl apply -f pvc.yml

# Deploy the app
kubectl apply -f deployment.yml

# Rolling update example
kubectl set image deployment/my-app my-container=nginx:1.21 --record
kubectl rollout status deployment/my-app

# Rollback if needed
kubectl rollout undo deployment/my-app

# Manual scaling
kubectl scale deployment my-app --replicas=4
