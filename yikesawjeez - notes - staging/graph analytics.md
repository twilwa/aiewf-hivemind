# graphs workshop

Tue, 03 Jun 25

### Graph Workshop Overview

- Neo4j graph workshop focused on using graph community detection and analysis for improving AI/LLM document retrieval
    
- Demonstrated use of Graph Data Science (GDS) library and k-nearest neighbors algorithm
    
- Key focus: Analyzing document similarities and improving retrieval efficiency
    

### Document Analysis Techniques

- Document Projection Process:
    
    - Create projection named “docs” containing only necessary nodes and properties
        
    - Include embedding property for similarity analysis
        
    - System provides node count and execution confirmation
        
- Community Detection:
    
    - Uses k-nearest neighbors to identify document clusters
        
    - Visualizes communities through color coding
        
    - Identifies bridge documents using betweenness centrality
        
    - Median word length found to be 512 characters, matching chunk size
        
    - Found 49 chunks with 0.98 similarity in Community 4702
        

### Improving Retrieval Quality

- Document Deduplication:
    
    - Uses APOC nodes collapse to reduce redundant content
        
    - Maintains document lineage while improving efficiency
        
    - Preserves relationships between collapsed nodes
        
- Diversity Enhancement:
    
    - Implements re-ranking for diverse responses
        
    - Uses PageRank to identify important documents
        
    - Creates co-occurrence relationships between related documents
        
    - Tracks document usage patterns across conversations
        

### Data Quality Considerations

- Signal Amplification:
    
    - Need to monitor and control signal amplification across agent chains
        
    - Important to verify and validate AI outputs
        
    - Focus on intelligent outcome management
        
- Content Analysis:
    
    - Look for clusters with poor ratings to identify problematic content
        
    - Analyze conversation lengths and community patterns
        
    - Consider both embedding similarity and structural relationships
        
    - Track document co-occurrence to understand concept relationships
        

---

Chat with meeting transcript: [https://notes.granola.ai/d/e85632d2-6528-44b5-be21-5c79b80663da](https://notes.granola.ai/d/e85632d2-6528-44b5-be21-5c79b80663da)