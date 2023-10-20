# Azure OpenAI Node.js Library

This is a fork of the official [OpenAI Node.js library](https://github.com/openai/openai-node) that has been adapted to support the Azure OpenAI API. The objective of this library is to minimize the changes required to migrate from the official OpenAI library to Azure OpenAI or revert back to OpenAI.

This library allows you to use Azure OpenAI's API without making any changes to your existing OpenAI code. You can simply add Azure information to your configuration and start using the Azure OpenAI model.

## Installation

To install this library, use the following command:
```bash
$ npm install azure-openai
```

## Usage

The library needs to be configured with your Azure OpenAI's key, endpoint and deploymentId. you can obtain these credentials from [Azure Portal](https://portal.azure.com). Please see the below screenshot:
![image](https://user-images.githubusercontent.com/26411726/225185239-6d1f3058-531c-4c7e-9496-8c2956d23f5d.png)

To migrate from the official OpenAI model to the Azure OpenAI model, you can just simply add **azure info into configuration** to migrate, that is it. You donot need to change any code. Please see the below steps:

1. Install the library by running the following command:
   ```bash
   npm install azure-openai
   ```

2. Update the import statement from "**openai**" to "**azure-openai**":
   ```typescript
   //import { Configuration, OpenAIApi } from "openai"; 
   import { Configuration, OpenAIApi } from "azure-openai"; 
   ```

3. Add the Azure OpenAI information to your project configuration:
   ```typescript
   this.openAiApi = new OpenAIApi(
      new Configuration({
         apiKey: this.apiKey,
         // add azure info into configuration
         azure: {
            apiKey: {your-azure-openai-resource-key},
            endpoint: {your-azure-openai-resource-endpoint},
            // deploymentName is optional, if you donot set it, you need to set it in the request parameter
            deploymentName: {your-azure-openai-resource-deployment-name},
            // deploymentName is optional, if you donot set it, `2023-03-15-preview` will be applied
            apiVersion: {your-azure-openai-resource-api-version},
         }
      }),
   );
   ```

4. run your code. That's it.

5. optional, if you use stream = true. you may need to change response
    ```
    // Azure OpenAI donot response delta data, so you need to change the response to text
    // const delta = parsed.choices[0].delta.content;
    const delta = parsed.choices[0].text;
    ```

6. optional, you can also set your Azure deploymentName by replacing your model with deployment name, like this:
    ```
    const response = await this.openAiApi.createCompletion({
      model: {your-azure-openai-resource-deployment-name},
      prompt: prompt,
      max_tokens: 100,
      top_p: 1,
      frequency_penalty: 0,
      presence_penalty: 0
    });
    ```

## Support
support latest version of OpenAI API, v3.2.0.

## Test
| API | Test Status | 
| --- | --- | 
| createChatCompletion | Pass |
| createCompletion | Pass |
| createEmbedding | Pass |
| createImage | Not Support |

Check [Azure OpenAI Rest Spec](https://github.com/Azure/azure-rest-api-specs/blob/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/preview/2023-03-15-preview/inference.json)

Please feel free to submit your [issues](https://github.com/1openwindow/azure-openai-node/issues) or pull requests to support other APIs.
