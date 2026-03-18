# [The Pragmatic SRE - Notes - CUJ, SLI/SLO](https://www.pragmaticsre.com/psre-guide)

>An SRE critical user journey is a sequence of steps a user takes to accomplish a specific goal within a system. By identifying these critical journeys, SREs can pinpoint the most important aspects of the system to monitor and measure. This understanding is crucial for establishing effective Service Level Indicators (SLIs) and Service Level Objectives (SLOs).

## 1. Why are SRE critical user journeys important?
1. Focus on what matters: By focusing on CUJ , SREs can prioritize their efforts and ensure that the most important aspects of the system are monitored and maintained.
2. Improved decision-making: Understanding critical user journeys helps SREs make informed decisions about resource allocation, capacity planning, and incident response.
3. Enhanced user experience: By monitoring and improving critical user journeys, SREs can directly impact the user experience.
4. Effective SLO definition: SLIs and SLOs can be defined more accurately and effectively when they are tied to specific user journeys.
5. Improved incident response: By knowing the impact of a failure on critical user journeys, SREs can prioritize incident response efforts.

## 2.  How to identify critical user journeys:

1.  User research: Conduct user research to understand how users interact with the system.
2. Business objectives: Identify the business goals that the system supports.
3.  System architecture: Analyze the system architecture to identify key components and dependencies.
4.  Customer support data: Review customer support tickets to identify common issues and pain points.

## 3. Example of a critical user journey and associated SLIs and SLOs: 

### Critical user journey: A user logs into the system, searches for a product, adds it to their cart, and checks out.

### SLIs: 
> Successful login rate
> Search query success rate
> Product page load time
> Checkout process completion rate 

### SLOs: 

> 99.9% successful login rate •
> 99.9% search query success rate •
> Average product page load time of 2 seconds •
> 99.9% checkout process completion rate

### By establishing clear SLIs and SLOs for critical user journeys, SREs can ensure that the system delivers a high-quality user experience and meets the needs of the business.

## Example: E-commerce Checkout Process

### A. Browse Products

-   **Description:** Users navigate through various product categories and view product details.
    
-   **Key Metrics:** Page load time, error rates, and search functionality performance.
    
-   **SLIs (Service Level Indicators):**
    
    1.  **Percentage of product pages loaded within 2 seconds.**
        
        -   **Metric:** `http_request_duration_seconds`
            
        -   **SLI:** Page load time
            
        -   **PromQL Query:**
            
            Code snippet
            
            ```
            histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket{job="ecommerce", handler="product_page"}[5m])) by (le))
            
            ```
            
        -   _Note: This query calculates the 99th percentile of the page load time for product pages._
            
    2.  **Number of successful search queries vs. total search queries.**
        

### B. Add to Cart

-   **Description:** Users add selected products to their shopping cart.
    
-   **Key Metrics:** Response time for adding items to the cart, error rates.
    
-   **SLIs:**
    
    1.  **Percentage of add-to-cart actions completed within 1 second.**
        
    2.  **Success rate of add-to-cart actions.**
        
        -   **Metric:** `http_requests_total`
            
        -   **PromQL Query:**
            
            Code snippet
            
            ```
            sum(rate(http_requests_total{job="ecommerce", handler="add_to_cart", status=~"2.."}[5m])) / sum(rate(http_requests_total{job="ecommerce", handler="add_to_cart"}[5m]))
            
            ```
            
        -   _Note: This query calculates the ratio of successful add-to-cart requests to total attempts._
            

### C. Checkout

-   **Description:** Users proceed to checkout, enter payment and shipping information, and place the order.
    
-   **Key Metrics:** Checkout page load time, payment processing time, error rates.
    
-   **SLIs:**
    
    1.  **Percentage of checkout pages loaded within 3 seconds.**
        
        -   **Metric:** `http_request_duration_seconds`
            
        -   **PromQL Query:**
            
            Code snippet
            
            ```
            histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket{job="ecommerce", handler="checkout"}[5m])) by (le))
            
            ```
            
    2.  **Percentage of payment transactions processed within 2 seconds.**
        
        -   **Metric:** `http_requests_total`
            
        -   **SLI:** Success rate of checkout transactions
            
        -   **PromQL Query:**
            
            Code snippet
            
            ```
            sum(rate(http_requests_total{job="ecommerce", handler="checkout", status=~"2.."}[5m])) / sum(rate(http_requests_total{job="ecommerce", handler="checkout"}[5m]))
            
            ```
            
    3.  **Number of successful checkout completions vs. total attempts.**
        

----------

I've converted that into a clean, structured Markdown format. I used a mix of nested lists and code blocks to make the technical definitions and PromQL queries much easier to scan.

----------

## Example. Implementing SLOs (Service Level Objectives)

### A. Define SLOs for Each Step

-   **Browse Products**
    
    -   **SLO:** 99.9% of product pages should load within 2 seconds.
        
    -   **PromQL Query:**
        
        Code snippet
        
        ```
        sum(rate(http_request_duration_seconds_bucket{job="ecommerce", handler="product_page", le="2"}[5m])) / 
        sum(rate(http_request_duration_seconds_count{job="ecommerce", handler="product_page"}[5m]))
        
        ```
        
-   **Add to Cart**
    
    -   **SLO:** 99.9% of add-to-cart actions should complete successfully.
        
    -   **PromQL Query:**
        
        Code snippet
        
        ```
        sum(rate(http_requests_total{job="ecommerce", handler="add_to_cart", status=~"2.."}[5m])) / 
        sum(rate(http_requests_total{job="ecommerce", handler="add_to_cart"}[5m]))
        
        ```
        
-   **Checkout**
    
    -   **SLO:** 99.9% of checkout pages should load within 3 seconds, and 99.9% of payment transactions should process within 2 seconds.
        
    -   **PromQL Query (Page Load):**
        
        Code snippet
        
        ```
        sum(rate(http_request_duration_seconds_bucket{job="ecommerce", handler="checkout", le="3"}[5m])) / 
        sum(rate(http_request_duration_seconds_count{job="ecommerce", handler="checkout"}[5m]))
        
        ```
        

----------

### Example SLO Configuration in Prometheus

Below is an example of how to define an SLO and a corresponding alert for the checkout success rate in your Prometheus rules:

YAML

```
groups:
  - name: slo-checkout
    rules:
      - record: slo:checkout:success_rate
        expr: |
          sum(rate(http_requests_total{job="ecommerce", handler="checkout", status=~"2.."}[5m])) / 
          sum(rate(http_requests_total{job="ecommerce", handler="checkout"}[5m]))

      - alert: CheckoutSuccessRateLow
        expr: slo:checkout:success_rate < 0.999
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Checkout success rate is below SLO"
          description: "The checkout success rate has fallen below the SLO of 99.9%."

```

> **Note:** This setup ensures that you are monitoring critical user journeys effectively and will be alerted immediately if the SLOs are breached.

----------