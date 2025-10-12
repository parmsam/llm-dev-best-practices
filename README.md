# Best Practices for LLM-based Development


This document outlines best practices that I’ve learned for developing
applications using Large Language Models (LLMs). It will cover various
aspects including prompt engineering, model selection, performance
evaluation, and ethical considerations. This is a living document and
will be updated as I get more experience in this area.

## System prompts

- Place each system prompt in a separate Markdown (`.md`) file for
  better organization and readability.
- Use a consistent naming convention for your system prompt files to
  easily identify their purpose. I usually go with `system-prompt.md`.
- Commit your system prompts to version control (such as `git`) to track
  changes over time.
- Consider adding toggles into your system prompts to enable or disable
  certain features or behaviors. This can work well with interpolating
  variables into your prompts.
  - For example, you might have a toggle for verbosity, where setting
    `verbose=true` in your prompt would instruct the model to provide
    more detailed responses.

## Use an LLM evaluation framework

- Avoid manually testing your LLM applications when making changes to
  system prompts, tools, or model parameters. Manual evaluation is
  time-consuming, inconsistent, and doesn’t scale as your application
  grows.
- Implement an automated evaluation framework to systematically measure
  performance across different configurations and track improvements
  over time.
- Choose an evaluation framework based on your technology stack:
  - **R users**: Use the
    [`vitals`](https://vitals.tidyverse.org/index.html) package for
    comprehensive LLM evaluation workflows
  - **Python users**: Use the [`Inspect`](https://inspect.aisi.org.uk/)
    library for rigorous AI system evaluation
- Set up evaluation datasets that represent real-world use cases and
  edge cases your application might encounter.
- Track key metrics consistently (accuracy, relevance, safety, latency)
  to make data-driven decisions about model improvements.

## Resources I’ve enjoyed

- [Ellmer vignette on Prompt
  Design](https://ellmer.tidyverse.org/articles/prompt-design.html)
- [Max Kuhn - Measuring LLM Effectiveness - Presented at The New York
  Data Science & AI Conference Presented by Lander Analytics (August 27,
  2025)](https://www.youtube.com/embed/TQKbaIR-8J4)
