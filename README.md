# GitHub Challenge

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey there!

Your challenge is ready.
Follow the instructions provided for this challenge and complete the required tasks in this repository.

Make sure your work is committed and pushed to your repository before submission.

Good luck!


---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

# GitHub Challenge


## TASK:1 Setup the project
## AIOps assessment scenario

This project simulates a payment service that is being monitored for performance and reliability. The service records transaction timing, CPU usage, memory usage, and log severity so operators can tell whether the system is behaving normally or starting to degrade.

### The operational problem

The main issue is that the payment service occasionally experiences slow responses, high resource usage, and error-level events. These symptoms can lead to failed or delayed payments, which affects the customer experience and increases operational risk. The team needs a way to spot these problems early and understand what is going wrong.

### Why AIOps matters here

AIOps helps connect live operational data with automated detection and event handling. In this assessment, telemetry is analyzed for anomalies, the relevant events are published to a topic, and the resulting signals are consumed to mimic how an operations pipeline would surface issues. The goal is to detect incidents faster, reduce manual investigation, and give the team more visibility into service health.

## TASK:2 Analyse Logs and Metrics


## Operational data analysis

The data in `data/service_data.json` contains a small set of synthetic service observations. Each record includes a timestamp, service name, performance metrics, and log details.

### 1. Metrics

The metric fields are:

- `response_time_ms`
- `cpu_percent`
- `memory_percent`

These values show how the service is performing at a given moment.

### 2. Log information

The log-related fields are:

- `log_level`
- `message`

These indicate whether the request was normal or if an error was reported, and provide context about what happened.

### 3. Timestamps

The `timestamp` field is used to order the events chronologically. It shows that the service stays stable at first and then begins to degrade over time.

### 4. Normal behavior

Normal observations have:

- response times around 120ms to 150ms
- CPU usage around 40% to 60%
- memory usage around 50% to 57%
- `INFO` log entries
- messages saying the payment request was processed successfully

### 5. Unusual behavior

The unusual observations occur later in the dataset, when:

- response times rise to 610ms and 640ms
- CPU reaches 75% and 94%
- memory reaches 70% and 91%
- the log level is `ERROR`
- messages mention timeouts

These records clearly indicate degraded service health and are the kind of incidents an AIOps workflow is meant to detect.