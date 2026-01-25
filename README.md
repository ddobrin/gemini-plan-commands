# Plan Commands Extension for usage with Gemini CLI and Gemini 3 Pro models
Gemini CLI commands to create, refine, implement and deploy a plan
An AI-powered extension for [Gemini CLI](https://github.com/google-gemini/gemini-cli) that facilites creating, refining, implementing and deploying a plan through natural conversation.

**Note:** The branch gemini-2-5 contains the previous set of instructions specific to 2.5 models

## Available Commands
* /plan:explain-project -  **Explore mode**. Interactively explains the codebase through guided discovery
* /plan:new - **Plan mode**. Generates a plan for a feature based on a description
* /plan:refine - **Refinement mode**. Refines an existing plan based on user feedback
* /plan:impl - **Implementation mode**. Implements a plan for a feature based on a description
* /plan:deploy - **Deployment mode**. Deploys the project to a target environment
* /plan:validate - **Validate mode**. Validate that a plan has been fully implemented in the codebase
* /review:review-code - Performs a code review on the specified code, providing feedback and suggestions
* /refactor:simplify-code - Simplifies and refines code for clarity, consistency, and maintainability while preserving all functionality
* /test:performance-tests - Generates a load testing script using the 'oha' library

## Available skills
* plan-explorer: Expertise in interactively explaining the codebase. Use when the user asks to "explain the project", "explore the code", or "how does this work".
* plan-author: Expertise in acting as a Staff Engineer to generate comprehensive implementation plans. Use when the user asks to "plan a feature", "create a new plan", or "design an architecture".
* plan-refiner: Expertise in refining architectural plans based on user feedback or new requirements. Use when the user asks to "update the plan", "change the plan", or "refine the strategy".
* plan-executor: Expertise in executing finalized architectural plans. Use when the user asks to "implement the plan", "build the feature", or "execute the strategy".
* plan-deployer: Expertise in deploying the project to a target environment. Use when the user asks to "deploy", "release", or "push to prod".
* plan-validator: Expertise in validating that the codebase matches a specific plan. Use when the user asks to "validate the plan", "check implementation", or "audit the code".
* code-simplifier: Expertise in simplifying and refining code for clarity, consistency, and maintainability while preserving all functionality. Use when the user asks to "simplify code", "refactor for clarity", or "clean up this file"
* database-analyst: Analyzes database schemas, migrations, ORM entities, and repository pattern across Java, Kotlin, and Python codebases. Identifies performance issues, N+1 queries, locking risks, normalization violations, and generates ERD documentation

## Prerequisites
Install the [Gemini CLI](https://github.com/google-gemini/gemini-cli)

**Learn more about** [Gemini CLI Extensions](https://github.com/google-gemini/gemini-cli/blob/main/docs/extensions/index.md)!  

## Extension Installation
From your command line:

```bash
gemini extensions install https://github.com/ddobrin/gemini-plan-commands
```

## Extension validation
Validate the extension from the command line:

```bash
gemini extensions validate
```

**Credits**: [@ddobrin](https://github.com/ddobrin), these commands have been copied from the [serverless production repository](https://github.com/GoogleCloudPlatform/serverless-production-readiness-java-gcp/tree/main/genai/quotes-llm/.gemini/commands)
