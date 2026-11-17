# Price Qian · Software Engineering Portfolio

I build distributed data systems with a focus on reliability, performance, and faster delivery of customer fixes. My work at AWS spans data plane mechanisms, control plane support, deployment pipelines, and Spark engine profiling.

## Selected impact

| Achievement | Result |
| --- | --- |
| Dynamic ACL updates at AWS | Reduced time-to-fix from **2 months to 2 weeks** for a global deployment |
| Spark engine performance at AWS | Improved **TPC-DS benchmark performance by 15%** |

## 1. Dynamic ACL updates at AWS

### The challenge

Our team received **10+ requests every month** to update a hardcoded ACL list. Customer workflows would fail without the required updates, but shipping a fix through the patch release process took **2 months**. This tied a recurring configuration change to a lengthy software release cycle.

### What I built

I built a mechanism to update the list dynamically across the data plane and control plane:

- **Data plane:** Enabled the underlying JVM process to read an external file in place of the hardcoded list.
- **Control plane:** Built support to vend that file to the data plane.
- **Delivery pipeline:** Built a pipeline to continuously ship the latest version of the file.

```mermaid
flowchart LR
    A[Latest ACL file] --> B[Continuous delivery pipeline]
    B --> C[Control plane file distribution]
    C --> D[Data plane JVM reads external file]
    D --> E[Updated ACL used by customer workflows]
```

### The result

Reduced time-to-fix from **2 months to 2 weeks for a global deployment**, decoupling ACL updates from the patch release cycle and accelerating fixes for failing customer workflows.

**Engineering strengths:** Data plane and control plane integration · JVM configuration · Continuous delivery · Operational reliability

## 2. Improving AWS Spark engine performance

### The challenge

Performance analysis of AWS' Spark engine revealed an opportunity to reduce unnecessary requests to an external catalog service.

### What I built

I built a profiler for the Spark engine and used it to identify a cache miss scenario that caused **2× the network requests** to the external catalog service.

The root cause was inconsistent cache keys between reads and writes. I fixed it by normalizing the cache key so that all cache reads and writes used the same standard.

### The result

Delivered a **15% performance improvement on the TPC-DS benchmark** by fixing the cache key inconsistency behind the redundant catalog requests.

**Engineering strengths:** Performance profiling · Root cause analysis · Cache correctness · Apache Spark · Benchmark-driven optimization

## How I approach engineering

- **Start with customer impact.** Prioritize changes that restore workflows and shorten the time customers wait for fixes.
- **Measure before optimizing.** Use profiling to identify the mechanism behind a performance problem.
- **Fix the underlying cause.** Separate frequently changing configuration from software releases and standardize cache keys at reads and writes.
- **Own the complete path.** Connect runtime behavior, control plane support, and delivery pipelines to achieve a production outcome.

---

This portfolio presents engineering case studies. It does not include AWS source code or internal implementation artifacts.
