GenomicsGPT
AI-Powered Multi-Agent System for Genomic Variant Interpretation
A production-ready RAG system that leverages LangChain, Azure OpenAI, and real ClinVar data to provide clinical variant interpretation with ACMG guideline analysis.


🎯 Project Overview
GenomicsGPT is a multi-agent AI system designed to assist clinicians and researchers in interpreting genomic variants. The system combines:

Multi-Agent Architecture using LangChain for intelligent task decomposition
RAG (Retrieval Augmented Generation) with Azure Cosmos DB and Azure AI Search
Real ClinVar Data - 100+ pathogenic variants from well-studied genes
ACMG/AMP Guidelines implementation for systematic variant classification
Interactive Web Interface built with Streamlit

Key Features
✅ Semantic Search - Vector embeddings for finding similar variants
✅ Structured Queries - Cosmos DB for gene-specific lookups
✅ ACMG Analysis - Automated application of clinical guidelines
✅ Evidence Synthesis - Multi-source information aggregation
✅ Clinical Recommendations - Actionable guidance for patient care

🏗️ Architecture
┌─────────────────────────────────────────────────────────────┐
│                     User Interface (Streamlit)               │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│              Coordinator Agent (LangChain)                   │
│  ┌──────────────┬──────────────┬────────────┬─────────────┐ │
│  │ ClinVar      │ Gene         │ Variant    │ ACMG        │ │
│  │ Search Tool  │ Search Tool  │ Details    │ Analysis    │ │
│  └──────────────┴──────────────┴────────────┴─────────────┘ │
└─────────────────────────┬───────────────────────────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│ Azure Cosmos │  │ Azure AI     │  │ Azure/OpenAI │
│ DB (NoSQL)   │  │ Search       │  │ GPT-4        │
│ - Variants   │  │ - Embeddings │  │ - Analysis   │
│ - Metadata   │  │ - Vector     │  │ - Reasoning  │
└──────────────┘  └──────────────┘  └──────────────┘

🚀 Quick Start
Prerequisites

Python 3.9+
Azure account (free tier sufficient)
OpenAI API key (or Azure OpenAI)
Git

Installation
bash# Clone the repository
git clone https://github.com/manveenmeng/genomics-gpt.git
cd genomics-gpt

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt


Setup Data
bash# Option 1: Use sample data (quick)
python scripts/create_sample_data.py

# Option 2: Download full ClinVar data
python scripts/download_clinvar.py

# Upload to Azure
python scripts/upload_to_azure.py
Run the Application
bash# Web Interface
streamlit run app/streamlit_app.py

# CLI Interface
python src/agents/genomics_agents.py

💻 Usage Examples
Web Interface

Open http://localhost:8501
Click example buttons or enter custom queries
View real-time agent reasoning
Explore analysis details and sources

CLI Interface
pythonfrom src.agents.genomics_agents import GenomicsAgentSystem

system = GenomicsAgentSystem()
result = system.interpret_variant("BRCA1 c.68_69delAG")
print(result["interpretation"])
Example Queries

"Find pathogenic variants in BRCA1"
"What is the clinical significance of TP53 mutations?"
"Analyze CFTR F508del variant"
"Interpret BRCA2 variants for breast cancer risk"

🛠️ Technology Stack
AI/ML

LangChain - Multi-agent orchestration
OpenAI GPT-4o-mini - Natural language reasoning
text-embedding-3-large - Semantic search embeddings

Azure Services

Cosmos DB - NoSQL document storage
AI Search - Hybrid vector + keyword search
Azure OpenAI - (Optional) Azure-hosted LLM

Frontend

Streamlit - Interactive web interface
Plotly - Data visualizations (future)

Data

ClinVar - NCBI variant database
ACMG Guidelines - Clinical interpretation standards



Key Requirements Demonstrated:

✅ Multi-agent workflows with LangChain
✅ RAG system with Azure infrastructure
✅ MLOps-ready architecture
✅ Genomics domain knowledge
✅ Production-quality code


# Create .env file
cp .env.example .env
# Edit .env with your API keys




## 🔌 MCP Server

GenomicsGPT includes a Model Context Protocol (MCP) server for tool integration:

### Features
- **Tool Discovery**: List all available genomics tools
- **Standardized Invocation**: Call tools with consistent interface
- **Health Monitoring**: Track system status
- **Interactive Docs**: Swagger UI at `/docs`

### Running the MCP Server
```bash
python src/mcp/mcp_server.py
```

Access the API at: http://localhost:8000
Interactive docs: http://localhost:8000/docs

### Example Usage
```bash
curl -X POST "http://localhost:8000/mcp/invoke" \
  -H "Content-Type: application/json" \
  -d '{
    "tool_name": "variant-lookup",
    "parameters": {"variant_id": "BRCA1"}
  }'
```

### Available Tools
- `variant-lookup`: Query variant databases
- `gene-variants`: Get all variants in a gene
