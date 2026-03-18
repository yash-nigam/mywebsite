# [The Pragmatic SRE - Notes - Key Principles](https://www.pragmaticsre.com/psre-guide)

# 1.  What is an SRE
- Effectively a software engineer working in operations supporting the resilience of applications, infrastructure', platforms and APIs
- You must be prepared to discuss your programming language of choice and some case studies on how you have used that in an SRE construct 

# Key SRE Principles
SRE emphasizes the following key principles:

## 1.  Automation and Automation:

1.  Automated Deployments:
- Automate the entire deployment process, from building and testing to deployment and rollback.
- This reduces human error and accelerates deployment time.

2. Configuration Management:
- Use configuration management tools like Ansible or Puppet to automate infrastructure provisioning and configuration.
3.  Self-Service Tools:
- Empower developers with self-service tools to deploy and manage their applications independently.

## 2. Continuous Delivery:

1.  Frequent Releases: Aim for frequent, small, and incremental releases to reduce the risk of large, disruptive changes.
2.  Automated Testing: Implement a robust automated testing suite to ensure code quality and prevent regressions.
3.  Blue-Green Deployments : Use blue-green deployments to minimize downtime and risk during releases.

## 3.  Incident Response: 

1.  Well-Defined Incident Response Plans: Have clear and concise incident response plans to guide teams through incidents. 
2.  Effective Communication: Ensure effective communication between teams during incidents.
3.  Post-Incident Review: Conduct thorough post-incident reviews to identify lessons learned and improve future responses. 
## 4.  Monitoring and Alerting:
1.  Proactive Monitoring: Implement comprehensive monitoring of systems and applications to detect issues before they impact users.
2.  Effective Alerting: Set up effective alerting mechanisms to notify the right people at the right time. 
3.  Automation of Response: Automate routine tasks like restarting services or scaling resources to minimize human intervention.

## 5.  Chaos Engineering:

1.  Proactive Failure Injection: Deliberately inject failures into systems to identify vulnerabilities and improve resilience. 
2.  Real-World Testing: Simulate real-world failures to test the system's ability to recover. 
3.  Continuous Improvement: Use the insights gained from chaos engineering to improve the system's reliability and resilience

## 6. Capacity planning 
1. is a critical aspect of SRE, ensuring that systems can handle expected and unexpected load
## 7.  Risk Embracing

1.  Calculated Risk-Taking:  SREs make informed decisions about when and how to introduce changes, balancing the potential benefits against the risks. 
2.  Fault Injection Testing: Simulating failures to identify vulnerabilities and improve resilience. 
4.  Post-Mortem Analysis: Learning from incidents to prevent future occurrences and improve system reliability.
## 8.  Eliminating Toil 
Toil refers to repetitive tasks that add little to no value. 
SREs strive to automate these tasks to free up time for more strategic work. 
This involves: 
1.  Automation: Creating scripts and tools to automate routine operations. 
2.  Self-Service Tools: Empowering engineers to solve problems independently, reducing the need for manual intervention. 
3.  Shift-Left: Involving SREs in the development process to prevent issues from arising in the first place.

## 9.  Release Engineering

1.  Release engineering focuses on the process of deploying software releases reliably and efficiently.
2.  SREs play a crucial role in this process by: 
	- Continuous Delivery: Automating the build, test, and deployment process.
	- Canary Releases: Gradually rolling out new features to a small subset of users to minimize risk.
	- Rollback Strategies: Having a plan in place to quickly revert to a previous version in case of issues.

## 10.  Postmortem Culture (Learning from Failure)

1. Conduct Regular Postmortems: After significant incidents, gather relevant teams to analyze what happened, identify root causes, and propose solutions. 
2. Promote a Blameless Culture: Encourage open and honest discussion without fear of punishment. Focus on learning from mistakes rather than assigning blame.
3.  Document Findings: Create detailed postmortem reports that include a timeline, root cause analysis, and action items. •
4.  Implement Corrective Actions: Prioritize and implement solutions to prevent future occurrences. •
5.  Share Lessons Learned: Disseminate knowledge across the organization to improve overall system reliability.

## 11. Tracking Outages
1. Establish a Centralized Outage Tracking System: Use a tool to record incidents, their impact, and resolution times.
2. Define Clear Incident Severity Levels: Categorize incidents based on their impact on users and services.
3. Track Mean Time to Repair (MTTR): Measure the time it takes to restore a system to its operational state.
4. Analyze Outage Trends: Identify patterns and recurring issues to proactively address them.

## 12.  Testing for Reliability
1. Chaos Engineering: Intentionally introduce failures into the system to test its resilience and identify vulnerabilities.
2.  Load Testing: Simulate heavy traffic to assess the system's performance under stress.
3. Failure Testing: Test how the system behaves in the event of component failures. 
4.  Recovery Testing: Verify the effectiveness of recovery procedures.

## 13.  Handling Overload 

1.  Implement Load Balancing: Distribute traffic across multiple servers to prevent overloading.
2. Utilize Caching: Reduce the load on backend systems by caching frequently accessed data.
3.  Graceful Degradation: Degrade service levels gracefully during periods of high load to avoid complete failures.
4.  Autoscaling: Automatically adjust the number of instances to match demand.

## 14.  Addressing Cascading Failures 

1.  Identify Dependencies: Map out dependencies between different system components.
2. Implement Circuit Breakers: Isolate failing components to prevent them from affecting other parts of the system.
3.  Rate Limiting: Limit the rate of incoming requests to prevent overload.



4.  Implement Error Budgets: Set service-level objectives (SLOs) and service-level indicators (SLIs) to measure reliability.
Hi! I'm your first Markdown file in **StackEdit**. If you want to learn about StackEdit, you can read me. If you want to play with Markdown, you can edit me. Once you have finished with me, you can create new files by opening the **file explorer** on the left corner of the navigation bar.