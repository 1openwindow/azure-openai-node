# Azure OpenAI Node.js Library

this is a fork of the official [OpenAI Node.js library](https://github.com/openai/openai-node) to support the Azure OpenAI API.
the objective is to minimize the changes that migrate from the official library to Azure OpenAI or revert back to OpenAI.

## Installation

```bash
$ npm install azure-openai
```

## Usage

The library needs to be configured with your Azure OpenAI's key, endpoint and deploymentId. you can obtain them from [Azure Portal](https://portal.azure.com).  
 
the following is the step to migrate from OpenAI model to Azure OpenAI model.
1. install the library
   ```
   $ npm install azure-openai
   ```

2. 
The library needs to be configured with your account's secret key, which is available on the [website](https://beta.openai.com/account/api-keys). We recommend setting it as an environment variable. Here's an example of initializing the library with the API key loaded from an environment variable and creating a completion:

```javascript
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
  basePath: //////////////////,
});
const openai = new OpenAIApi(configuration);

const completion = await openai.createCompletion({
  model: "///////////////",
  prompt: "Hello world",
});
console.log(completion.data.choices[0].text);
```