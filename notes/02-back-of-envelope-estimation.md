# Chapter 2 — Back-of-the-Envelope Estimation

> **Big idea:** In interviews you must estimate system capacity or performance using
> *thought experiments and common numbers*. To do this well you need to master three
> tools: **powers of two**, **latency numbers**, and **availability numbers**. The point
> isn't a precise answer — it's showing you can reason about **scale**.

---

## 1. Powers of Two

Data volume is expressed with powers of two. The base unit is a **byte** = 8 bits.
An **ASCII character = 1 byte**.

| Power | Approx value | Full name | Short |
|------:|-------------:|-----------|:-----:|
| 2^10 | ~1 Thousand | 1 Kilobyte | 1 KB |
| 2^20 | ~1 Million | 1 Megabyte | 1 MB |
| 2^30 | ~1 Billion | 1 Gigabyte | 1 GB |
| 2^40 | ~1 Trillion | 1 Terabyte | 1 TB |
| 2^50 | ~1 Quadrillion | 1 Petabyte | 1 PB |

> Rule of thumb: each step up is **~1000×** (technically 1024×).

---

## 2. Latency Numbers Every Programmer Should Know

Approximate numbers (from Dr. Jeff Dean, Google). Values are dated but the **relative
orders of magnitude** are what matter.

| Operation | Approx time |
|---|---|
| L1 cache reference | 0.5 ns |
| Branch mispredict | 5 ns |
| L2 cache reference | 7 ns |
| Mutex lock/unlock | 100 ns |
| Main memory reference | 100 ns |
| Compress 1 KB with Zippy | 10,000 ns = 10 µs |
| Send 2 KB over 1 Gbps network | 20,000 ns = 20 µs |
| Read 1 MB sequentially from memory | 250,000 ns = 250 µs |
| Round trip within same data center | 500,000 ns = 500 µs |
| Disk seek | 10,000,000 ns = 10 ms |
| Read 1 MB sequentially from network | 10,000,000 ns = 10 ms |
| Read 1 MB sequentially from disk | 30,000,000 ns = 30 ms |
| Send packet CA → Netherlands → CA | 150,000,000 ns = 150 ms |

**Units:** 1 ns = 10⁻⁹ s · 1 µs = 10⁻⁶ s = 1,000 ns · 1 ms = 10⁻³ s = 1,000 µs = 1,000,000 ns.

**Takeaways:**
- **Memory is fast, disk is slow.** Avoid disk seeks when possible.
- **Simple compression is fast.** Compress data *before* sending over the network if possible.
- Data centers are usually in different regions → **inter-region transfer takes time**.
- The internet is the bottleneck: network round trips across continents dominate (150 ms).

---

## 3. Availability Numbers

**High availability** = the system stays operational for a desirably long time, measured
as a **percentage of uptime** (100% = never down). Most services target **99% to 100%**.

An **SLA (Service Level Agreement)** formally defines the uptime a provider guarantees.
Uptime is measured in **"nines"** — more nines = less downtime.

| Availability % | Downtime / day | Downtime / year |
|---|---|---|
| 99% (two nines) | 14.40 min | 3.65 days |
| 99.9% (three nines) | 1.44 min | 8.77 hours |
| 99.99% (four nines) | 8.64 s | 52.60 min |
| 99.999% (five nines) | 864 ms | 5.26 min |
| 99.9999% (six nines) | 86.4 ms | 31.56 s |

---

## 4. Worked Example — Estimate Twitter QPS & Storage

**Assumptions:**
- 300 million monthly active users (MAU).
- 50% of users use Twitter **daily** → **150M daily active users (DAU)**.
- Users post **2 tweets/day** on average.
- **10%** of tweets contain media.
- Data retained for **5 years**.

### Query Per Second (QPS) estimation

```text
DAU = 150,000,000
Tweets/day = 150M users × 2 tweets = 300M tweets/day

Tweets QPS = 300,000,000 / 86,400 s  ≈  3,500 QPS   (seconds in a day ≈ 86,400)

Peak QPS = 2 × QPS  ≈  7,000 QPS      (rule of thumb: peak ≈ 2× average)
```

### Media storage estimation

```text
Average tweet size:
  tweet_id          64 bytes
  text             140 bytes
  media          1,000,000 bytes (1 MB)

Media per day = 300M tweets × 10% × 1 MB = 30,000,000 MB/day = 30 TB/day

5-year media storage = 30 TB × 365 × 5 ≈ 54,750 TB ≈ 55 PB
```

> Notice the **structure**: state assumptions → compute daily numbers → scale to QPS and
> to retention window. Interviewers care about this reasoning path.

---

## 5. Tips for Estimation

- **Rounding & approximation** — interviews aren't about precise math. Simplify:
  `99987 / 9.1` → estimate `100,000 / 10`. Speed and clarity beat precision.
- **Write down your assumptions** — so you (and the interviewer) can reference them.
- **Label your units** — is it 5 MB or 5 GB? Ambiguity causes mistakes.
- **Practice the common ones**: QPS, peak QPS, storage, cache size, number of servers.

---

## Cheat Sheet

**Memorize these:**
- Seconds in a day ≈ **86,400** (use **100,000** = 10⁵ to simplify).
- **Peak QPS ≈ 2 × average QPS**.
- Powers of two: KB(2¹⁰) → MB(2²⁰) → GB(2³⁰) → TB(2⁴⁰) → PB(2⁵⁰), each ~1000×.
- Memory ≈ 100 ns · Data-center round trip ≈ 500 µs · Disk seek ≈ 10 ms · Cross-continent ≈ 150 ms.
- 1 char (ASCII) = 1 byte.

**Estimation recipe:**
```text
1. State assumptions (users, actions/user/day, item size, retention).
2. DAU = MAU × daily-active fraction.
3. Actions/day = DAU × actions per user.
4. QPS = actions/day ÷ 86,400 ;  Peak QPS = 2 × QPS.
5. Storage/day = actions/day × fraction × item size.
6. Total storage = storage/day × 365 × retention_years.
```

---

## Practice Questions

1. A photo app has 500M MAU, 40% daily active, each user uploads 1 photo/day at 2 MB.
   Estimate **QPS**, **peak QPS**, and **1-year storage**.
2. Convert **99.99%** availability into approximate downtime per day and per year.
3. Roughly how much longer does a disk seek take than a main-memory reference (orders of
   magnitude)?
4. Why is `peak QPS ≈ 2 × average QPS` a *rough* heuristic? When would it be wrong?
5. You need to cache 20% of daily tweets (from the example above) in memory. Estimate the
   cache size needed for text-only tweets.
6. Why should you compress data before sending it across data centers? Back it with a
   latency number.
