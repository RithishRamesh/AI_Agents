# Azure OpenAI Integration for Router AI Agent

This README explains how to set up the **API key** and **Azure endpoint** for the **Azure OpenAI** service and how to integrate them into the **Router AI Agent** system.

## Steps to Set Up API Key and Azure Endpoint for Azure OpenAI

### **Step 1: Create an Azure OpenAI Account**
1. Go to the [Azure portal](https://portal.azure.com/).
2. Search for **"Azure OpenAI"** in the search bar.
3. Create a new **Azure OpenAI resource** in the region that suits your needs (such as East US, West Europe, etc.).
4. During the process, Azure will assign you an **API key** and **endpoint URL**. This API key will allow you to make requests to the Azure OpenAI models, and the endpoint is the URL where you can send those requests.

### **Step 2: Retrieve API Key and Azure Endpoint**
1. After creating the Azure OpenAI resource, go to the resource page in the Azure portal.
2. On the left panel, under the **Keys and Endpoint** section, you’ll find the following details:
   - **API Key**: This is the key that you’ll use to authenticate your requests.
   - **Endpoint**: This is the URL that you will use to connect to the OpenAI service (usually it looks something like `https://<your-resource-name>.openai.azure.com/`).
   - **API Version**: You will also need to use the correct API version when making requests. In this case, it's `"2024-05-01-preview"`.

### **Step 3: Set Up the API Key and Endpoint in Your Code**

In your Python code, set the **API key** and **Azure endpoint** as follows:

```python
# API info. Replace with your own keys and endpoint
api_key = "your-api-key-here"  # Replace with the actual API key from Azure
azure_endpoint = "https://<your-resource-name>.openai.azure.com/"  # Replace with your Azure OpenAI endpoint
api_version = "2024-05-01-preview"  # API version, replace with your version if needed
```
**api_key**: This is where you insert the API key you obtained from Azure.

**azure_endpoint**: This is where you insert the endpoint URL of your Azure OpenAI resource. The URL typically follows this format:

https://<your-resource-name>.openai.azure.com/

Replace <your-resource-name> with the actual resource name you created in Azure.

**api_version**: This is the version of the API you're using. The version in the code ("2024-05-01-preview") should match the version provided by Azure for the specific models you are working with.

### **Step 4: Use the API Key and Endpoint in the Application**
Once the API key and endpoint are set up, you can use them to create an LLM connection and interact with the Azure OpenAI models. This will allow you to send requests and receive responses.

Example of setting up the connection:

```python
Copy
from llama_index.llms.azure_openai import AzureOpenAI
from llama_index.embeddings.azure_openai import AzureOpenAIEmbedding
from llama_index.core import Settings

# Setup the LLM connection using the API key and endpoint
Settings.llm = AzureOpenAI(
    model="gpt-35-turbo",  # Choose the model you want to use, like GPT-3.5 Turbo
    deployment_name="agentai-gpt35",  # The deployment name in your Azure OpenAI resource
    api_key=api_key,  # Your Azure API key
    azure_endpoint=azure_endpoint,  # Your Azure endpoint
    api_version=api_version  # The API version
)

# Setup the embedding model
Settings.embed_model = AzureOpenAIEmbedding(
    model="text-embedding-ada-002",  # Choose the embedding model, like text-embedding-ada-002
    deployment_name="agentai-embedding",  # The deployment name in your Azure OpenAI resource
    api_key=api_key,  # Your Azure API key
    azure_endpoint=azure_endpoint,  # Your Azure endpoint
    api_version=api_version  # The API version
)
```

### **Step 5: Test the Setup**
Once you've set up the API key and endpoint, and connected to Azure OpenAI using the code above, you can test the connection by querying the LLM or using it for embedding.

Example query:

```python
response = Settings.llm.query("Hello, how are you?")
print(response)
```
If everything is set up correctly, the system will send the query to Azure OpenAI and return the response.

Security Tips for API Keys
Never hardcode API keys: It's best practice to avoid hardcoding sensitive information such as API keys directly in the code, especially in public repositories. Instead, store them securely in environment variables or a secrets manager.

Use environment variables: You can use os.getenv() to load the API key and endpoint from environment variables:

```python
api_key = os.getenv("AZURE_API_KEY")
azure_endpoint = os.getenv("AZURE_ENDPOINT")
```

### **Summary**
**API Key**: You retrieve this from the Azure portal once you create the OpenAI resource. It’s used to authenticate requests to the Azure OpenAI service.

**Azure Endpoint**: This is the URL provided by Azure for your OpenAI service resource, and you need it to make API calls.

**How to Set Up**: Store the API key and endpoint in your code (or environment variables) and configure them when setting up your LLM connection in your Python code.

Let me know if you need further clarification or assistance with the setup!