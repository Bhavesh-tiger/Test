<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HAL Agentflow - Interactive Guide</title>
    <!-- Chosen Palette: Warm Neutral -->
    <!-- Application Structure Plan: The SPA is designed as a narrative journey to understand HAL. It starts with a high-level introduction, then presents the core "Generation Lifecycle" as an interactive flowchart. This is followed by a detailed, interactive breakdown of the Input Schema, the available components (Agents/Tools), and the Output Schema. This thematic, top-down structure was chosen because it guides a new user from the 'what' to the 'how', making the complex system digestible. It prioritizes the user's learning path over simply mirroring the README's document structure. -->
    <!-- Visualization & Content Choices: The core Generation Lifecycle is visualized using a custom flowchart built with HTML and Tailwind CSS borders, avoiding SVG/Mermaid. This diagram is interactive; clicking a step reveals its details. The Input Schema is presented as an interactive "explorer" where hovering over keys reveals descriptions, which is more engaging than a static table. Goal: Organize/Inform -> Method: Interactive Diagram/Explorer -> Interaction: Click/Hover -> Justification: Breaks down complex processes and schemas into manageable, explorable parts, enhancing user understanding. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #F7F5F2; /* Warm Neutral Background */
            color: #44403C; /* Stone 700 */
        }
        .accent-color { color: #EA580C; } /* Orange 600 */
        .accent-bg { background-color: #EA580C; }
        .card {
            background-color: #FFFFFF;
            border-radius: 0.75rem;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
            transition: all 0.2s ease-in-out;
        }
        .card:hover {
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
            transform: translateY(-2px);
        }
        .flow-step {
            border: 2px solid #E7E5E4; /* Stone 200 */
            cursor: pointer;
        }
        .flow-step.active {
            border-color: #EA580C;
            box-shadow: 0 0 15px rgba(234, 88, 12, 0.2);
        }
        .flow-arrow {
            font-size: 2rem;
            color: #A8A29E; /* Stone 400 */
        }
        .json-key {
            color: #92400E; /* Amber 800 */
            font-weight: 600;
            cursor: pointer;
        }
        .json-string { color: #059669; } /* Emerald 600 */
        .json-special { color: #EA580C; }
        .tooltip {
            position: absolute;
            display: none;
            background-color: #292524; /* Stone 800 */
            color: #F7F5F2;
            padding: 0.5rem 0.75rem;
            border-radius: 0.5rem;
            font-size: 0.875rem;
            z-index: 10;
            max-width: 300px;
            pointer-events: none;
        }
        .nav-link.active {
            color: #EA580C;
            font-weight: 600;
        }
    </style>
</head>
<body class="antialiased">

    <!-- Header & Navigation -->
    <header class="bg-white/80 backdrop-blur-lg sticky top-0 z-50 border-b border-stone-200">
        <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex items-center">
                    <span class="text-2xl font-bold accent-color">HAL Agentflow</span>
                </div>
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-4">
                        <a href="#overview" class="nav-link text-stone-500 hover:accent-color px-3 py-2 rounded-md text-sm font-medium transition">Overview</a>
                        <a href="#lifecycle" class="nav-link text-stone-500 hover:accent-color px-3 py-2 rounded-md text-sm font-medium transition">Lifecycle</a>
                        <a href="#input-schema" class="nav-link text-stone-500 hover:accent-color px-3 py-2 rounded-md text-sm font-medium transition">Input Schema</a>
                        <a href="#components" class="nav-link text-stone-500 hover:accent-color px-3 py-2 rounded-md text-sm font-medium transition">Components</a>
                    </div>
                </div>
            </div>
        </nav>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">

        <!-- Section 1: Overview -->
        <section id="overview" class="text-center py-16">
            <h1 class="text-4xl md:text-5xl font-bold tracking-tight text-stone-900">No-Code Agentic Workflow Builder</h1>
            <p class="mt-6 max-w-3xl mx-auto text-lg text-stone-600">
                HAL Agentflow is a powerful backend application that translates natural language descriptions into structured, executable JSON workflows. It uses a multi-agent system to process, plan, validate, and refine user requests, ensuring robust and high-quality output.
            </p>
        </section>

        <!-- Section 2: The Generation Lifecycle -->
        <section id="lifecycle" class="py-16">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-stone-900">The Generation Lifecycle</h2>
                <p class="mt-4 max-w-2xl mx-auto text-stone-600">HAL uses a sophisticated, multi-step process to ensure every generated workflow is accurate and robust. Click on any step to learn more about its role.</p>
            </div>
            <div class="flex flex-col items-center space-y-4">
                <!-- Flowchart Diagram -->
                <div id="flow-step-query" class="flow-step card w-full max-w-md p-4 text-center">
                    <h3 class="font-semibold text-stone-800">1. User Query</h3>
                    <p class="text-sm text-stone-500">The process starts with a natural language prompt.</p>
                </div>
                <div class="flow-arrow">↓</div>
                <div id="flow-step-clarification" class="flow-step card w-full max-w-md p-4 text-center">
                    <h3 class="font-semibold text-stone-800">2. Clarification</h3>
                     <p class="text-sm text-stone-500">Identifies and resolves ambiguities.</p>
                </div>
                <div class="flow-arrow">↓</div>
                <div id="flow-step-plan" class="flow-step card w-full max-w-md p-4 text-center">
                    <h3 class="font-semibold text-stone-800">3. Planning & Validation</h3>
                     <p class="text-sm text-stone-500">Generates and rigorously checks the workflow.</p>
                </div>
                 <div class="flow-arrow">↓</div>
                <div id="flow-step-output" class="flow-step card w-full max-w-md p-4 text-center">
                    <h3 class="font-semibold text-stone-800">4. Final Workflow</h3>
                     <p class="text-sm text-stone-500">A validated, executable JSON is produced.</p>
                </div>
            </div>
            <!-- Details Panel for Flowchart -->
            <div id="lifecycle-details" class="mt-12 card p-8 min-h-[200px] max-w-3xl mx-auto">
                <h3 id="details-title" class="text-2xl font-bold accent-color"></h3>
                <p id="details-text" class="mt-4 text-stone-600"></p>
            </div>
        </section>

        <!-- Section 3: Input Schema -->
        <section id="input-schema" class="py-16">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-stone-900">Configuring a Request: The Input Schema</h2>
                <p class="mt-4 max-w-2xl mx-auto text-stone-600">To generate a workflow, you provide HAL with a configuration object. This schema defines how to specify your query and data sources. Hover over any key for a detailed description.</p>
            </div>
            <div class="card max-w-3xl mx-auto">
                <div class="p-6 bg-stone-800 rounded-t-lg text-stone-300 font-mono text-sm">
                    HAL_Input_Schema.json
                </div>
                <div class="p-6 font-mono text-sm bg-stone-50 rounded-b-lg">
                    <pre>{
    <span class="json-key" data-tooltip="The unique identifier for the project.">"projectId"</span>: <span class="json-string">"Workflow_Agentflow_v1_main"</span>,
    <span class="json-key" data-tooltip="The version of the workflow configuration.">"version"</span>: <span class="json-string">"1.0.0"</span>,
    <span class="json-key" data-tooltip="A unique identifier for this specific workflow run.">"workflowId"</span>: <span class="json-string">"Workflow_agentflow_1"</span>,
    <span class="json-key" data-tooltip="The framework used to execute the workflow (e.g., 'langgraph').">"workflowFramework"</span>: <span class="json-string">"langgraph"</span>,
    <span class="json-key" data-tooltip="The original user query in natural language.">"userQuery"</span>: <span class="json-string">"user query for workflow"</span>,
    <span class="json-key" data-tooltip="An object containing all data source and model configurations.">"configuration"</span>: {
        <span class="json-key" data-tooltip="Defines how to fetch system prompts from a database.">"promptSource"</span>: {
            <span class="json-key" data-tooltip="Must be 'database'.">"type"</span>: <span class="json-string">"database"</span>,
            <span class="json-key" data-tooltip="The ID of the secret in a secret manager that holds the database connection string.">"connectionSecretId"</span>: <span class="json-string">"..."</span>,
            <span class="json-key" data-tooltip="The SQL query to execute to fetch the prompts.">"query"</span>: <span class="json-string">"SELECT ..."</span>
        },
        <span class="json-key" data-tooltip="Defines how to fetch available agents and tools from an API.">"componentSource"</span>: {
            <span class="json-key" data-tooltip="Must be 'api'.">"type"</span>: <span class="json-string">"api"</span>,
            <span class="json-key" data-tooltip="The base URL for the component service API.">"baseUrl"</span>: <span class="json-string">"..."</span>,
            <span class="json-key" data-tooltip="An object defining the API authentication method.">"authentication"</span>: { ... },
            <span class="json-key" data-tooltip="An object containing the specific paths for agents and tools.">"endpoints"</span>: { ... }
        },
        <span class="json-key" data-tooltip="Defines the language model to be used for generation.">"modelConfig"</span>: { ... }
    }
}</pre>
                </div>
            </div>
        </section>

        <!-- Section 4: Components -->
        <section id="components" class="py-16">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-stone-900">The Building Blocks: Agents & Tools</h2>
                <p class="mt-4 max-w-2xl mx-auto text-stone-600">HAL builds workflows by combining two types of components: high-level **Agents** for complex tasks and granular **Tools** for specific actions.</p>
            </div>
            <div class="max-w-3xl mx-auto">
                <div class="flex justify-center border-b border-stone-200 mb-6">
                    <button id="agents-btn" class="component-btn py-3 px-6 text-lg font-semibold border-b-2 border-orange-600 text-orange-600">Agents</button>
                    <button id="tools-btn" class="component-btn py-3 px-6 text-lg font-semibold border-b-2 border-transparent text-stone-500">Tools</button>
                </div>
                <div id="components-content">
                    <!-- Content will be injected here -->
                </div>
            </div>
        </section>

    </main>
    
    <div id="tooltip-box" class="tooltip"></div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const lifecycleSteps = {
                query: {
                    title: '1. User Query',
                    text: 'Everything begins with a user\'s request in natural language. This could be a simple instruction like "Email a report" or a complex, multi-step process. HAL is designed to understand the intent behind the user\'s words.'
                },
                clarification: {
                    title: '2. Clarification & Refinement',
                    text: 'To avoid errors, the Clarification Node first checks the prompt for ambiguity. If critical details are missing (like a filename or an email address), it can ask the user for more information. The prompt is then refined for the next stage.'
                },
                plan: {
                    title: '3. Planning & Multi-Layered Validation',
                    text: 'The Planner Node generates an initial workflow. This draft is then rigorously tested by three validation agents: Structural (checks JSON format), Logical (checks data flow and business logic), and Hallucination (ensures only existing components are used). If any check fails, a Refiner agent attempts to fix the workflow, creating a self-correction loop.'
                },
                output: {
                    title: '4. Final Workflow Output',
                    text: 'Once a workflow passes all validation steps, it receives a final quality grade and is returned as a structured, executable JSON object. If the main process fails, an intelligent fallback system can still generate a viable workflow to ensure a result is always provided.'
                }
            };

            const componentsData = {
                agents: [
                    { name: 'data_ingestion_agent', description: 'Ingests data from various sources like APIs, databases, or files.' },
                    { name: 'sentiment_analysis_agent', description: 'Analyzes a given text to determine its sentiment.' },
                    { name: 'agentic_RAG', description: 'Answers complex questions by retrieving and synthesizing information from a vector database.' },
                    { name: 'financial_report_agent', description: 'Generates a financial report from transactional data.' }
                ],
                tools: [
                    { name: 'read_file', description: 'Reads the content of a file from a given path.' },
                    { name: 'send_email', description: 'Sends an email to a specified recipient.' },
                    { name: 'execute_sql', description: 'Executes a single SQL statement on a configured database.' },
                    { name: 'make_api_call', description: 'Makes a generic HTTP request to a specified URL.' }
                ]
            };

            const flowSteps = document.querySelectorAll('.flow-step');
            const detailsTitle = document.getElementById('details-title');
            const detailsText = document.getElementById('details-text');

            function updateDetails(stepId) {
                const content = lifecycleSteps[stepId];
                detailsTitle.textContent = content.title;
                detailsText.textContent = content.text;

                flowSteps.forEach(step => {
                    step.classList.remove('active');
                    if (step.id.includes(stepId)) {
                        step.classList.add('active');
                    }
                });
            }

            flowSteps.forEach(step => {
                step.addEventListener('click', () => {
                    const stepId = step.id.replace('flow-step-', '');
                    updateDetails(stepId);
                });
            });

            updateDetails('query');

            const tooltipBox = document.getElementById('tooltip-box');
            document.querySelectorAll('.json-key').forEach(key => {
                key.addEventListener('mousemove', (e) => {
                    tooltipBox.style.display = 'block';
                    tooltipBox.textContent = key.dataset.tooltip;
                    tooltipBox.style.left = e.pageX + 15 + 'px';
                    tooltipBox.style.top = e.pageY + 15 + 'px';
                });
                key.addEventListener('mouseleave', () => {
                    tooltipBox.style.display = 'none';
                });
            });

            const agentsBtn = document.getElementById('agents-btn');
            const toolsBtn = document.getElementById('tools-btn');
            const componentsContent = document.getElementById('components-content');

            function renderComponents(type) {
                const data = componentsData[type];
                let html = '<div class="space-y-4">';
                data.forEach(item => {
                    html += `
                        <div class="card p-4">
                            <h4 class="font-semibold text-stone-800">${item.name}</h4>
                            <p class="text-sm text-stone-600 mt-1">${item.description}</p>
                        </div>
                    `;
                });
                html += '</div>';
                componentsContent.innerHTML = html;
            }

            agentsBtn.addEventListener('click', () => {
                agentsBtn.classList.add('border-orange-600', 'text-orange-600');
                toolsBtn.classList.remove('border-orange-600', 'text-orange-600');
                toolsBtn.classList.add('border-transparent', 'text-stone-500');
                renderComponents('agents');
            });

            toolsBtn.addEventListener('click', () => {
                toolsBtn.classList.add('border-orange-600', 'text-orange-600');
                agentsBtn.classList.remove('border-orange-600', 'text-orange-600');
                agentsBtn.classList.add('border-transparent', 'text-stone-500');
                renderComponents('tools');
            });

            renderComponents('agents');

            const navLinks = document.querySelectorAll('.nav-link');
            const sections = document.querySelectorAll('section');
            
            window.addEventListener('scroll', () => {
                let current = '';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if (pageYOffset >= sectionTop - 80) {
                        current = section.getAttribute('id');
                    }
                });

                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href').includes(current)) {
                        link.classList.add('active');
                    }
                });
            });
        });
    </script>
</body>
</html>
