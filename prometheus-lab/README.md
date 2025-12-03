# LAB 1
# Monitoring with Prometheus 

## Objective
Monitor a Docker container using Prometheus

## Setup
- Docker container: nginx
- Prometheus container setup
- Metrics scrape and visualized 

## Steps
1. Install Prometheus
    [prometheus_setup.sh](/Modern-DevOps-Practices/ch2/prometheus/prometheus_setup.sh)
2. Configure Prometheus and Node Exporter
    [prometheus.yml](/prometheus-lab/prometheus.yml)
3. Pull and run cadvisor container
  ```bash
  docker run -d   --name cadvisor   --privileged   --restart always   -p 8080:8080   -v /:/rootfs:ro   -v /var/run:/var/run:rw   -v /sys:/sys:ro   -v /var/lib/docker/:/var/lib/docker:ro   -v /sys/fs/cgroup:/sys/fs/cgroup:ro   gcr.io/cadvisor/cadvisor:latest
  ```

4. Pull and run nginx container
    ```bash
    docker run -d --name webserver nginx
    ```
5. Access prometheus on browser at _http://localhost:9090_ and run commands to load and visualize metrics
```PromQL
container_memory_usage_bytes{name="webserver"}
node_cpu{instance="localhost:9100",job="node_exporter"}
```

## Results
- CAdvisor Web Interface
![cadvisor web interface](/prometheus-lab/Screenshots/cadvisor.png)
*Figure 1: cAdvisor dashboard showing container metrics.*

- Benchmark test 
```bash
ab -n 100000 http://localhost:8081/
```
![benchmark test](/prometheus-lab/Screenshots/benchmarking.png)
*Figure 2: Shell window showing benchmark test results.*

- Container Memory Usage
![container memory usage bytes](/prometheus-lab/Screenshots/container_memory_usage.png)
*Figure 3: Prometheus dashboard showing container memory usage* metrics.
![graph](/prometheus-lab/Screenshots/cmu_graph.png)
*Figure 4: Prometheus dashboard showing container memory usage graph.*

- Node CPU metrics
![node cpu metrics](/prometheus-lab/Screenshots/node_cpu.png)
*Figure 5: Prometheus dashboard showing node cpu metrics.*

## Learnings 
- How Prometheus scrapes metrics
- Container networking
- YAML configs


