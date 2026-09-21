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

## AIOps assessment scenario

This project simulates a payment service that is being monitored for performance and reliability. The service records transaction timing, CPU usage, memory usage, and log severity so operators can tell whether the system is behaving normally or starting to degrade.

### The operational problem

The main issue is that the payment service occasionally experiences slow responses, high resource usage, and error-level events. These symptoms can lead to failed or delayed payments, which affects the customer experience and increases operational risk. The team needs a way to spot these problems early and understand what is going wrong.

### Why AIOps matters here

AIOps helps connect live operational data with automated detection and event handling. In this assessment, telemetry is analyzed for anomalies, the relevant events are published to a topic, and the resulting signals are consumed to mimic how an operations pipeline would surface issues. The goal is to detect incidents faster, reduce manual investigation, and give the team more visibility into service health.