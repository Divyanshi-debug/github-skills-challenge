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

## TASK:3 Identify Anomalies

The anomaly detection logic in [src/anomaly_detector.py](src/anomaly_detector.py) flags an observation when response time, CPU, or memory exceed the configured thresholds, or when the log level is `ERROR`.

### Anomalies detected

The anomalous records are the entries at:

- `2026-09-20T10:05:00`
- `2026-09-20T10:06:00`

These records were flagged because:

- response time reached 610ms and 640ms
- CPU usage reached 75% and 94%
- memory usage reached 70% and 91%
- the log level was `ERROR`
- the messages reported payment and database timeouts

### Normal vs anomalous observations

The earlier records are normal because they show stable latency, moderate resource use, and successful `INFO` log messages. The later records are clearly anomalous because they combine elevated resource usage with error-level log events.

### Detection limitation

The current detection approach uses fixed thresholds. That works well for this dataset, but it may not adapt to normal workload variation in a real environment. A more robust approach would compare values against historical baselines or dynamic thresholds.

## TASK:4 Verify AIOps Event Flow

The complete event flow in this repository is:

Operational Data → Anomaly Detection → Event → Producer → Topic → Consumer → AIOps

### Component roles

- `Producer`: creates and sends anomaly events
- `Topic`: the in-memory queue that stores published events
- `Consumer`: reads events from the topic and passes them downstream
- `Event/message`: the structured anomaly payload with service, timestamp, type, and reasons

### Workflow result

Running the project workflow shows that the event flow works end-to-end:

```text
==================================================
AIOps Pipeline Result
==================================================
Records processed: 10
Anomalies detected: 2
Events consumed: 2
```

The pipeline produces two anomaly events for the payment service, and the final output clearly identifies the issue.

## TASK:5 Investigate and Correct the Workflow

I identified and corrected two issues within the existing architecture:

1. Topic mismatch in the pipeline
   - Affected component: [src/aiops_pipeline.py](src/aiops_pipeline.py)
   - Cause: the producer and consumer were using different in-memory topics, so events were published and consumed from separate queues.
   - Correction: both components now share the same `EventTopic`.

2. Incorrect log-level detection
   - Affected component: [src/anomaly_detector.py](src/anomaly_detector.py)
   - Cause: the detector was checking for `WARNING`, but the dataset uses `ERROR` for real incidents.
   - Correction: the detector now checks for `ERROR` and includes the relevant reason in the event.

### Final corrected workflow execution

The final run of the workflow showed:

```text
Records processed: 10
Anomalies detected: 2
Events consumed: 2
```

The output included the following anomalies:

- `2026-09-20T10:05:00` — High response time, Error log detected
- `2026-09-20T10:06:00` — High response time, High CPU utilization, High memory utilization, Error log detected

This confirms the event flow works correctly and the final AIOps output reflects the detected issue.

## TASK:7 Reproduction steps

To reproduce this demonstration, follow these steps:

1. Open the repository in a Codespace or local terminal.
2. Change into the project directory:

```bash
cd /workspaces/github-skills-challenge
```

3. Run the pipeline:

```bash
python src/aiops_pipeline.py
```

4. Observe the output. The script will process the operational data, detect anomalies, publish them to the topic, consume them, and print the final AIOps result.
5. If you want to run the project tests, use:

```bash
python -m pytest -q
```

### Summary

This project models a payment service that becomes unstable under heavy load, produces timeout errors, and triggers performance-related anomalies. The AIOps workflow reads the operational telemetry, detects abnormal behavior, emits events to a topic, and consumes those events to produce a readable downstream report. The corrected flow successfully demonstrates the complete operational monitoring pipeline.

---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)