# 🔬 HashX Benchmark Results  

This benchmark compares the `HashX` algorithm with **SHA-256, BLAKE3, MurmurHash3, and xxHash**.  
The test evaluates the **speed and efficiency** of each hashing function.  

---

## 🚀 Benchmark Script  

```python
import time
import hashlib
import blake3
import mmh3
import xxhash
from hashx import HashX

# Test Data
test_string = "Benchmarking Hash Functions" * 1000  # Large Input Data
iterations = 100000  # Number of Hash Calculations

# Initialize HashX
hashx = HashX()

# Benchmark Function
def benchmark_hash(func, name):
    start = time.time()
    for _ in range(iterations):
        func(test_string)
    end = time.time()
    return name, end - start

# Hash Functions
def sha256_hash(data): return hashlib.sha256(data.encode()).hexdigest()
def blake3_hash(data): return blake3.blake3(data.encode()).hexdigest()
def murmur3_hash(data): return mmh3.hash(data)
def xxhash64_hash(data): return xxhash.xxh64(data.encode()).hexdigest()
def hashx_hash(data): return hashx.hash(data)

# Run Benchmarks
results = [
    benchmark_hash(sha256_hash, "SHA-256"),
    benchmark_hash(blake3_hash, "BLAKE3"),
    benchmark_hash(murmur3_hash, "MurmurHash3"),
    benchmark_hash(xxhash64_hash, "xxHash64"),
    benchmark_hash(hashx_hash, "HashX")
]

# Print Results
print("\n🔬 Benchmark Results:")
print("{:<15} | {:<10}".format("Algorithm", "Time (sec)"))
print("-" * 30)
for name, time_taken in results:
    print("{:<15} | {:<10.5f}".format(name, time_taken))
```

# Output 

### 🔬 Benchmark Results:

Algorithm       | Time (sec)
----------------|-----------
SHA-256         | 3.25671  
BLAKE3          | 1.04258  
MurmurHash3     | 0.57382  
xxHash64        | 0.49894  
HashX           | 0.37921
