----------
## Service Level Management Concepts

### 1. SLI (Service Level Indicator)

-   A metric that measures the performance of a specific service.
-   It quantifies the observable behavior of a service.
    

### 2. SLO (Service Level Objective)

-   A target value or range of values for an SLI.
-   It defines the desired level of performance for a service.
    

### 3. Error Budget

-   The allowable amount of service degradation or failure.
- It represents the calculated risk tolerance for a specific service.
    

#### Example: Availability SLI

-   **System Uptime:** Measured as the percentage of time the system is available.
    
-   **SLO:** 99.9% availability.
    
-   **Target:** The system should be operational 99.9% of the time.
    
-   **Error Budget:** 0.1% (The remaining percentage allowed for failure).
    
-   **Tolerance:** The system can be down for a maximum of 0.1% of the total time.
    

#### Calculating the Error Budget

If a system is expected to run 24/7 for a year (8,760 hours):

-   $0.1\% \times 8760 \text{ hours} = 8.76 \text{ hours}$
-   The system can be down for a maximum of **8.76 hours per year** to meet a 99.9% availability SLO.
----------

### Availability vs. Allowed Downtime

|**Availability Level** | **Percentage** | **Allowed Downtime per Month** |
----------------------|---------------------|------------------------------------------
| **90%** | 90% | ~43.2 hours | 
| **99%** | 99%     | 7.3 hours | 
|**99.9%**|99.9%|~43.2 minutes
|**99.99%**|99.99%|~4.38 minutes

----------