## Problems
* 99% Mem usage
* Separate the problem:
  - High mem, low cpu:
    + NGINX Memory Leak or High Buffer Allocation (1)
    + High Traffic Causing Excessive Open Connections (2)
  - High mem, high cpu:
    + NGINX Overloaded by High Traffic (Legitimate Load) (3)
    + NGINX Under DDoS or Bot Attack (4)
    + NGINX Memory Leak or Configuration Misuse (5)

## Solutions
* Issue (1):
  - Possible Cause:
    + Large buffer settings consuming excessive memory.
    + A module or an NGINX bug causing a memory leak.
    + Improper caching causing excessive in-memory objects.
  - Impact
    + System slowdown and eventual out-of-memory (OOM) crashes.
    + NGINX may become unresponsive while still using low CPU.
    + If swap usage is high, performance degrades due to swap thrashing.
  - solve:
    + Optimize NGINX Buffering Settings Reduce memory-intensive buffering
    + Limit Keep-Alive Requests
    + Flush Old Connections

* Issue (2):
  - Possible Cause:
    + NGINX is handling a very high number of concurrent connections.
    + Too many idle keep-alive connections consuming memory.
    + Requests with large headers or bodies leading to excessive buffering.
  - Impact
    + NGINX memory usage stays high, even when CPU remains low.
    + Incoming connections may start getting dropped.
    + If the system runs out of memory (OOM), it can crash.
  - solve:
    + Set Connection Limits
    + Enable Connection Rate Limiting

* Issue (3):
  - Possible Cause:
    + A huge traffic spike is overwhelming the VM.
    + Too many concurrent requests, keep-alive connections, or large files being served.
  - Impact
    + High memory usage due to request buffering
    + High CPU usage due to excessive SSL/TLS handshakes, request processing, and logging.
    + Slow response times, increased latencies, or request failures.
  - solve:
    + Limit Keep-Alive & Connections
    + Enable Rate Limiting
    + Reduce Buffer Sizes
    + Enable Caching

* Issue (4):
  - Possible Cause:
    + Attackers sending malicious traffic, overloading NGINX.
    + A large number of fake connections, POST requests, or high-rate requests.
    + Slowloris attacks keeping connections open indefinitely.
  - Impact
    + High CPU usage due to processing requests.
    + High memory usage due to holding open connections
    + System may crash, causing downtime.
  - solve:
    + Check for Unusual IP Traffic
    + Block Suspicious IPs
    + Enable Rate Limiting
    + Use AWS WAF or Cloudflare for Protection

* Issue (5):
  - Possible Cause:
    + Misconfigured worker_processes or cache settings.
    + NGINX holding too many connections open.
    + A memory leak in an NGINX module.
  - Impact
    + High memory usage grows over time.
    + High CPU due to excessive processing.
    + Crashes due to OOM killer.
  - solve:
    + Optimize Worker Processes

## Monitoring
+ Utilize Prometheus and Grafana to monitor and alert for abnormal traffic
+ Use the ELK stack to trace unusual IP addresses in logs
