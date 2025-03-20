# SRE TRAINING (DAY 25) - Toil & Kubernetes Monitoring with Prometheus and Grafana

## **Toil in Site Reliability Engineering (SRE)**
In today's session, we explored the concept of **toil** in SRE, which encompasses repetitive, manual, and automatable operational work that provides minimal long-term value. This includes tasks such as manually restarting services, repeatedly responding to the same alerts, and conducting routine deployments without automation. SRE's primary goal is to minimize toil through automation, enabling engineers to focus on higher-value activities that enhance system reliability and efficiency.

---

## **Prometheus and Grafana Overview**
We also studied **Prometheus** and **Grafana**, two critical tools for monitoring and observability in Kubernetes environments:

### **Prometheus**
- A monitoring system that gathers and stores metrics as time-series data.
- Utilizes **PromQL** for querying and analyzing metrics.
- Collects metrics from configured endpoints such as Kubernetes pods and services.

### **Grafana**
- A visualization tool for creating dashboards from data sources like Prometheus.
- Enables users to configure real-time alerts and notifications.
- Compatible with multiple data sources, including **Loki** for log aggregation.

---

## **Execution of the Kubernetes Monitoring Setup**
Today, I implemented a script to establish Kubernetes monitoring using **Minikube, Prometheus, Loki, and Grafana**. The process involved:

### **1. Minikube Setup**
- Started Minikube with Docker as the driver, allocating **2 CPUs and 3GB RAM**.
- Confirmed that the Kubernetes cluster was operational and ready.
  ![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/minikube.png)

### **2. Deploying a Sample Logging Application**
- Established a `sample-app` namespace in Kubernetes.
- Deployed a **BusyBox-based logger** application that produces **INFO, DEBUG, and ERROR logs**.
- The application continuously generates log messages to replicate real-world workloads.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/namespace.png)

### **3. Installing Prometheus**
- Added the **Prometheus Helm repository** and updated it.
- Created a `monitoring` namespace and installed **Prometheus** with minimal resource configurations.
- Verified Prometheus was functioning properly and collecting Kubernetes metrics.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/prometheus.png)

### **4. Installing Loki for Log Aggregation**
- Installed **Loki** using Helm to gather logs from the `sample-app` namespace.
- Configured Loki for efficient log storage and retrieval.
  ![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/loki.png)

### **5. Installing Grafana**
- Installed **Grafana** with **Prometheus and Loki** as pre-configured data sources.
- Set up the admin password and enabled dashboards for log visualization.
- Confirmed that Grafana was operational and accessible.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/grafana.png)

### **6. Accessing Grafana and Importing Dashboards**
- Employed **port-forwarding** to make Grafana available at `http://localhost:3000`.
- Accessed Grafana using `admin/admin` credentials.
- Imported a dashboard to visualize **application logs and resource metrics**.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/port-forwarding.png)
---

## **Grafana Dashboard Creation**
After establishing the monitoring infrastructure, I manually created a **Grafana dashboard** to visualize Kubernetes logs and metrics.

- Launched Grafana and navigated to **Dashboards > Create a new dashboard**.
- Added a **Logs Panel** using **Loki** as the data source.
- Utilized the query `{namespace="sample-app"}` to fetch logs.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/app_logs.png)
- Added another panel for **filtered error logs** using the query `{namespace="sample-app"} |= "ERROR"`.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/error_logs.png)
- Set up a **CPU Usage Panel** using **Prometheus**.
  - Employed the query `sum(rate(container_cpu_usage_seconds_total{namespace="sample-app"}[5m])) by (pod)`.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/cpu_usage.png)
- Created a **Log Volume Panel** to monitor logs over time.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/log_volume.png)
- Modified dashboard settings, including **refresh rate (5s)** and **default time range (Last 15 minutes)**.
![](https://github.com/bhoomikaushik/notes/tree/main/Week6/Images/settings.png)
- Saved the dashboard for ongoing monitoring.

The monitoring setup was completed successfully, providing real-time visibility into application logs and system performance.
