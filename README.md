# Comprehensive-Web-Application-Performance-Testing-Analysis-Using-K6
Comprehensive Web Application Performance Testing &amp; Analysis Using K6

Performance testing is crucial for evaluating whether a web application can maintain responsiveness, reliability, and scalability under load. This report documents a complete performance testing cycle on the public web application **https://test.k6.io/**, utilizing the modern load testing tool **K6**.

# 📑 Table of Contents

1.  [Introduction & Objectives](#1-introduction--objectives)
    * [Test Types Executed](#test-types-executed)
2.  [Tool Selection Justification – Why K6?](#2-tool-selection-justification--why-k6)
3.  [Test Environment Setup](#3-test-environment-setup)
4.  [Test Scenarios & Methodology](#4-test-scenarios--methodology)
    * [4.1 Breakpoint Test](#41-breakpoint-test)
    * [4.2 Capacity Test](#42-capacity-test)
    * [4.3 Ramp-Up Test](#43-ramp-up-test)
5.  [Test Scripts (K6)](#5-test-scripts-k6)
    * [5.1 Breakpoint Test Script](#51-breakpoint-test-script)
    * [5.2 Capacity Test Script](#52-capacity-test-script)
    * [5.3 Ramp-Up Test Script](#53-ramp-up-test-script)
6.  [Test Results & Interpretation](#6-test-results--interpretation)
    * [6.1 Breakpoint Test Conclusion](#61-breakpoint-test-conclusion)
    * [6.2 Capacity Test Conclusion](#62-capacity-test-conclusion)
    * [6.3 Ramp-Up Test Conclusion](#63-ramp-up-test-conclusion)
7.  [Bottlenecks Identified](#7-bottlenecks-identified)
8.  [Recommendations for Improvement](#8-recommendations-for-improvement)
9.  [Video Presentation Walkthrough](#9-video-presentation-walkthrough)
10. [Final Conclusion](#10-final-conclusion)

## 1. Introduction & Objectives

Modern applications face unpredictable traffic, making performance testing essential to prevent system failures and poor user experience.

This testing cycle was designed to identify:
* System stability under increasing load
* Maximum capacity before performance degrades
* Scalability as the number of Virtual Users (VUs) increases
* Critical bottlenecks and failure points
* Recommendations for improving performance based on empirical evidence

### Test Types Executed
1.  **Breakpoint Test**
2.  **Capacity Test**
3.  **Ramp-Up Test**

All tests were scripted using K6, executed locally on Windows, and results were exported in JSON format for analysis and visualization.

## 2. Tool Selection Justification – Why K6?

K6 was selected as the primary load testing tool due to its suitability for professional and automated testing:

* **Lightweight & Portable:** K6 provides a standalone executable file (`k6.exe`), simplifying deployment and reducing system overhead.
* **Script-Based & Developer Friendly:** Test scenarios are written in **JavaScript**, which makes customizing complex load patterns and maintaining scripts straightforward.
* **Accurate Metrics:** K6 accurately tracks essential performance indicators such as Response time (`http_req_duration`), Error rate, Throughput, and VUs.
* **Export to JSON:** The ability to export metrics to `.json` format facilitates advanced data visualization and analysis (e.g., using Grafana).
* **Industry Adoption:** K6 is widely used by major companies (Grafana, Microsoft), validating its credibility and relevance for real-world testing.

## 3. Test Environment Setup

| Component | Configuration |
| :--- | :--- |
| **Operating System** | Windows 10 |
| **Testing Tool** | K6 Portable (Standalone .exe) |
| **Target Application** | `https://test.k6.io/` |
| **Network** | Home broadband (~100 Mbps) |
| **Output Format** | JSON exported logs |
| **Test Machine Specs** | Intel-based CPU, 8GB RAM |

**Execution Command:**

"C:\Program Files\k6\k6.exe" run testfile.js

**JSON Export Command:**

"C:\Program Files\k6\k6.exe" run testfile.js --out json=output.json

## 4. Test Scenarios & Methodology

The following test scenarios were designed to observe system behavior under various traffic patterns:

4.1 Breakpoint Test

Objective: Identify the point at which the system begins to fail due to excessive load.
Approach: Gradually increased load from 10 VUs to 200 VUs, monitoring response time and error rate.
Interpretation: Reveals the system’s maximum tolerable load before breakdown.

4.2 Capacity Test
Objective: Determine the maximum stable load the system can handle while maintaining acceptable performance.
Approach: Long-duration steady load with gradual increases at fixed intervals.
Interpretation: Shows sustained operating limit of the system.

4.3 Ramp-Up Test
Objective: Measure scalability when user count increases slowly and steadily.
Approach: Start with low VUs and increase smoothly over time.
Interpretation: Useful to understand how the system handles growing real-world traffic.

## 5. Test Scripts (K6)

5.1 Breakpoint Test Script

import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  stages: [
    { duration: '1m', target: 10 },
    { duration: '1m', target: 30 },
    { duration: '1m', target: 50 },
    { duration: '1m', target: 70 },
    { duration: '1m', target: 100 },
    { duration: '1m', target: 150 },
    { duration: '1m', target: 200 },
  ],
};

export default function () {
  http.get('[https://test.k6.io/](https://test.k6.io/)');
  sleep(1);
}

5.2 Capacity Test Script

import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  stages: [
    { duration: '10m', target: 50 },
    { duration: '10m', target: 100 },
    { duration: '10m', target: 150 },
    { duration: '10m', target: 200 },
  ],
};

export default function () {
  http.get('[https://test.k6.io/](https://test.k6.io/)');
  sleep(1);
}

5.3 Ramp-Up Test Script

import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  stages: [
    { duration: '15m', target: 300 },
    { duration: '5m', target: 300 },
    { duration: '5m', target: 0 },
  ],
};

export default function () {
  http.get('[https://test.k6.io/](https://test.k6.io/)');
  sleep(1);
}

## 6. Test Results & Interpretation
The results were exported to JSON and visualized as line charts showing Response Time (ms) over time.

6.1 Breakpoint Test Conclusion
Finding: The system responded quickly (100–300 ms) until the load reached 70–100 VUs.
Breakdown: Response time spiked drastically to 20,000–40,000 ms at this threshold, indicating a clear breakpoint and the upper safety limit of the system. [Image: <img width="755" height="425" alt="breakpoint graf" src="https://github.com/user-attachments/assets/d3708b0a-3d1e-4f6a-a4b9-4e29214d5273" />


6.2 Capacity Test Conclusion
Finding: As duration and load progressed, the response time showed a gradual increase, peaking at 4000–5500 ms.
Capacity: The system's maximum stable operating capacity is approximately 150 VUs, after which performance rapidly degrades, leading to significant user slowdowns. <img width="719" height="391" alt="capacity graf" src="https://github.com/user-attachments/assets/d45c7c31-6860-416c-af6b-5174f8bce8d2" />


6.3 Ramp-Up Test Conclusion
Finding: The system experienced several extreme latency spikes (up to 14,000 ms, 18,000 ms, and 30,000 ms) during the smooth ramp-up stage.
Scalability: This demonstrates poor scalability; the system cannot handle gradual, real-world traffic growth efficiently due to backend exhaustion. <img width="710" height="388" alt="rampup graf" src="https://github.com/user-attachments/assets/f36ba620-2cea-4447-9293-ffc639b066b4" />

## 7. Bottlenecks Identified
Based on the empirical evidence, the following bottlenecks were identified:

High Latency Under Load: Significant delays occur under moderate to high traffic.

Scalability Issues: The system does not scale linearly with an increasing number of users.

Backend Saturation: Possible resource exhaustion in areas like Server CPU, Database response time, Application thread pool, or Network I/O.

No Load Balancing: The rapid failure suggests a potential single-node architecture being overwhelmed.

## 8. Recommendations for Improvement
To enhance the web application's performance and reliability, the following actions are recommended:

Implement Caching: Reduce pressure on the backend by caching static and frequently accessed content.

Introduce Load Balancers: Distribute the load among multiple application instances to ensure scalability and redundancy.

Increase Server Resources: Add CPU/RAM capacity to delay performance degradation under high loads.

Optimize Backend Queries: Identify and tune slow database requests, as these often cause large latency spikes.

Apply Rate Limiting: Control sudden, unsustainable traffic bursts that could lead to system overload.

## 9. Video Presentation Walkthrough
A detailed walkthrough of the test execution, configuration steps, and key result interpretation is available in the video below.

[⚠️ INSERT YOUTUBE VIDEO LINK HERE ⚠️]

## 10. Final Conclusion
This exercise demonstrated K6's effectiveness in providing a structured evaluation of web application behavior under various load conditions. The limitations, stability, and bottlenecks of the target application were clearly identified:

Breakpoint: System failure observed at 70–100 VUs.

Capacity: Maximum stable load determined to be 150 VUs.

Ramp-Up: System exhibits poor scalability under gradual traffic growth.

The insights and recommendations provided serve as a crucial foundation for improving the web application's reliability before deployment in production environments.

