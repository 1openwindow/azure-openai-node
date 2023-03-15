# Azure OpenAI Node.js Library

This is a fork of the official [OpenAI Node.js library](https://github.com/openai/openai-node) that has been adapted to support the Azure OpenAI API. The objective of this library is to minimize the changes required to migrate from the official OpenAI library to Azure OpenAI or revert back to OpenAI.
## Installation

To install this library, use the following command:
```bash
$ npm install azure-openai
```

## Usage

The library needs to be configured with your Azure OpenAI's key, endpoint and deploymentId. you can obtain these credentials from [Azure Portal](https://portal.azure.com). Please see the below screenshot:
![image](https://user-images.githubusercontent.com/26411726/225185239-6d1f3058-531c-4c7e-9496-8c2956d23f5d.png)

To migrate from the official OpenAI model to the Azure OpenAI model, please follow these steps:

1. Install the library by running the following command:
   ```
   $ npm install azure-openai
   ```

2. Update the import statement from "**openai**" to "**azure-openai**":
   ```
   //import { Configuration, OpenAIApi } from "openai"; 
   import { Configuration, OpenAIApi } from "azure-openai"; 
   ```

3. Pass the **key** and **endpoint** in the configuration:
    ```
    this.openAiApi = new OpenAIApi(
      new Configuration({
        // this is the key of auzre openai resource
        apiKey: {your-azure-openai-resource-key},
        // this is the endpoint of auzre openai resource. Add this line to pass the base path
        basePath: "https://${your-azure-openai-resource-name}.openai.azure.com/",
      })
    );
    ```

4. update **deploymentId** in model parameter when send request to Azure OpenAI:
   ```
   const completion = await this.openAiApi.createCompletion({
      // this is the deploymentId of auzre openai resource. pass the deployment id into model parameter
      model: ${your-azure-openai-resource-deploymentId},
      prompt: "Hello world",
      ......
    });
   ```

5. optional, if you use stream = true. you may need to change response
    ```
    // Azure OpenAI donot response delta data, so you need to change the response to text
    // const delta = parsed.choices[0].delta.content;
    const delta = parsed.choices[0].text;
    ```

## Test
Currently, only "gpt-3.5-turbo" API has been tested. Please feel free to submit your issues or pull requests to support other APIs.