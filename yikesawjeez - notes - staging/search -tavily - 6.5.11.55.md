---
title: "Dynamic Evaluation Framework for AI Search Systems"
source: "Technical Presentation"
author: "Ting Yu Mong (MongoDB), Diana (Quotient AI)"
created: 2024-12-19
tags: 
  - highlight
  - ai-search
  - evaluation-metrics
  - rag-systems
  - dynamic-benchmarking
  - reference-free-evaluation
  - llm-evaluation
description: "Discussion on moving from static to dynamic evaluation frameworks for AI search systems, introducing reference-free metrics and holistic evaluation approaches"
---

## Key Takeaways

### Dynamic vs Static Evaluation
- **Static datasets insufficient**: Traditional benchmarks like Simple QA and HotPot QA don't reflect real-world, rapidly evolving information needs
- **Dynamic datasets essential**: Must reflect the changing pace of the web for production RAG systems
- **Real-world alignment**: Dynamic evaluation provides broad coverage and continuous relevancy for any domain or use case

### Reference-Free Metrics Framework
Three core metrics for evaluating AI search without ground truth:

1. **Answer Completeness**: Classifies responses as fully addressed, unaddressed, or unknown
2. **Document Relevance**: Percentage of retrieved documents actually relevant to the question
3. **Hallucination Detection**: Identifies facts in responses not present in grounding documents

### Evaluation Insights
- **Trade-offs exist**: High performance on one metric may compromise others (completeness vs hallucination)
- **Correlation with ground truth**: Reference-free metrics showed 0.94 correlation with traditional accuracy scores
- **Diagnostic capability**: Combined metrics help identify root causes and appropriate remediation strategies

## Relevance

### For AI System Design
- Implement holistic evaluation frameworks measuring source diversity, relevancy, and hallucination rates
- Design systems with supervisor nodes for coordination in multi-agent architectures
- Build evaluation pipelines that can handle both simple factual and multi-hop reasoning questions

### For Production Deployment
- Use LangSmith or similar observability tools to track experiments and performance over time
- Implement continuous evaluation against latest data rather than static benchmarks
- Ensure transparency by requiring grounding document access for proper evaluation

### For Evaluation Strategy
- Move beyond simple accuracy metrics to comprehensive evaluation frameworks
- Leverage unsupervised evaluation methods to scale without labeled data
- Generate evidence-based question-answer pairs with full traceability to sources
- Address bias proactively and ensure fair coverage across different perspectives

### Future Vision
- Build AI systems that continuously improve themselves
- Develop agents that learn from patterns, detect outdated information, and identify unreliable sources
- Create systems capable of self-correction without human intervention
- Focus on augmented AI that goes beyond traditional benchmarking and monitoring


n this meeting, participants discussed the framework and metrics used for evaluating AI search providers, emphasizing the importance of reference-free metrics in cases where ground truths are not available.

Key Decisions Made:

- Emphasis on the transition from static to dynamic benchmarking for AI systems.
- Agreement on the need for continuous improvement and self-learning in AI agents.

Action Items:

- No specific action items with owners were mentioned in the transcript.

Follow-ups or Next Steps:

- Future discussions are expected to focus on refining the evaluation metrics and addressing identified issues within AI search systems.

Additional Key Points:

1. The conversation highlighted the limitations of static datasets in evaluating AI search systems.
2. Participants reviewed three key reference-free metrics: answer completeness, document relevance, and hallucination detection.
3. Trade-offs between completeness, competitiveness, and hallucination rates were discussed.
4. Emphasis was placed on the significance of grounding documents in ensuring response accuracy.

Conclusions and Takeaways:

- The meeting underscored the critical need for dynamic datasets that reflect real-time information for effective AI benchmarking.
- Known issues with existing metrics were acknowledged, including the difficulties in quantifying correctness without ground truth.

Disagreements or Alternative Viewpoints:

- There were no explicit disagreements noted in the discussion; however, different perspectives on the effectiveness of metrics were implied.

Unresolved Issues or Open Questions:

- Open questions remain regarding the best practices for integrating new methodologies into current AI evaluation frameworks.


# Dynamic AI search evaluation framework and benchmarking strategies

Thu, 05 Jun 25

### Evaluation Principles for AI Search Systems

- Two guiding principles:
    
    - Web-based foundation requires keeping up with constant changes
        
    - Truth is often subjective and contextual, requiring unbiased evaluation methods
        

### Static vs Dynamic Evaluation Methods

- Static datasets:
    
    - SimpleQA: Benchmark for evaluating retrieval accuracy for single-answer questions
        
    - HardQA: Tests multi-hop questions requiring cross-document reasoning
        
- Dynamic evaluation advantages:
    
    - Real-world alignment
        
    - Broad coverage for any domain
        
    - Regular refreshes ensure latest data evaluation
        
    - Open-source agent available for building dynamic eval sets
        

### Dynamic Evaluation Process

- Three-step framework:
    
    - Generates broad web queries for targeted domains
        
    - Aggregates grounding documents from multiple AI search providers
        
    - Generates evidence-based Q&A pairs with answer context
        
- Uses Weights & Biases for experiment tracking
    

### Benchmarking Results

- Evaluation of 6 AI search providers using:
    
    - Static benchmark: SimpleQA dataset
        
    - Dynamic benchmark: ~1000 rows of generated data
        
- Reference-free metrics measured:
    
    - Answer completeness
        
    - Document relevance (0.94 correlation with performance scores)
        
    - Hallucination detection
        
- Key finding: Provider X showed highest hallucination rate but also highest document relevance
    

### Future Development

- Planned improvements:
    
    - Support for various question types
        
    - Enhanced fairness and coverage
        
    - Supervisor node for multi-agent architectures
        
    - Focus on continuous self-improvement capabilities
        
    - Automated hallucination detection and correction
        

---

Chat with meeting transcript: [https://notes.granola.ai/d/b0592656-1d66-4182-bca0-803a8958aec1](https://notes.granola.ai/d/b0592656-1d66-4182-bca0-803a8958aec1)