----------

# SRE Failure Mode Analysis: A Guide

An **SRE Failure Mode** is a specific way in which a system or service can fail. As an SRE, your goal is to transition from "hoping it works" to "knowing how it breaks" so you can build resiliency.

### What defines a Failure?

-   **Downtime:** The service is unreachable.
    
-   **Degradation:** The service is slow or "flappy" (Partial failure).
    
-   **Data Loss:** Information is corrupted or permanently deleted.
    

----------

## The Lifecycle of Failure Management

The SRE must navigate four distinct stages to harden a system against potential disasters.

### 1. Identification

-   **Map Critical User Journeys (CUJ):** Trace a customer's path (e.g., _Click Cart → View Items → Checkout → Payment_).
    
-   **Locate Weak Points:** Ask where the services are hosted, how they are instrumented, and if the data is saved at each step.
    
-   **Brainstorm "What-Ifs":** Consider hardware failures, software bugs, network hiccups, and human error.
    

### 2. Analysis

-   **Simulate Scenarios:** What if the "Add to Cart" API fails? What if the payment service is slow?
    
-   **Test Edge Cases:** What happens if a user adds 1,000 items to their cart simultaneously?
    
-   **Impact Assessment:** Determine which failures cause a total blackout versus a minor inconvenience.
    
-   **Prioritization:** Rank failures based on severity and probability.
    

### 3. Mitigation

-   **Redundancy:** Ensure there is no single point of failure (SPOF).
    
-   **Failover Mechanisms:** Automate the switch to a backup system when the primary fails.
    
-   **Circuit Breakers:** Prevent a failing service from "poisoning" or overwhelming the rest of the app.
    

### 4. Detection

-   **Custom Metrics:** Don't just monitor if a server is "up"; monitor the _latent_ performance.
    
-   **Proactive Alerting:** Find out the payment service is slow before the customer tweets about it.
    
-   **Distributed Tracing:** Use tools like **Jaeger** or **Zipkin** to see exactly where a request is getting stuck in a microservice web.
    

----------

## Failure Mode Examples

### Case Study A: The Database

-   **Mode:** Connection failure.
    
-   **Impact:** Complete application downtime.
    
-   **Mitigation:** Implement DB replication and automated failover.
    
-   **Detection:** Alerts for "Connection Refused" errors and health check monitoring.
    

### Case Study B: Microservices Cascading Failure

-   **The Problem:** Service A fails, causing Service B to hang, eventually crashing the entire site.
    
-   **The Fix:**
    
    1.  **Map Dependencies:** Know exactly which service relies on which.
        
    2.  **Chaos Engineering:** Inject network errors to see if the system recovers gracefully.
        
    3.  **Circuit Breaker Pattern:** If Service A is failing, stop calling it immediately to save Service B.
        

----------

## Common Sources of Failure

**Category**

**Typical Causes**

**Hardware**

Disk drive failures, network card issues, power outages.

**Software**

Logic bugs, memory leaks, configuration errors, or security vulnerabilities.

**Network**

Latency spikes, DNS resolution failures, or partitioned regions.

**Human Error**

Accidental deletions, misconfigured production environments, or poor procedures.

**Third-Party**

Failures in external APIs (e.g., PayPal/Stripe) or breaking changes in 3rd party code.

**Security**

Cyberattacks (DDoS), data breaches, and unauthorized access attempts.

----------

> **SRE Pro-Tip:** Resilience is not about preventing every failure; it's about ensuring that when a failure happens, it is **detected quickly** and **contained easily**.

Would you like me to help you draft a **Post-Mortem (Incident Report) Template** to document these failures when they occur?