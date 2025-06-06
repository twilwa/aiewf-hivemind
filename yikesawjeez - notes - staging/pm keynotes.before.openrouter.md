---
title: "State of AI Engineering Survey 2025 - Early Findings and Evaluation Trends"
source: "AI Engineering Conference 2025"
author: "Multiple speakers including Ankur Goyal (Braintrust CEO)"
created: 2025-06-05
tags:
  - highlight
  - ai-engineering
  - survey-data
  - evaluation
  - braintrust
  - multimodal
  - agents
  - fine-tuning
  - rag
  - openrouter
description: "Early findings from the 2025 State of AI Engineering Survey covering industry trends, evaluation practices, multimodal adoption, and the introduction of Loop - an automated evaluation optimization tool"
---


### AI Model Cost Analysis

- Chinese AI labs currently lead both reasoning and non-reasoning open weight models
    
    - BTC holds top position
        
    - Alibaba’s QUINT3 series ranks second in reasoning
        
    - Meta and NVIDIA’s Nemotron (Llama fine-tunes) following closely
        

### Cost Comparison Metrics

- Intelligence Index Running Costs:
    
    - GPT-3 (O3): ~$2,000
        
    - GPT-4.1: ~30x cheaper than GPT-3
        
    - GPT-4.1 Nano: ~500x cheaper than GPT-3
        

### Implementation Considerations

- Cost structure should drive application architecture decisions
    
- Sequential API calls comparison:
    
    - Can run 500 calls with GPT-4.1 Nano for less cost than single GPT-3 query
        
    - 30 sequential API calls with GPT-4.1 remain cost-effective
        
- Important to consider total Intelligence Index cost rather than just per-token pricing
    
    - Labs may discourage this comprehensive cost analysis approach
        

### Next Steps

- Review cost implications for current applications
    
- Consider model selection based on cost-to-performance ratio
    
- Evaluate sequential API call strategies based on cost structure
    

---

Chat with meeting transcript: https://notes.granola.ai/d/2b773dbf-9c87-4157-88aa-f8ae96cf63b5