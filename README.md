# Code Analyst Agent 🤖

An advanced AI-powered Code Analyst that leverages the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) and Google's Gemini 3 Pro model to connect directly to your GitHub repositories. It scans, analyzes, and answers complex questions about your codebase, acting as an expert developer and data analyst paired with you.

## 🌟 Features

*   **GitHub Integration via MCP**: Seamlessly connects to GitHub using the official [GitHub MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/git) to search code, read files, and explore repositories.
*   **Intelligent Code Scanning**: Implements a "Search-Verify-Read" operational loop to locate relevant files and extract precise logic.
*   **SQL & Logic Analysis**: Specialized instructions for analyzing SQL files, extracting calculation logic, aggregations, and data lineage (though capable of analyzing any code).
*   **Powered by Gemini 3 Pro**: Utilizes `gemini-3-pro-preview` for state-of-the-art reasoning and code understanding.
*   **Privacy-First**: Runs locally and connects securely to your cloud and git providers.

## 📋 Prerequisites

Before you begin, ensure you have the following installed and configured:

1.  **Python 3.10+**: [Download Python](https://www.python.org/downloads/)
2.  **Node.js & npm** (Required for the GitHub MCP server): [Download Node.js](https://nodejs.org/)
3.  **Google Cloud Project**:
    *   A Google Cloud project with Vertex AI API enabled.
    *   [Google Cloud CLI](https://cloud.google.com/sdk/docs/install) installed and authenticated (`gcloud auth login`).
4.  **GitHub Account**: Access to the repositories you want to analyze.

## 🛠️ Installation

1.  **Clone the Repository**
    ```bash
    git clone <your-repo-url>
    cd codeanalyst
    ```

2.  **Install Python Dependencies**
    It is recommended to use a virtual environment.
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    pip install -r requirements.txt
    ```
    *(Note: If `requirements.txt` is missing, ensure you have `python-dotenv`, `google-cloud-aiplatform`, and the `google-adk` package installed).*

## ⚙️ Configuration

1.  **Environment Variables**
    Copy the example environment file to create your own configuration:
    ```bash
    cp .env.example .env
    ```

2.  **Configure `.env`**
    Open the `.env` file and fill in the required details:

    *   `GITHUB_PERSONAL_ACCESS_TOKEN`: A GitHub PAT is required for the agent to access your repositories.
        *   👉 **[Generate a Token Here](https://github.com/settings/tokens?type=beta)**
        *   **Scopes Required**: Select `repo` (Full control of private repositories) or specifically `read:packages` / `read:org` depending on your needs.
    *   `GOOGLE_CLOUD_PROJECT`: Your Google Cloud Project ID.
    *   `GOOGLE_CLOUD_REGION`: The region for Vertex AI (e.g., `us-central1`).

    ```ini
    # Example .env configuration
    GITHUB_PERSONAL_ACCESS_TOKEN="ghp_xxxxxxxxxxxxxxxxxxxx"
    GOOGLE_CLOUD_PROJECT="your-project-id"
    GOOGLE_CLOUD_REGION="us-central1"
    ```

## 🚀 Usage

The agent is defined in `agent.py`. It initializes a `root_agent` with the GitHub MCP toolset.

To run the agent, you can execute the script:

```bash
python agent.py
```

### 💡 How it Works

The agent follows a strict **"Search-Verify-Read"** protocol:
1.  **Identify Context**: When you ask about a project or file, it searches the repo structure.
2.  **Deep Retrieval**: It reads the specific files identified.
3.  **Logic Extraction**: It parses the code (e.g., SQL logic) to answer your specific question.

### Example Queries
*   *"Find the calculation logic for `daily_active_users` in the `marketing_analytics` project."*
*   *"Trace the lineage of the `revenue_total` field in `sales_data.sql`."*
*   *"Compare the implementation of `calculate_tax` between `v1_finance` and `v2_finance` folders."*

## 📚 Resources

*   **[Model Context Protocol (MCP)](https://modelcontextprotocol.io/)**: Learn about the open standard for connecting AI models to data.
*   **[GitHub MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/git)**: Documentation for the specific tool used to connect to GitHub.
*   **[Gemini Models](https://deepmind.google/technologies/gemini/)**: Information about the Gemini model family.
