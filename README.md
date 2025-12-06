# Comprehensive-Web-Application-Performance-Testing-Analysis-Using-K6
Comprehensive Web Application Performance Testing &amp; Analysis Using K6

Performance testing is crucial for evaluating whether a web application can maintain responsiveness, reliability, and scalability under load. This report documents a complete performance testing cycle on the public web application **https://test.k6.io/**, utilizing the modern load testing tool **K6**.

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
Capacity: The system's maximum stable operating capacity is approximately 150 VUs, after which performance rapidly degrades, leading to significant user slowdowns. [Image: Placeholder for Capacity Test Graph]

6.3 Ramp-Up Test Conclusion
Finding: The system experienced several extreme latency spikes (up to 14,000 ms, 18,000 ms, and 30,000 ms) during the smooth ramp-up stage.
Scalability: This demonstrates poor scalability; the system cannot handle gradual, real-world traffic growth efficiently due to backend exhaustion. [Image: Placeholder for Ramp-Up Test Graph]
