HAL Agentflow: No-Code Agentic Workflow Builder
<p align="center">
<strong>Translate natural language into structured, executable JSON workflows.</strong>
</p>

HAL Agentflow is a powerful backend application that uses a multi-agent system built with LangGraph to process, plan, validate, and refine user requests. It transforms simple descriptions of a process into robust, high-quality JSON workflows ready for execution.

✨ Key Features
Natural Language to Workflow: Simply describe a process, and the system generates a corresponding JSON graph.

Agentic Architecture: Leverages a graph of specialized AI agents (nodes) for different tasks like planning, validation, and refinement.

Multi-Layered Validation:

Structural: Fast, programmatic check for valid JSON and graph connectivity.

Logical: LLM-based check for business logic and data flow coherence.

Hallucination: Ensures the workflow only uses components that actually exist.

Self-Correction Loop: If a workflow fails validation, it's automatically sent to a Refiner agent with feedback to fix the errors.

Intelligent Fallback: If the main agent graph fails, a powerful fallback mechanism can generate a workflow, even inventing necessary components to fulfill the user's request.

Dynamic LLM Support: Easily switch between LLM providers (Google Gemini, Azure OpenAI) via environment variables.

📂 Project Structure
The project is organized with a clear separation of concerns, from the core application logic to the static configurations and frontend templates.

/hal-agentflow
├── IO/
│   ├── HAL_Config.json
│   ├── HAL_Input_Schema.json
│   ├── HAL_Output_Schema.json
│   ├── HAL_Input_Sample.json
│   └── HAL_Output_Sample.json
├── nodes/
│   ├── __init__.py
│   ├── clarification_node.py
│   ├── nlp_preprocessor_node.py
│   ├── planner_node.py
│   ├── quality_grader_node.py
│   ├── refiner_node.py
│   └── validation_nodes.py
├── static/
│   ├── agents.json
│   ├── tools.json
│   └── prompt.json
├── templates/
│   └── index.html
├── app.py
├── state.py
├── workflow.py
├── utils.py
├── .env
└── requirements.txt

Schemas & Data Contracts
The IO/ directory contains the formal data contracts that define the inputs HAL accepts and the outputs it produces. This ensures clear communication and seamless integration with other teams and systems.

HAL_Config.json: Defines the input schema for configuring a HAL workflow generation request, specifying data sources for prompts and components.

HAL_Input_Schema.json: The formal JSON Schema contract for HAL_Config.json.

HAL_Output_Schema.json: The formal JSON Schema contract for the workflow object that HAL generates.

HAL_Input_Sample.json: A sample HAL_Config.json file showing a valid request structure.

HAL_Output_Sample.json: A sample of a successfully generated workflow object.

🚀 Getting Started
1. Setup and Installation
Clone the Repository

git clone <your-repository-url>
cd hal-agentflow

Create a Virtual Environment

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

Install Dependencies

pip install -r requirements.txt

2. Configure Environment Variables
Create a .env file in the root directory and add the necessary credentials for your chosen LLM provider.

For Google Gemini:

MODEL_PROVIDER="Google"
GOOGLE_API_KEY="YOUR_GOOGLE_AI_STUDIO_API_KEY"
PORT=5005

For Azure OpenAI:

MODEL_PROVIDER="AzureOpenAI"
AZURE_OPENAI_API_KEY="YOUR_AZURE_OPENAI_KEY"
AZURE_OPENAI_ENDPOINT="YOUR_AZURE_OPENAI_ENDPOINT"
AZURE_OPENAI_DEPLOYMENT_NAME="YOUR_DEPLOYMENT_NAME"
AZURE_OPENAI_API_VERSION="YOUR_API_VERSION"
PORT=5005

3. Run the Application
With your virtual environment activated, start the Flask server:

python app.py

The backend will be running on http://localhost:5005. You can interact with the application by opening the templates/index.html file in your browser.

⚙️ How It Works
A user enters a prompt into the web UI (e.g., "When a new invoice PDF arrives, extract the data...").

The Flask backend receives the prompt at the /generate-workflow endpoint.

The LangGraphOrchestrator is invoked, starting the agentic graph.

Clarification Node: Checks if the prompt is ambiguous. If so, it returns questions to the user.

NLP Preprocessor Node: Extracts intent and domain, and refines the prompt.

Planner Node: Generates the first draft of the workflow JSON.

Validation Nodes: The JSON is passed through structural, logical, and hallucination checks.

Refiner Node: If any validation fails, the workflow and error messages are sent to the refiner, which attempts a fix. The corrected version is then sent back to the validation nodes.

Quality Grader Node: Once a workflow passes all validations, this node gives it a final score and feedback.

The final, validated JSON is sent back to the frontend to be displayed.
