

# High-Performance In-Memory Key-Value Store

A Redis-inspired, high-performance in-memory key-value store implemented in C++. The project focuses on efficient caching, concurrent access, cache eviction strategies, TTL-based expiration, and request rate limiting.

It provides multiple cache implementations, including LRU, LFU, and Sharded Cache, along with rate-limiting algorithms and a multithreaded benchmarking suite to evaluate performance under concurrent workloads.

## Features

- **LRU Cache:** Implements the Least Recently Used eviction policy.
- **LFU Cache:** Implements the Least Frequently Used eviction policy.
- **Sharded Cache:** Distributes cache entries across multiple shards to improve concurrent access.
- **TTL-Based Expiration:** Supports configurable time-to-live for cache entries.
- **Thread Safety:** Uses synchronization mechanisms to support concurrent cache operations.
- **Rate Limiting:** Includes Token Bucket and Sliding Window algorithms.
- **Performance Benchmarking:** Measures throughput and latency under multithreaded workloads.
- **Unit Testing:** Includes GoogleTest-based tests for cache operations, concurrency, expiration, sharding, and rate limiting.

## Technologies Used

- **Language:** C++
- **Build System:** CMake
- **Testing Framework:** GoogleTest
- **Core Concepts:** Data Structures, Multithreading, Synchronization, Memory Management
- **Algorithms:** LRU, LFU, Token Bucket, Sliding Window

## Project Architecture

The project consists of the following core components:

| Component | Description |
|---|---|
| LRU Cache | Evicts the least recently used entry when capacity is reached. |
| LFU Cache | Evicts the least frequently accessed entry. |
| Sharded Cache | Distributes keys across multiple shards for concurrent access. |
| TTL Management | Supports expiration of cache entries after a configured duration. |
| Token Bucket | Controls request rates using a token replenishment mechanism. |
| Sliding Window | Restricts requests within a moving time window. |
| Benchmark Suite | Evaluates throughput and latency under concurrent workloads. |

## Repository Structure

```text
.
├── include/
│   ├── LRUCache.h
│   ├── LFUCache.h
│   ├── ShardedCache.h
│   └── RateLimiter.h
│
├── src/
│   ├── LRUCache.cpp
│   ├── LFUCache.cpp
│   ├── ShardedCache.cpp
│   └── RateLimiter.cpp
│
├── tests/
│   ├── test_lru.cpp
│   ├── test_lfu.cpp
│   ├── test_sharded_cache.cpp
│   └── test_rate_limiter.cpp
│
├── benchmarks/
│   └── benchmark.cpp
│
├── CMakeLists.txt
└── README.md
```

*Note: This is a suggested logical structure. Adjust the paths and filenames to match the actual repository.*

## Getting Started

### Prerequisites

Make sure the following tools are installed:

- C++ compiler supporting C++17 or later
- CMake
- Git
- GoogleTest

### Clone the Repository

```bash
git clone <repository-url>
cd <repository-folder>
```

### Build the Project

Create a build directory:

```bash
mkdir build
cd build
```

Configure the project:

```bash
cmake ..
```

Compile the source code:

```bash
cmake --build .
```

## Running Tests

The project uses GoogleTest for unit testing.

Run the test suite using:

```bash
ctest --output-on-failure
```

The tests cover:

- Cache insertion and retrieval
- LRU eviction behavior
- LFU eviction behavior
- TTL-based expiration
- Concurrent cache operations
- Sharded cache functionality
- Token Bucket rate limiting
- Sliding Window rate limiting

## Cache Implementations

### 1. LRU Cache

The Least Recently Used cache removes the entry that has not been accessed for the longest period when the cache reaches its capacity.

**Key characteristics:**
- Maintains recently accessed entries.
- Evicts the least recently used entry.
- Provides efficient cache operations.

### 2. LFU Cache

The Least Frequently Used cache removes the entry with the lowest access frequency when the cache reaches its capacity.

**Key characteristics:**
- Tracks access frequency.
- Prioritizes frequently accessed entries.
- Uses frequency information to determine eviction.

### 3. Sharded Cache

The Sharded Cache divides the cache into multiple independent sections, or shards.

**Key characteristics:**
- Distributes keys across shards.
- Uses deterministic key routing.
- Supports concurrent operations.
- Reduces contention compared with a single shared cache lock.

## TTL-Based Expiration

The cache supports optional Time-To-Live (TTL) expiration for individual entries.

An entry becomes expired after its configured lifetime.

Expiration is handled through:

- Lazy expiration during cache access.
- Explicit cleanup using `purge_expired()`.

This helps prevent expired entries from remaining in the cache indefinitely.

## Rate Limiting

The project implements two rate-limiting algorithms.

### Token Bucket Algorithm

The Token Bucket algorithm controls request rates using a bucket of tokens.

- Tokens are replenished over time.
- Each request consumes a token.
- Requests are rejected when insufficient tokens are available.

### Sliding Window Algorithm

The Sliding Window algorithm tracks requests within a moving time interval.

- Maintains request timestamps.
- Removes requests outside the active time window.
- Restricts the number of requests allowed during the configured interval.

## Performance Benchmarking

The project includes a multithreaded benchmarking suite to evaluate cache performance under concurrent workloads.

The benchmark measures:

| Metric | Description |
|---|---|
| Throughput | Number of operations completed per second |
| p50 Latency | Median operation latency |
| p95 Latency | Latency below which 95% of operations complete |
| p99 Latency | Latency below which 99% of operations complete |

These metrics help evaluate the performance and scalability of the cache implementations.

## Design Considerations

The project explores important systems programming concepts:

- Efficient data structures and eviction policies
- Hash-based key lookup
- Thread synchronization
- Concurrent data access
- Sharded storage architecture
- TTL-based resource management
- Request throttling
- Performance measurement

## Future Improvements

Potential extensions include:

- Persistence and snapshot support
- Distributed caching
- Network-based client-server communication
- Additional eviction policies
- Cache statistics and monitoring
- Improved benchmark visualizations

## Author

**Srishti Mishra**
