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
2. Configure Promoetheus and Node Exporter
    [prometheus.yml](/prometheus-lab/prometheus.yml)
3. Pull and run cadvisor container
  _docker run -d   --name cadvisor   --privileged   --restart always   -p 8080:8080   -v /:/rootfs:ro   -v /var/run:/var/run:rw   -v /sys:/sys:ro   -v /var/lib/docker/:/var/lib/docker:ro   -v /sys/fs/cgroup:/sys/fs/cgroup:ro   gcr.io/cadvisor/cadvisor:latest_
4. Pull and run nginx container
    _docker run -d --name webserver nginx_
5. Access prometheus on browser and run commands to load and visualize metrics

## Results
- CAdvisor Web Interface
![cadvisor web interface](/prometheus-lab/Screenshots/cadvisor.png)

- Benchmark test _ab -n 100000 http://localhost:8081/_
![benchmark test](/Screenshots/benchmarking.png)

- Container Memory Usage
![container memory usage bytes](/prometheus-lab/Screenshots/container_memory_usage.png)
![graph](/prometheus-lab/Screenshots/cmu_graph.png)

- Node CPU metrics
![node cpu metrics](/prometheus-lab/Screenshots/node_cpu.png)

## Learnings 
- How Prometheus scrapes metrics
- Container networking
- YAML configs


