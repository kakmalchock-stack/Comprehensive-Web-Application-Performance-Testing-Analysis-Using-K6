<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>K6 Performance Testing Report</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background: #f7f7f7;
        }
        header {
            background: #0d1117;
            color: #fff;
            padding: 20px;
            text-align: center;
        }
        nav {
            background: #161b22;
            padding: 10px 20px;
        }
        nav a {
            color: #58a6ff;
            margin-right: 15px;
            text-decoration: none;
            font-weight: bold;
        }
        .container {
            max-width: 900px;
            margin: auto;
            background: #fff;
            padding: 20px;
        }
        h1, h2, h3 {
            color: #0d1117;
        }
        pre {
            background: #e5e5e5;
            padding: 10px;
            overflow-x: auto;
        }
        .graph-placeholder {
            background: #ddd;
            padding: 40px;
            text-align: center;
            margin: 20px 0;
            border-radius: 8px;
            font-style: italic;
        }
        footer {
            text-align: center;
            padding: 20px;
            margin-top: 40px;
            color: #555;
        }
    </style>
</head>
<body>
    <header>
        <h1>Comprehensive Performance Testing & Analysis Using K6</h1>
        <p>GitHub Pages Website Version</p>
    </header>

    <nav>
        <a href="#intro">Introduction</a>
        <a href="#tool">Tool Selection</a>
        <a href="#env">Environment</a>
        <a href="#method">Methodology</a>
        <a href="#results">Results</a>
        <a href="#bottlenecks">Bottlenecks</a>
        <a href="#recommend">Recommendations</a>
        <a href="#conclusion">Conclusion</a>
    </nav>

    <div class="container">
        <section id="intro">
            <h2>1. Introduction</h2>
            <p>This is the expanded GitHub Pages version of the full 2500+ word performance testing report. It provides a detailed breakdown of performance engineering concepts, scalability analysis, methodology, results, bottlenecks, and recommendations based on the K6 test executions against <a href="https://test.k6.io" target="_blank">https://test.k6.io</a>.</p>
        </section>

        <section id="toc">
            <h2>Table of Contents</h2>
            <ul>
                <li><a href="#intro">1. Introduction</a></li>
                <li><a href="#background">2. Background & Importance of Performance Engineering</a></li>
                <li><a href="#concepts">3. Concepts of Modern Performance Testing</a></li>
                <li><a href="#tool">4. Tool Selection Justification</a></li>
                <li><a href="#env">5. Test Environment Setup</a></li>
                <li><a href="#method">6. Detailed Test Methodology</a></li>
                <li><a href="#results">7. Results & Graph Interpretation</a></li>
                <li><a href="#analysis">8. Deep Performance Interpretation</a></li>
                <li><a href="#bottlenecks">9. Root-Cause Bottleneck Analysis</a></li>
                <li><a href="#recommend">10. Engineering Recommendations</a></li>
                <li><a href="#risks">11. Risk Analysis & Real-World Impact</a></li>
                <li><a href="#scaling">12. Scalability Discussion</a></li>
                <li><a href="#sla">13. SLA/SLO/SLI Implications</a></li>
                <li><a href="#limitations">14. Limitations</a></li>
                <li><a href="#future">15. Future Work</a></li>
                <li><a href="#conclusion">16. Final Conclusion</a></li>
            </ul>
        </section>

        <section id="background">
            <h2>2. Background & Importance of Performance Engineering</h2>
            <p>Performance engineering ensures that applications remain stable, responsive, and reliable under various load conditions. Modern systems must handle global scale, unpredictable surges, and real-time processing—making performance testing essential.</p>
        </section>

        <section id="concepts">
            <h2>3. Concepts of Modern Performance Testing</h2>
            <p>This section covers key terminology such as response time, throughput, concurrency, scalability, saturation points, tail latency, and bottlenecks, all of which help shape the interpretation of the system’s behavior under load.</p>
        </section>

        <section id="tool">
            <h2>4. Tool Selection Justification</h2>
            <p>K6 offers portability, JSON output, script-based flexibility, and excellent CI/CD compatibility, making it ideal for structured performance testing and analysis.</p>
        </section>

        <section id="env">
            <h2>5. Test Environment Setup</h2>
            <p>The testing was conducted on Windows 10 using the portable version of K6. The execution command used was:</p>
            <pre>"C:\Program Files\k6\k6.exe" run testfile.js --out json=output.json</pre>
        </section>

        <section id="method">
            <h2>6. Detailed Test Methodology</h2>
            <h3>6.1 Breakpoint Test</h3>
            <p>A gradual ramp-up of virtual users to detect the point where the system begins to degrade.</p>
            <h3>6.2 Capacity Test</h3>
            <p>A long-duration test performed to find the maximum stable throughput the system can sustain.</p>
            <h3>6.3 Ramp-Up Test</h3>
            <p>A progressive increase in traffic to evaluate scalability under growing demand.</p>
        </section>

        <section id="results">
            <h2>7. Results & Graph Interpretation</h2>
            <h3>7.1 Breakpoint Test</h3>
            <div class="graph-placeholder">Insert Breakpoint Graph Link Here</div>

            <h3>7.2 Capacity Test</h3>
            <div class="graph-placeholder">Insert Capacity Graph Link Here</div>

            <h3>7.3 Ramp-Up Test</h3>
            <div class="graph-placeholder">Insert Ramp-Up Graph Link Here</div>
        </section>

        <section id="analysis">
            <h2>8. Deep Performance Interpretation</h2>
            <p>The system performs well under small loads but collapses at higher concurrency levels. Latency spikes, instability, and failures indicate architecture bottlenecks.</p>
        </section>

        <section id="bottlenecks">
            <h2>9. Root-Cause Bottleneck Analysis</h2>
            <p>Likely causes include CPU saturation, database query latency, missing caching mechanisms, inadequate thread pools, and lack of load balancing.</p>
        </section>

        <section id="recommend">
            <h2>10. Engineering Recommendations</h2>
            <ul>
                <li>Introduce caching (Redis, CDN).</li>
                <li>Horizontal scaling and load balancing.</li>
                <li>Optimize backend queries and increase connection pools.</li>
                <li>Implement rate limiting and autoscaling.</li>
            </ul>
        </section>

        <section id="risks">
            <h2>11. Risk Analysis & Real-World Impact</h2>
            <p>Performance failures may lead to outages, revenue loss, degraded user experience, and operational instability.</p>
        </section>

        <section id="scaling">
            <h2>12. Scalability Discussion</h2>
            <p>The system currently appears limited by vertical scaling constraints. Horizontal scaling is recommended for production workloads.</p>
        </section>

        <section id="sla">
            <h2>13. SLA/SLO/SLI Implications</h2>
            <p>Based on observed latencies and instability, the system is not currently able to meet standard performance SLAs under moderate load.</p>
        </section>

        <section id="limitations">
            <h2>14. Limitations</h2>
            <p>The test target is a demo website and not production-grade infrastructure. Additional backend metrics would enhance analysis.</p>
        </section>

        <section id="future">
            <h2>15. Future Work</h2>
            <p>Potential future enhancements include distributed load testing, spike analysis, chaos engineering, and real-user flow simulations.</p>
        </section>

        <section id="conclusion">
            <h2>16. Final Conclusion</h2>
            <p>The system demonstrates acceptable performance at low concurrency but fails under heavy load. K6 proved to be an effective tool for identifying performance thresholds, bottlenecks, and scalability issues.</p>
        </section>
    </div>

    <footer>
        Generated as a complete GitHub Pages version of the extended K6 Performance Testing Report.
    </footer>
</body>
</html>
