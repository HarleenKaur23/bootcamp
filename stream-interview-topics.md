# Stream Interview Topics and Subtopics

A single merged checklist in three parts:

- **Part A** – Java Stream API (sections 1–12)
- **Part B** – Data-stream algorithm problems (sections 13–19)
- **Part C** – Stream processing systems (sections 20–25)

---

# Part A – Java Stream API

## 1. Fundamentals

- What a stream is, and how it differs from a collection
- Pipeline structure: source → intermediate operations → terminal operation
- Lazy evaluation (nothing runs until a terminal operation is called)
- Element-by-element processing through the pipeline, not stage by stage
- Internal vs. external iteration
- Streams are single-use; reuse throws `IllegalStateException`
- Encounter order (ordered sources such as `List` vs. unordered such as `HashSet`)
- Non-interference (do not modify the source during a pipeline)
- Stateless lambdas and avoiding side effects
- The "effectively final" rule for variables used in lambdas
- Infinite streams and why they need `limit` or a short-circuiting operation
- Closing streams: `BaseStream`, `AutoCloseable`, `onClose()`, try-with-resources

## 2. Creating Streams

- From collections: `stream()`, `parallelStream()`
- From arrays: `Arrays.stream()`, `Stream.of()`
- The `Stream.of(int[])` pitfall (gives `Stream<int[]>`, not `IntStream`)
- Generated: `Stream.iterate()` (with and without predicate), `Stream.generate()`, `Stream.builder()`
- Ranges: `IntStream.range()`, `IntStream.rangeClosed()`
- From strings: `String.chars()`, `Pattern.splitAsStream()`
- From files and readers: `Files.lines()`, `BufferedReader.lines()`
- From maps: `map.entrySet().stream()`, `keySet().stream()`, `values().stream()`
- Random numbers: `Random.ints()`, `doubles()`
- Empty and nullable: `Stream.empty()`, `Stream.ofNullable()`
- Combining: `Stream.concat()`

## 3. Intermediate Operations

- Filtering: `filter`, `distinct`
- Slicing: `limit`, `skip`, `takeWhile`, `dropWhile`
- Mapping: `map`, `flatMap`, `mapMulti`
- Mapping to primitives: `mapToInt`, `mapToLong`, `mapToDouble`
- Sorting: `sorted()`, `sorted(Comparator)`
- Debugging: `peek`
- Stateless operations (`filter`, `map`) vs. stateful operations (`sorted`, `distinct`, `limit`)
- Custom intermediate operations: `gather()` with Gatherers

## 4. Terminal Operations

- Iteration: `forEach`, `forEachOrdered`
- Reduction: `reduce` (three forms: accumulator only; identity + accumulator; identity + accumulator + combiner)
- Aggregation: `count`, `min`, `max`
- Collection: `collect`, `toList()`, `toArray`
- Matching: `anyMatch`, `allMatch`, `noneMatch`
- Finding: `findFirst`, `findAny`
- Short-circuiting terminal operations
- Escape hatches: `iterator()`, `spliterator()`

## 5. Collectors

- To collections: `toList`, `toSet`, `toCollection`
- To maps: `toMap` (key mapper, value mapper, merge function, map supplier), duplicate-key handling
- Unmodifiable: `toUnmodifiableList`, `toUnmodifiableSet`, `toUnmodifiableMap`
- Grouping: `groupingBy` (single-level, multi-level, with downstream collector, with map factory such as `TreeMap` or `LinkedHashMap`)
- Partitioning: `partitioningBy` (with and without downstream collector)
- Strings: `joining` (delimiter, prefix, suffix)
- Numeric: `counting`, `summingInt`, `averagingInt`, `summarizingInt` (and Long/Double variants)
- Min and max: `minBy`, `maxBy`
- Downstream adapters: `mapping`, `filtering`, `flatMapping`, `collectingAndThen`
- General reduction: `reducing`
- Two collectors at once: `teeing`
- Concurrent: `groupingByConcurrent`, `toConcurrentMap`
- Custom collectors: `Collector.of`
- Collector internals: supplier, accumulator, combiner, finisher
- Collector characteristics: `CONCURRENT`, `UNORDERED`, `IDENTITY_FINISH`

## 6. Primitive Streams

- `IntStream`, `LongStream`, `DoubleStream`
- Converting: `boxed()`, `mapToObj()`, `asLongStream()`, `asDoubleStream()`
- Built-in aggregates: `sum`, `average`, `min`, `max`, `summaryStatistics`
- `OptionalInt`, `OptionalLong`, `OptionalDouble`
- Boxing and unboxing cost; when to prefer primitive streams

## 7. Functional Foundations

- Lambda expressions: syntax, type inference, variable capture
- Method references: static, bound instance, unbound instance, constructor
- Functional interfaces and `@FunctionalInterface`
- Core interfaces: `Predicate`, `Function`, `Consumer`, `Supplier`
- Two-argument and operator interfaces: `BiFunction`, `BiPredicate`, `BiConsumer`, `UnaryOperator`, `BinaryOperator`
- Composition: `Predicate.and/or/negate`, `Function.andThen/compose`, `Function.identity()`
- `Optional`: `of`, `ofNullable`, `empty`, `map`, `flatMap`, `filter`, `orElse`, `orElseGet`, `orElseThrow`, `ifPresent`, `ifPresentOrElse`, `stream()`
- `orElse` vs. `orElseGet` (eager vs. lazy evaluation)
- `Comparator`: `comparing`, `comparingInt`, `thenComparing`, `reversed`, `naturalOrder`, `reverseOrder`, `nullsFirst`, `nullsLast`
- Map entry comparators: `Map.Entry.comparingByKey()`, `comparingByValue()`

## 8. Parallel Streams

- `parallel()` vs. `sequential()`; `isParallel()`
- Fork/Join framework and the common pool
- Running a parallel stream in a custom `ForkJoinPool`
- Spliterator: `tryAdvance`, `trySplit`
- Spliterator characteristics: `ORDERED`, `SIZED`, `SUBSIZED`, `DISTINCT`, `SORTED`, `IMMUTABLE`, `CONCURRENT`, `NONNULL`
- How the source affects splitting (`ArrayList` and arrays split well; `LinkedList` and `Stream.iterate` poorly)
- Thread safety, shared mutable state, and race conditions
- Ordering: `unordered()`, `forEach` vs. `forEachOrdered`
- Associativity and identity requirements in `reduce`
- Why blocking I/O in the common pool is a problem
- When parallel streams help and when they hurt

## 9. Version-Specific Features

- Java 8: Stream API, lambdas, `Optional`, Collectors
- Java 9: `takeWhile`, `dropWhile`, `Stream.ofNullable`, `iterate` with predicate, `Optional.stream()`, `Collectors.filtering`, `Collectors.flatMapping`
- Java 10: `toUnmodifiableList/Set/Map`
- Java 12: `Collectors.teeing`
- Java 16: `Stream.toList()`, `mapMulti`
- Java 24: Stream Gatherers (`gather()`, `windowFixed`, `windowSliding`, `fold`, `scan`, `mapConcurrent`)

## 10. Common Conceptual Questions

- Stream vs. collection
- Intermediate vs. terminal operations
- `map` vs. `flatMap`
- `findFirst` vs. `findAny`
- `reduce` vs. `collect`
- `forEach` vs. `forEachOrdered`
- `peek` vs. `map`
- `limit` vs. `skip`
- `Collection.forEach` vs. `Stream.forEach`
- `Stream.toList()` vs. `Collectors.toList()`
- `groupingBy` vs. `partitioningBy`
- `Stream.of()` vs. `Arrays.stream()`
- Sequential vs. parallel streams
- Stream vs. for-loop: performance and readability

## 11. Pitfalls and Best Practices

- Reusing a consumed stream
- Handling checked exceptions inside lambdas
- Handling nulls in streams and in `toMap` values
- Duplicate keys in `toMap` without a merge function
- Modifying the source collection during the pipeline
- Mutating external state from `forEach` instead of collecting
- Relying on `peek` for logic
- Ordering bugs in parallel streams
- Forgetting to close I/O-backed streams
- Debugging stream pipelines

## 12. Coding Problems

### 12.1 Numbers
- Filter even and odd numbers
- Sum, average, max, and min
- Second or nth highest and lowest
- Find duplicates; remove duplicates
- Squares or cubes of each element
- Prime numbers in a range
- Numbers starting with a given digit
- Sum of digits
- Find missing numbers in a range
- Pairs that sum to a target
- Cumulative (running) sum
- Fibonacci series with `Stream.iterate`

### 12.2 Strings
- Character frequency
- First non-repeated character
- First repeated character
- Reverse a string; reverse each word
- Palindrome check
- Check whether two strings are anagrams; group anagrams
- Longest and shortest string
- Word count in a sentence
- Remove duplicate characters
- Count vowels and consonants
- Sort strings by length
- Join with a delimiter; convert a list to a comma-separated string and back

### 12.3 Lists and Arrays
- Remove duplicates
- Common elements of two lists
- Merge and sort two arrays
- Flatten a list of lists
- Sort ascending and descending
- Top N elements
- Partition into even and odd
- Zip two lists using `IntStream.range`
- Cartesian product of two lists
- Split a list into chunks or batches
- Distinct by a property (the `distinctByKey` pattern)

### 12.4 Maps
- Sort a map by key or by value
- Convert a list to a map
- Invert a map
- Build a frequency map
- Most frequent element
- Merge two maps

### 12.5 Employee and Object Problems
- Group employees by department
- Count per department
- Highest-paid employee per department
- Average and total salary per department
- Nth highest salary
- Sort by multiple fields
- Partition by age, gender, or salary threshold
- Employee names joined by department
- Oldest and youngest employee
- Flatten nested objects (orders → line items → products)
- Group by date, month, or year

---

# Part B – Data-Stream Algorithm Problems

## 13. Running Statistics

- Median from a data stream (two heaps)
- Moving average from a data stream
- Running max and min
- Exponential moving average
- Running variance and standard deviation
- Product of the last K numbers

## 14. Top-K and Ranking

- Kth largest element in a stream
- Top K frequent elements
- Rank of a number in a stream (Fenwick tree or BST)
- Counting inversions online

## 15. Sliding Window

- Sliding window maximum (monotonic deque)
- Sliding window median
- Count distinct elements in every window
- First unique number in a stream
- Longest subarray or substring over a stream (two pointers)
- Hit counter
- Rate limiter (fixed window, sliding window, token bucket)

## 16. Sampling

- Reservoir sampling
- Random pick from a stream of unknown length
- Weighted reservoir sampling
- Distributed reservoir sampling

## 17. Frequency and Approximation

- Majority element (Boyer–Moore voting)
- Heavy hitters (Misra–Gries)
- Count-Min Sketch
- Bloom filter
- HyperLogLog (distinct count)

## 18. Strings, Intervals, and Ordering

- Stream of characters (trie or Aho–Corasick)
- First non-repeating character in a stream
- Data stream as disjoint intervals
- Merge K sorted streams
- Handling out-of-order events

## 19. Design Problems

- Logger rate limiter
- Online stock span
- Stock price fluctuation
- Time-based key-value store
- LRU and LFU cache

---

# Part C – Stream Processing Systems

## 20. Kafka Core

- Topics, partitions, offsets
- Producers: acknowledgements, batching, partitioning strategy, idempotent producer
- Consumers and consumer groups; rebalancing
- Offset management and commit strategies
- Replication, leaders, and in-sync replicas
- Delivery guarantees: at-most-once, at-least-once, exactly-once
- Ordering guarantees within and across partitions
- Retention and log compaction
- Schema management and schema evolution

## 21. Stream Processing Frameworks

- Kafka Streams, Flink, Spark Structured Streaming
- Stateless vs. stateful operations
- KStream vs. KTable; stream-table duality
- Joins: stream-stream, stream-table
- State stores and checkpointing
- Micro-batch vs. true streaming

## 22. Windowing and Time

- Tumbling, hopping (sliding), and session windows
- Event time vs. processing time
- Watermarks
- Late and out-of-order data

## 23. Reliability and Operations

- Backpressure
- Idempotency and deduplication
- Dead-letter queues and retries
- Replay and reprocessing
- Consumer lag and monitoring
- Scaling partitions and consumers

## 24. System Design Questions

- Real-time analytics pipeline
- Clickstream processing
- Fraud detection
- Top-K trending items
- Log aggregation
- Real-time notifications
- Change data capture

## 25. Reactive Streams

- Publisher, Subscriber, Subscription, Processor
- Backpressure strategies
- Project Reactor: `Mono`, `Flux`
- RxJava: `Observable`, `Flowable`
- Hot vs. cold publishers
- Reactive streams vs. Java 8 streams
