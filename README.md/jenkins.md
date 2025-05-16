# DevOps Troubleshooting Log

A personal log of errors I've encountered while working on DevOps projects; building multibranch pipelines etc 

---

## Error 1: Docker Daemon Permission Denied

**Error Message:**
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock
**Cause:**
Jenkins (inside a Docker container) does not have permission to access the Docker daemon socket on the host machine.
**solution:**
sudo chown root:docker /var/run/docker.sock
sudo chmod 666 /var/run/docker.sock

