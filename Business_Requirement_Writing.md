# Business Requirement Writing for Technical Team



## Requirement Purpose

### Understand the user needs

Understanding your users’ needs and being able to define the problem statement is the first step for writing better requirements. A good strategy to understand user needs clearly is to find answers to the ***“three W’s”:***

- **What** – What are we doing?
- **Why** – Why are we doing it?
- **Who** – Who is going to benefit from what we are doing?

Finding answers to the ***“three W’s”*** can help you immensely in developing a better understanding of the customer’s problems and needs and ultimately how you can reduce or resolve their pain points.

## Requirement Type

### Decleartive 

This kind of requirements is a tool that can ellicit the "Why" and "Who". It focus on the requirement background information, like where the requirement is from, and what kind of problem is this requriement is trying to solve. Decleartive means in this requirement, it only contains the why and who information, does not include the "Acceptance Criteria" or any technical details how this requirement should be implemented. 

### Imperative

Compared with declartive, the imperative requirement should be "testable". "Testable" means any technical team member can prepare the test cases to cover the possible path of business logic. Usually, it contains the "Acceptance Criteria" and even the architecture design and even test cases in TDD(Test Driven Development) process.



## Example

## Summary

Health check GET method support

## Background

customer needs check the meganode health status with load balancer through https Get function. Most load balancer does not support POST function, and all our meganode endpoints are only available through POST approach.

## User Story

As a system admin, I need configure my loadbalancer to check the health status of muitilple node service, so that the system can forward the RPC request to the available node service.

## Acceptance Criteria

1. The health status can be accessed through GET method. 
2. The health status API returns 200 if node service is in normal status.
3. The health status API returns 500 if node service is in abnormal status.

## Note:

Health status is not a standard RPC endpoints, should be included in the enhanced API.