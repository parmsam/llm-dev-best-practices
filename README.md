# Best Practices for LLM-based Development

This document outlines best practices that I've learned for developing applications using Large Language Models (LLMs). It will cover various aspects including prompt engineering, model selection, performance evaluation, and ethical considerations. This is a living document and will be updated as I get more experience in this area.

## System prompts

`System prompts` define general behavior for your LLM application. They set the context and guidelines for how the model should respond to `user prompts` (which usually ask specific questions).

- Place each system prompt in a separate Markdown (`.md`) file for better organization and readability.
- Use a consistent naming convention for your system prompt files to easily identify their purpose. I usually go with `system-prompt.md`.
- Commit your system prompts to version control (such as `git`) to track changes over time.
- Interpolate dynamic data into your system prompts to customize behavior based on context. This can include user preferences, application state, or specific instructions for the task at hand.
  - Consider adding toggles into your system prompts to enable or disable certain features or behaviors. This can work well with interpolating variables into your prompts.
  - For example, you might have a toggle for verbosity, where setting `verbose=true` in your prompt would instruct the model to provide more detailed responses.
- Be explicit and clear in your system prompts to minimize ambiguity. Clearly define the role of the model, the expected format of responses, and any constraints or guidelines it should follow. There are many frameworks and guidelines available online to help with this.

### Curate the context

- If you want your LLM to provide accurate and relevant responses, it's crucial to provide it with the right context. This can be done by including relevant information in the system prompt (`prompt stuffing`) or by using techniques like retrieval-augmented generation (`RAG`) to fetch pertinent data from external sources.
- Provide examples of desired outputs in the system prompt to guide the model's responses.
- Provide sufficient background information and details relevant to the target user group.
- Regularly update the context to ensure it remains relevant and accurate as your application evolves.

## Work in small pieces and iterate

- Break down complex tasks into smaller, manageable components. This makes it easier to test and refine individual parts of your application.
- Follow the [SolveIt approach](https://parmsam.github.io/garden/solve-it) for iterative LLM-assisted code development and problem-solving:
  - Understand the Problem
  - Devise a Plan
  - Carry Out the Plan
  - Look Back and Reflect
- Start with a minimal viable product (MVP) and gradually add features and complexity based on user feedback and testing. The same principles from [lean startups](https://en.wikipedia.org/wiki/Lean_startup) apply here.

## Use an LLM evaluation framework

- Avoid manually testing your LLM applications when making changes to system prompts, tools, or model parameters. Manual evaluation is time-consuming, inconsistent, and doesn't scale as your application grows.
- Implement an automated evaluation framework to systematically measure performance across different configurations and track improvements over time.
- Choose an evaluation framework based on your technology stack:
  - **R users**: Use the [`vitals`](https://vitals.tidyverse.org/index.html) package for comprehensive LLM evaluation workflows
  - **Python users**: Use the [`Inspect`](https://inspect.aisi.org.uk/) library for rigorous AI system evaluation
- Set up evaluation datasets that represent real-world use cases and edge cases your application might encounter.
- Track key metrics consistently (accuracy, relevance, safety, latency) to make data-driven decisions about model improvements.

### Maintain your evaluation datasets

- Regularly update your evaluation datasets to reflect changes in user needs, application features, and model capabilities.

### Ensure you evaluate both answerable and unanswerable questions

- Your evaluation datasets should include a mix of questions that the model can answer and questions that it cannot. This helps assess the model's ability to handle uncertainty and avoid hallucinations. 
- You can check if the model appropriately indicates when it doesn't know the answer or when a question is outside its knowledge scope.

## Maintain your knowledge store

- If your application uses a knowledge base or retrieval system to provide context to the LLM, ensure that this knowledge store is regularly updated and maintained.      
  - This includes adding new information, removing outdated content, and ensuring data quality. This is an easy aspect to overlook but is crucial for maintaining the accuracy and relevance of your LLM's responses.

## Know your models and their limitations

- Different LLMs have varying strengths and weaknesses. Familiarize yourself with the capabilities and limitations of the models you are using.
- This may be obvious but choose the right model for the task at hand. For example, use models optimized for R code generation when building R coding assistants.
  - Use smaller, cheaper models for simple tasks and reserve powerful models for complex ones.
- Important factors include token limits, training cut-off dates, release date, cost, rate limits, modalities, and specific biases. This knowledge is acquired through reading official documentation, online research, and experimentation.

## Security and Privacy

- Store API keys and sensitive credentials in environment variables or secure credential stores, never in code
- Implement data anonymization and ensure compliance with privacy regulations (GDPR, CCPA) when sending user data to LLM APIs
- Validate and sanitize user inputs to prevent prompt injection attacks for applications that external users can interact with

## Production Deployment

- Consider caching LLM responses for repeated queries to reduce costs and improve performance
- Set up monitoring for response times, error rates, token usage, and costs
- Design fallback strategies when primary LLM services are unavailable

## User Transparency

- Clearly communicate when and how LLMs are being used in your application
- Provide users with information about the solution's capabilities and limitations

## Resources I've enjoyed learning from

- [Ellmer vignette on Prompt Design](https://ellmer.tidyverse.org/articles/prompt-design.html)
- [Max Kuhn - Measuring LLM Effectiveness - Presented at The New York Data Science & AI Conference Presented by Lander Analytics (August 27, 2025)](https://www.youtube.com/embed/TQKbaIR-8J4)
- [A Field Guide to Rapidly Improving AI Products from Humal Husain's blog](https://hamel.dev/blog/posts/field-guide/)
- [Frequently Asked Questions (And Answers) About AI Evals from Hamel Husain's blog](https://hamel.dev/blog/posts/evals-faq/index.html)
- [Here's how I use LLMs to help me write code from Simon Willison's blog](https://simonwillison.net/2025/Mar/11/using-llms-for-code/)
- [Lean Startup methodology Wiki article](https://en.wikipedia.org/wiki/Lean_startup)
- [The Solveit approach turns frustrating AI conversations into learning experiences from Rens'Blog](http://rensdimmendaal.com/posts/solveit-course-key-take-aways)