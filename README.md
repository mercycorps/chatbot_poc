# Mercy Corps: Proof of Concept Chatbot
This repository contains technical documentation for a proof-of-concept chatbot developed by Mercy Corps using Microsoft OpenAI studio. It is intended to help other humanitarian organizations experiment with their own proofs of concept as a way to explore approaches to infrastructure, safety, and security in the Azure environment. It is not intended to be a perfect solution, and users are responsible for ensuring the accuracy, reliability, and safety of their own results. 

This repository combines Microsoft Documentation with our own experiences and is composed of two primary files: 
- This `README` page provides background on the use-case, the overall philosophy of the project, and cost estimation. 
- The [Resource Deployment file of the repository](PoC_resource_deployment.md) provides the documentation used to establish the environment and launch the chatbot.

This repository should not be viewed as a step-by-step guide, rather, as a resource for Azure administrators and technologists who want to create a proof-of-concept. While we have tried to keep the documentation as clear as possible, successfully following this documentation will benefit from a familiarity with the Microsoft Azure environment and a firm understanding of data services architecture.

## Background
The increasing availability and ease of use of generative AI tools, such as ChatGPT, has led to increasing use of these tools for business purposes without oversight or governance. While these tools present significant opportunities, they also present significant risk. The prevalence of generative AI, whether as stand-alone tools or as features built-in to our existing enterprise level systems, is set to increase as more and more companies promote the technology. This means that staff need capacity building to better evaluate, use, or deploy generative AI as part of various operations. The objective of this project is to begin building this capacity by establishing basic infrastructure for building secure, safe, tools in a controlled environment.

This project is a collaboration between Mercy Corps' Data Protection & Privacy team (DPP), various functions within the IT department, and the Monitoring, Evaluation, and Learning team (MEL).

## Use Case
Mercy Corps has a large "Digital Library" of institutional knowledge and several teams have expressed an interest in using generative AI to explore various collections in the library. This proof of concept created a beta chat bot using a model for text generation to produce outputs based on authoritative Mercy Corps documentation. There are several significant outcomes of this project.  
- Providing a safe alternative to using tools like ChatGPT online, while providing commensurate user experience. In this case, “safe” is defined as: 
    - Ensuring that Mercy Corps' responsible data policy will govern the use of the technology. 
    - The risk of data leakage will be reduced because any inputs to the chatbot, such as accidentally incorporating personally identifiable information, will remain under the control of Mercy Corps and not parent companies.  
    - The parameters of the chatbot can be set to limit or mitigate “hallucinations” – or the fabrication of false information – by limiting the chatbots source material to that of the Digital Library, thereby ensuring that official Mercy Corps information is the primary source of information.  
- Adding value to the Digital Library by offering the ability to work in a range of languages, translate, and generally make the contents of the Digital Library more accessible.  
- A better understanding of how users interact with generative AI, the types of infrastructure or tools that Mercy Corps should build or invest in, and to build the capacity of teams and individuals involved in the project by working together to implement a generative AI solution in a safe environment.   

Initial prototype: From September through October 2023 DPP tested a prototype that created with [Exchange Design](https://www.exchange.design/). The prototype had relatively strict working parameters and was grounded in 46 documents selected by DPP and MEL. Overall, the bot performed well in summarizing documents; providing aggregate information; translating text; generating code for languages such as Python; and generating initial “brainstorming” ideas for things like logic frames, theories of change, etc. In conjunction with the value of mitigating risk by providing a safe and secure testing environment the team was overwhelmingly supportive of developing infrastructure internally.  

### Values: 
This project is being developed in accordance with ethical principles for the use of AI, with the stated purpose of understanding how the following can be implemented in a generative AI tool.  
- Fairness: How might an AI system allocate opportunities, resources, or information in ways that are fair to the humans who use it?
- Reliability and safety: How might the system function well for people across different use conditions and contexts, including ones it was not originally intended for? 
- Data Protection & Privacy: How might the system be designed to support privacy and security?
- Inclusiveness: How might the system be designed to be inclusive of people of all abilities? 
- Transparency: How might people misunderstand, misuse, or incorrectly estimate the capabilities of the system? 
- Accountability: How can we create oversight so that humans can be accountable and in control? 

### Additional Outputs
While this repository is dedicated to the technical work of building a chatbot, the overall project has two other primary outputs:
1. Research on the evolving regulatory landscape to support safeguarding and compliance objectives, including policy development.
2. The creation of processes and procedures to assess and inventory artificial intelligence systems in accordance with emerging regulations. 

## Key Features:
Our chatbot uses the [Retrieval Augmented Generation (RAG)](https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview) model for document intelligence using AI. This is the industry standard when proprietary data not already known to a large language model (LLM). The chatbot acts as "reference librarian" to select the most appropriate documents. ​However a weakness of RAG is that it cannot fully understand whether the data that is being retrieved is the most relevant information and relies heavily on how data are structured (e.g. [chunking](https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-chunk-documents), metadata, etc.)

![Mercy Corps' RAG Model](images/rag-architecture-diagram.png)

## Environment
This proof of concept was created in the Microsoft Azure environment with an E3 license. Understanding what is included in your license can be an art in itself and we found the following documentation incredibly helpful:
- [This page shows the details of what is included with an E3 license.](https://m365maps.com/files/Microsoft-365-E3.htm)
- [This page can be used to compare various licensing tiers](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/modern-work-plan-comparison---enterprise-2024-10-01.pdf). 

The documentation used to establish the environment and launch the chatbot can be found in the [Resource Deployment file of the repository](PoC_resource_deployment.md). 

## Cost Estimation
DPP analyzed costs of establishing, refining, and maintaining this chatbot for a three-month period during which was a period of fairly limited use. Broadly speaking, the chatbot could be used by a small team (e.g. 5 users) for around $1,000 per month. This assumes limited new document processing and each user submitting a few prompts daily or a few days of heavy usage per user. A more conservative estimate for expanding use of the bot to a much larger team and continuing to process new batches of documents would be $2,000 per month. Noted below are a few areas where the performance of services could be reduced. We strongly encourage system or business owners to track charges monthly to more precisely forecast future charges. 

The average monthly cost for this chatbot was $787.16. For the most part, these are the fixed, monthly costs for things like document storage and access to various services. The most significant cost for this is the "Cognitive search" service, which incurs charges of $749.95 / mo. This cost could be lowered by choosing a lower tier of service. For a small team, lowering the service tier and turning off options such as chat history, could significantly lower the monthly cost. See [Microsoft documentation for Azure AI search pricing here](https://azure.microsoft.com/en-us/pricing/details/search/) and accompanying [documentation for service tier pricing here](https://learn.microsoft.com/en-us/azure/search/search-sku-tier).

There are a few other services in the resource group that contribute to the overall charge, but most of these - taken together - run less than one dollar per day. The storage costs for this chatbot were extremely modest. The MEL team processed roughly 300 `.pdf` files with storage costs running under one dollar. Blob storage costs are estimated at is $0.21 month per 10GB of BLOB. 

The consumption charges for "tokenization" when creating prompts and receiving outputs is harder to gauge. We have calculated that, during the June - September period, there were 21 days of significant usage (e.g. uploading documents, testing various prompts and outputs, etc.). The average cost per day was $5.49 and this could be used as a rough measure for the likely cost of one user, per day, who is running a significant number of prompts. Adding documents to the chatbot requires additional processing and our estimates for one such session is that uploading and processing 200 documents to the chatbot costs roughly $30. 

