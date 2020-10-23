---
title: 'COMPSCI 753 Notes'
date: 2020-06-30 09:00:00
intro: "University of Auckland COMPSCI 753 - Algorithms for Massive Data"
featured_image:
tags: Notes
---

> Course outline sorted out by myself for quick revision
> <i>University of Auckland COMPSCI 753 - Algorithms for Massive Data</i>

<br/>

## Data Stream
<hr/>

**Find similar items**
- Jaccard Similarity
- Shingling -> MinHash -> LSH
- MinHash
    - Random permutations
    - One-pass MinHash
<br/>

**Sampling data stream**
- Fixed proportion
- Fixed size
    - Reservoir Sampling
<br/>

**Find frequent items**
- [Deterministic] Misra-Gries
    - `(m-m')/(k+1)` decrement steps at most
- [Randomized] CountMin Sketch
<br/>

**Filtering data stream**
- Bloom Filter
    - 1 hash function
    - k hash functions
<br/>

**Locality Sensitive Search (LSH)**
- `(r, c, p1, p2)`-sensitive
- Jaccard similarity/distance
    - MinHash
- Cosine similarity/distance
    - SimHash

<br/>

# Graph
<hr/>

**Link Analysis**
- TF.IDF
- Term Spam
- PageRank
    - Dead ends
        - Recursively remove
        - Taxation
- Biased PageRank
- Link Spam (Spam Farm)
    - Trust Rank
    - Spam Mass
<br/>

**Social Network Analysis**
- Small world property
    - Power law degree distribution
- Core-Periphery structure
- Strength of ties
    - Triadic closure
- Clustering Coefficient
    - Triangle enumeration
- Community Detection
    - K-core decomposition
- Influence Maximization
    - Greedy-based
    - Sketch-based
<br/>
	

**Join Analysis**
- Natural join
- Semijoin
- Multiway join
- Acyclic join
    - Yannakakis Algorithm

