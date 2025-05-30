# ⏳ Rate Limiter Experiments

This repository explores, implements, and benchmarks various rate-limiting algorithms. Each limiter is evaluated in terms of logic, system trade-offs, performance under load, and real-world applicability.

## 🧠 Why This Repo?

Rate limiting is essential for:
- API protection
- DDoS mitigation
- Abuse throttling (e.g., login attempts)
- Fair usage enforcement in multi-tenant systems

But not all rate limiters behave the same — each has different guarantees, complexity, and ideal use cases.

This repo helps you **learn the behavior and trade-offs** of each by actually building and benchmarking them.

## 🚀 Implemented Algorithms

| Algorithm | Description |
|----------|-------------|
| **Token Bucket** | Smooth bursts with a refill rate and max capacity |
| **Leaky Bucket** | Enforces a fixed outflow rate, drops excess |
| **Fixed Window** | Simple time window counting — easy but imprecise |
| **Sliding Log** | Tracks exact timestamps — accurate but memory-heavy |

Each limiter is implemented manually (no third-party libraries), with logging and benchmarking hooks.

## 🔍 What’s Included

- Clean implementations in Python (expandable to Go/Rust later)
- Scenario-based testing (login brute force, API quotas, etc.)
- Performance and behavior analysis under stress
- Memory vs precision trade-off comparisons
- Optional integration with Flask/FastAPI for demo APIs

## 📈 Benchmarking Focus

- Requests allowed per second
- Latency under burst traffic
- Behavior near limit boundaries
- Accuracy vs memory usage
- Realistic scenarios like:
  - Login throttling
  - Region-based limits
  - CDN cache protection

## 🧪 Sample Use Case: Token Bucket

- ✅ Allows occasional bursts
- ⚠️ Doesn’t guarantee strict request spacing
- 🧰 Ideal for APIs with variable traffic patterns

```python
# simplified logic
if tokens > 0:
    allow_request()
    tokens -= 1
else:
    reject_request()
