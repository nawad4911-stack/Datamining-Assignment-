# CSAI 422 – Assignment 3: Conversational Weather Agent  

## Getting Started  

### 1. Install Required Packages  

Run the following command to install all dependencies:  

```bash
pip install -r requirements.txt
```

### 2. Configure Environment Variables  

Inside the project directory, create a file named `.env` and include the following variables:  

```env
API_KEY=your_api_key
BASE_URL=your_base_url
LLM_MODEL=your_model_name
WEATHER_API_KEY=your_weatherapi_key
```

### 3. Launch the Application  

Start the agent using:  

```bash
python conversational_agent.py
```

---

## Project Summary  

This project builds a conversational weather assistant that can respond to user queries by integrating external tools and applying reasoning techniques.

### 1. Basic Agent  

The Basic Agent is designed to handle straightforward weather-related questions. It utilizes tool calling to fetch current conditions or forecasts and generates human-readable responses.

### 2. Chain of Thought Agent  

This version enhances the Basic Agent by introducing:  

- A calculator tool  
- Step-by-step reasoning  
- Support for comparisons and numerical operations  

### 3. Advanced Agent  

The Advanced Agent further expands capabilities by including:  

- Robust error handling for tool execution  
- Both parallel and sequential tool usage  
- Multi-step reasoning workflows  
- Structured JSON responses for complex queries  

### Bonus: Evaluation Framework  

An evaluation component is included to compare agents based on:  

- Quality of responses  
- Execution speed  
- Performance differences between sequential and parallel processing  

---

## Sample Interactions  

### Basic Agent  

**User:** What is the weather in Cairo?  
**Assistant:** The current temperature in Cairo is 25°C with clear skies.  

---

### Chain of Thought Agent  

**User:** What is the temperature difference between Cairo and London?  
**Assistant:**  

- Cairo: 25°C  
- London: 15°C  
- Difference = 10°C  

Therefore, Cairo is 10°C warmer than London.  

---

### Advanced Agent  

**User:** Compare Cairo, Dubai, and Paris and tell me which is warmer.  

**Assistant (JSON output):**  

```json
{
  "query_type": "comparison",
  "locations": ["Cairo", "Dubai", "Paris"],
  "summary": "Dubai has the highest temperature among the three cities.",
  "tool_calls_used": ["get_current_weather"],
  "final_answer": "Dubai is the warmest city currently."
}
```

---

## Discussion  

The three agent types illustrate a progression in reasoning ability and performance:  

- The Basic Agent is fast and suitable for simple queries but lacks depth for complex tasks.  
- The Chain of Thought Agent improves accuracy by decomposing problems and performing calculations.  
- The Advanced Agent delivers the most robust performance by:  
  - Running multiple tool calls simultaneously  
  - Managing multi-step reasoning processes  
  - Producing structured and interpretable outputs  

Notably, parallel execution reduces response time significantly when handling multiple locations compared to sequential processing.  

---

## Challenges and Resolutions  

### 1. API Failures  

Some requests failed due to invalid inputs or connectivity issues.  
**Fix:** Implemented error handling to ensure safe tool execution.  

### 2. Multi-step Reasoning Issues  

The agent initially struggled with completing tasks requiring multiple steps.  
**Fix:** Introduced iterative execution with a capped loop for reasoning steps.  

### 3. JSON Output Consistency  

Maintaining valid structured output was difficult.  
**Fix:** Added validation checks to enforce required JSON fields.  

### 4. Environment Setup  

Managing API keys caused initial setup problems.  
**Fix:** Adopted `.env` configuration using `python-dotenv`.  

---

## Resources  

- OpenAI Function Calling Guide:  
  https://platform.openai.com/docs/guides/function-calling  

- OpenAI Structured Outputs Guide:  
  https://platform.openai.com/docs/guides/structured-outputs  

- WeatherAPI Documentation:  
  https://www.weatherapi.com/docs/  

- OpenRouter Documentation:  
  https://openrouter.ai/docs  

---

## Additional Notes  

The project uses OpenRouter as the language model provider, which is compatible with the OpenAI API. As a result, OpenAI documentation served as the main reference for implementing tool calling and structured outputs.  

For security reasons, the `.env` file is excluded from the repository.  
