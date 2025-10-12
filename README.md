# Best Practices for LLM-based Development


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

- As you make updates to your system prompt tools, and other LLM
  parameters, you should not manually check the performance of your
  LLM-based applications. Instead, use an evaluation framework to
  automate this process.
  - If you’re using R, I recommend the
    [`vitals`](https://vitals.tidyverse.org/index.html) package and if
    you use Python, I recommend the
    [`Inspect`](https://inspect.aisi.org.uk/) library.

## Resources I’ve enjoyed

- https://ellmer.tidyverse.org/articles/prompt-design.html#best-practices
- 
