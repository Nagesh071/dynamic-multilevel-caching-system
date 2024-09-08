Dynamic Multilevel Caching System:
----------------------------------
Overview:
--------
This project implements a Dynamic Multilevel Caching System that efficiently manages data across multiple cache levels. The system supports dynamic addition and removal of cache levels, customizable eviction policies (LRU and LFU), and data retrieval with automatic promotion between cache levels.

Key Features:
-------------
Multilevel Caching: Supports multiple cache levels (e.g., L1, L2, etc.), each with its own size and eviction policy.
Eviction Policies: Supports Least Recently Used (LRU) and Least Frequently Used (LFU) eviction policies.
Dynamic Cache Management: Allows dynamic addition and removal of cache levels at runtime.
Concurrency: Thread-safe operations to handle concurrent access to the cache.
Data Retrieval and Promotion: Retrieves data from the highest-priority cache level and promotes it to higher levels if found in lower levels.

Approach and Key Decisions:
---------------------------
1. Cache Level Design
CacheLevel Class: Each cache level is encapsulated in a CacheLevel class that handles storage, eviction policy, and size management.
Eviction Policies: The system supports both LRU and LFU policies, implemented via separate classes (LRU, LFU) inheriting from a common EvictionPolicy base class.
2. Data Retrieval and Insertion
Retrieval: When data is requested, the system checks from L1 downwards. If found in a lower level, the data is promoted to higher levels following the eviction policy.
Insertion: Data is always inserted at L1. If L1 is full, the least recently/frequently used data is evicted based on the selected policy.
3. Dynamic Cache Level Management
Addition and Removal: Cache levels can be added or removed at runtime, allowing for flexible and adaptive cache management.
4. Concurrency Considerations
Thread Safety: Used Python's threading.Lock to ensure that all operations on the cache are thread-safe, allowing for concurrent reads and writes.
dynamic-multilevel-caching-system/
├── src/
│   ├── cache.py   # Implementation of the cache system with CacheLevel, LRU, LFU classes.
│   └── main.py    # Main script to run sample test cases.
├── tests/
│   └── test_cache.py  # Placeholder for future unit tests.
└── README.md     # Documentation explaining the project.

Explanation of Files:
---------------------
src/cache.py: Contains the core implementation of the cache system, including the CacheLevel, LRU, LFU, and DynamicMultilevelCache classes.
src/main.py: Demonstrates how to use the caching system with various test cases, showcasing its functionality.
tests/test_cache.py: Placeholder for unit tests. Future work could include expanding test coverage here.


How to Run:
------------

Prerequisites
---------------
Python 3.x installed on your system.

Steps to Run
------------
Clone the Repository:
git clone https://github.com/yourusername/dynamic-multilevel-caching-system.git
cd dynamic-multilevel-caching-system
Run the Test Cases:
Navigate to the src directory:
cd src
Execute the main.py script:
python main.py

This will run the sample test cases, demonstrating how the caching system works across different cache levels and eviction policies.

Sample Output
After running the main.py script, you should see output similar to the following:
L1 Cache: [('A', '1'),  ('B', '2'), ('C', '3')]
L2 Cache: []
L1 Cache: [('A', '1'), ('D', '4'), ('C', '3')]
L2 Cache: [('B', '2')]
L1 Cache: [('D', '4'), ('C', '3'), ('A', '1')]
L2 Cache: [('B', '2')]
L1 Cache: [('E', '5'), ('D', '4'), ('A', '1')]
L2 Cache: [('C', '3')]
L1 Cache: [('E', '5'), ('F', '6'), ('D', '4')]
L2 Cache: []
L1 Cache: [('E', '5'), ('F', '6'), ('D', '4')]

Key Decisions and Assumptions:
------------------------------
Eviction Policy Implementation: Chose OrderedDict for LRU for its efficient handling of insertion order. For LFU, used a combination of a dictionary and a heap to track frequencies and evict the least frequently used items.
Concurrency: Ensured thread safety using threading.Lock to allow safe concurrent access, although concurrency was not deeply explored in the provided test cases.
Dynamic Management: Allowed cache levels to be added or removed, which may not always be common in fixed caching systems but adds flexibility to this design.
Future Enhancements
Unit Tests: Add comprehensive unit tests to validate edge cases, concurrency, and overall system stability.
Performance Optimization: Investigate performance bottlenecks, especially in the promotion mechanism, and optimize data structures if necessary.
Additional Eviction Policies: Consider implementing more eviction policies like FIFO (First In, First Out) for broader applicability.
Conclusion
This dynamic multilevel caching system provides a flexible and efficient way to manage cache across multiple levels with customizable eviction policies. The system is designed to be thread-safe and can be easily extended or modified for different use cases.
