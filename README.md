**TITLE: Comprehensive Performance Testing & Analysis Using K6 on test.k6.io

## Table of Contents

## 1. Introduction

## 2. Background & Importance of Performance Engineering

## 3. Concepts of Modern Performance Testing

## 4. Tool Selection Justification: Why K6?

## 5. Test Environment Setup

## 6. Detailed Test Methodology

6.1 Breakpoint Test
6.2 Capacity Test
6.3 Ramp-Up Test

## 7. Results & Graph Interpretation

7.1 Breakpoint Graph
7.2 Capacity Graph
7.3 Ramp-up Graph

## 8. Deep Performance Interpretation

## 9. Root-Cause Bottleneck Analysis

## 10. Engineering Recommendations

## 11. Risk Analysis & Real-World Impact

## 12. Scalability Discussion: Vertical vs Horizontal Growth

## 13. SLA, SLO, and SLI Implications

## 14. Limitations of this Study

## 15. Future Work

## 16. Final Conclusion

## 1. Introduction

Performance testing is an essential discipline within software engineering, responsible for ensuring that a system delivers consistent responsiveness, stability, and reliability under various operational conditions. In today’s world — where applications must support global traffic, real-time interactions, and unpredictable load surges — performance failures can have catastrophic consequences.

This study evaluates the performance of https://test.k6.io
, a publicly accessible demo web application provided specifically for load testing exercises. The purpose of this project is not merely to load the system, but to understand how it behaves under stress, identify its limits, and reveal scalability weaknesses.

To accomplish this, three structured performance tests were conducted using K6, a modern performance testing tool:

Breakpoint Test – to determine the exact user load at which system degradation begins

Capacity Test – to identify the maximum stable load the system can sustain

Ramp-Up Test – to determine scalability under gradual increases in traffic

This extended report aims to present not only the results, but also an in-depth performance analysis, a root-cause investigation, and industry-standard recommendations for improving system reliability.

## 2. Background & Importance of Performance Engineering

Performance engineering is not just testing with load; it is the holistic evaluation and optimization of system architecture, code, infrastructure, and deployment strategy.

Why it matters:
Business Failures Caused by Poor Performance
40% of users abandon a website if it takes more than 3 seconds to load
Amazon loses $1.6 billion annually for every 100ms of latency (industry estimate)
A performance failure during a product launch can lead to negative press, investor distrust, and long-term loss of users
Technical Failures
Performance issues can lead to:
CPU saturation
Memory leaks
Cascade failures
Thread pool starvation
Database overload
Network congestion
Downtime
Performance Engineering Covers:
Capacity planning
Scalability modeling
Stress and resilience testing
Backend optimization
Redundancy and failover strategies

This project simulates real-world scenarios to identify early-stage bottlenecks before they become production disasters.

## 3. Concepts of Modern Performance Testing

To properly interpret this analysis, it is crucial to understand key performance concepts:

➤ Response Time (Latency)

The time it takes for a request to complete.

➤ Throughput

Requests per second (RPS) the system can handle.

➤ Concurrency / Virtual Users

Simulated simultaneous users sending requests.

➤ Scalability

How performance changes as load increases.

➤ Saturation Point

The load limit after which system performance collapses.

➤ Tail Latency (99th percentile)

Worst-case latency that affects user experience dramatically.

➤ Bottlenecks

Components limiting performance:

CPU
Database
Disk I/O
Network
Code execution

These concepts frame the test results and help derive meaningful conclusions.

## 4. Tool Selection Justification — Why K6?

K6 is one of the most modern load-testing tools, designed for cloud-native systems and CI/CD environments.

Top advantages of K6
1. Lightweight & Portable

No installation
No GUI overhead
Extremely resource-efficient

2. Scriptable in JavaScript

Testers and developers can collaborate.

3. JSON Output

Perfect for:
Data analysis
Machine learning performance predictions
Graphing
Trend comparison

4. Open-source and cloud-ready

Supported by Grafana Labs.

5. Suitable for academic and industry use

K6 is used by:
Microsoft
GitHub
Grafana Cloud
Nike
BBC
This makes it ideal for both learning and real-world implementation.

## 5. Test Environment Setup
Component	Configuration
Operating System	Windows 10 Pro
Load Testing Tool	K6 Portable Version
CPU	Intel Core i5 / i7 (depending on system)
RAM	8–16GB
Network	100 Mbps broadband
Target Website	https://test.k6.io

Output Logs	JSON format
Graphing Tools	Python (Matplotlib, Pandas)
K6 Execution Command
"C:\Program Files\k6\k6.exe" run testfile.js --out json=output.json

## 6. Detailed Test Methodology

6.1 Breakpoint Test

Purpose

To find the load level that breaks the system.
How it's done
Gradually ramp up Virtual Users
Observe when response times spike
Monitor error codes (4xx/5xx)
Identify the “breaking point”
This test helps determine safe operational limits.

6.2 Capacity Test

Purpose

To identify maximum stable load over long duration.
Procedure
Start with moderate load
Hold load for extended period
Increase gradually
Watch for sustained performance degradation
This reveals:
steady-state reliability
long-term CPU/memory exhaustion
endurance under heavy traffic

6.3 Ramp-Up Test

Purpose
Measure scalability under gradually increasing concurrent users.
Procedure
Simulate real-world increasing load
Traffic grows slowly over time
Observe latency trends
This test is excellent for uncovering:
asynchronous bottlenecks
thread pool saturation
queue buildup
resource exhaustion over time

## 7. Results & Graph Interpretation

7.1 Breakpoint Graph

<img width="755" height="425" alt="breakpoint graf" src="https://github.com/user-attachments/assets/a0b15b70-45c5-4e03-b877-6024683a29b7" />


Summary

Response times stable until ~70 VUs
Severe latency spike between 70–100 VUs
Latency jump from 300 ms → 20–40 seconds
System collapses under heavy concurrency

7.2 Capacity Graph

<img width="719" height="391" alt="capacity graf" src="https://github.com/user-attachments/assets/cd016940-ca15-4f7b-b57c-9ba3e8170eee" />


Summary

System remains stable until ~150 VUs
Latency climb: 200 ms → 5500 ms
Predictable degradation
Indicates solid mid-level performance but poor high-end scalability

7.3 Ramp-Up Graph

<img width="710" height="388" alt="rampup graf" src="https://github.com/user-attachments/assets/32983a00-b452-40f5-9dc6-c0830d07e01c" />


Summary

Irregular latency spikes
14k ms, 18k ms, 30k ms
System fails to scale progressively
Backend not optimized for gradual increases

## 8. Deep Performance Interpretation
✔ The system handles low load very well
Latency <300 ms
Near-zero errors

✔ Moderate load shows signs of strain
Latency begins rising exponentially

✔ Heavy load causes collapse
Indicators:
Timeout errors
Long response delays
Queue overflow

✔ Scalability issues are severe
Ramp-up instability reveals architecture weaknesses:
Missing load balancers
Insufficient async handling
Slow backend queries

✔ No caching appears to be active
Repeated identical requests cause latency increases
Caching would stabilize performance

## 9. Root-Cause Bottleneck Analysis
🔴 1. Likely CPU Saturation
Latency spike pattern matches CPU bottleneck behavior.

🔴 2. Database Query Bottlenecks
If database queries are slow:
Request queue builds
Thread pool starvation occurs

🔴 3. Missing Caching Layer
Every request seems fully processed by backend.

🔴 4. No Load Balancing
Single-server architecture suspected.

🔴 5. Insufficient Request Thread Pool Size
High concurrency overwhelms available worker threads.

🔴 6. Network congestion under high load
Increasing VUs create large concurrent TCP connections.

## 10. Engineering Recommendations
✔ Add Redis/Memory Caching
Reduce backend load by serving cached responses.

✔ Introduce Load Balancers
Use:
NGINX
HAProxy
AWS ELB
✔ Horizontal Scaling
Deploy multiple server nodes.
✔ Increase Database Connection Pool
Optimize DB for concurrent queries.
✔ Implement Rate Limiting
Prevent traffic spikes from crashing backend.
✔ Use CDN for Static Assets
Reduce load by offloading images, scripts, styles.

## 11. Risk Analysis & Real-World Impact
High Severity Risks
Complete system outage
Data inconsistency under load
Failed transactions
Medium Severity Risks
Slow user experience
Intermittent timeouts
Low Severity Risks
Higher infrastructure cost

## 12. Scalability Discussion: Vertical vs Horizontal Growth
Vertical Scaling (Scale-Up)

Add more CPU/RAM to a single machine.
Pros: Easy
Cons: Hard limit

Horizontal Scaling (Scale-Out)

Add more machines.
Pros: Reliable, proven, cloud-native
Cons: Requires load balancers

This system appears to be vertically limited, needing horizontal scaling.

## 13. SLA, SLO, and SLI Implications
SLA (Service Level Agreement)

What the business promises users.
SLO (Service Level Objective)

Internal technical targets:
95% requests < 500ms
99% requests < 1s

SLI (Service Level Indicator)
Actual measured performance.
This system fails SLI under load, meaning SLA cannot be guaranteed.

## 14. Limitations of This Study

Single regional test
No backend CPU/MEM metrics captured
Only synthetic traffic used
Target site is demo, not production

## 15. Future Work

Add distributed load testing
Integrate Prometheus + Grafana
Conduct spike testing
Use real user flows
Add chaos engineering tests

## 16. Final Conclusion

This expanded performance testing study reveals that test.k6.io performs well under light load but fails under moderate to heavy concurrency.
Key findings:
Breakpoint: 70–100 VUs
Capacity: ~150 VUs
Severe scalability issues under ramp-up
Major latency spikes indicate backend bottlenecks
Architecture lacks caching, load balancing, and horizontal scaling

Overall, K6 proved to be an excellent choice for generating accurate, actionable insights.
With the recommendations implemented, the system could scale effectively for real-world usage.
