# Plan Commands Extension for Gemini CLI 
Gemini CLI commands to create, refine, implement and deploy a plan
An AI-powered extension for [Gemini CLI](https://github.com/google-gemini/gemini-cli) that facilites creating, refining, implementing and deploying a plan through natural conversation.

## Available Commands
* /plan:explain-project -  **Explore mode**. Interactively explains the codebase through guided discovery
* /plan:new - **Plan mode**. Generates a plan for a feature based on a description
* /plan:refine - **Refinement mode**. Refines an existing plan based on user feedback
* /plan:impl - **Implementation mode**. Implements a plan for a feature based on a description
* /plan:deploy - **Deployment mode**. Deploys the project to a target environment
* /review:review-code - Performs a code review on the specified code, providing feedback and suggestions

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
