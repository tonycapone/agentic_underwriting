# Agentic Underwriting System - Proof of Concept

This repository contains a proof-of-concept implementation of an agentic underwriting system for life insurance applications. The system uses AI agents built with the Strands framework to analyze insurance applications, detect medical impairments, and calculate risk scores.

The main value is in the **two Jupyter notebooks** (`detection_agent.ipynb` and `scoring_agent.ipynb`) that demonstrate the complete workflow.

## What This Demonstrates

This proof-of-concept shows how AI agents built with the Strands framework can:

1. **Detect medical impairments** by analyzing multiple data sources (applications, prescription history, lab results, MIB records)
2. **Calculate risk scores** by consulting underwriting guidelines and applying rating tables
3. **Generate audit trails** with detailed explanations for each decision

The notebooks demonstrate a complete end-to-end workflow from raw data ingestion to final risk scoring.

## How to Use This Demo

The entire demonstration is contained in two interactive notebooks with extensive documentation:

### 1. Detection Agent (`agent/detection_agent.ipynb`)
**What it does:** Analyzes multiple data sources to identify medical impairments and extract scoring factors.

Open this notebook first to see how the agent:
- Ingests JSON data from applications, RX history, labs, and MIB
- Uses semantic search to find relevant underwriting guidelines
- Identifies impairments and compiles evidence from multiple sources
- Outputs structured JSON ready for risk scoring

**Try changing:** The `mock_data_path` variable to switch between test cases (`diabetes_cardiovascular` or `hypertension`)

### 2. Scoring Agent (`agent/scoring_agent.ipynb`)
**What it does:** Calculates risk scores by applying underwriting rules to detected impairments.

Open this notebook to see how the agent:
- Looks up rating tables for each impairment
- Applies scoring factors to determine debits and credits
- Uses a calculator tool for exact arithmetic
- Generates detailed explanations for audit trails

**Try changing:** The `impairments_payload` variable to test different clinical scenarios (e.g., higher blood pressure, additional complications)

### Quick Start

```bash
# Install dependencies
pip install -r agent/requirements.txt

# Launch Jupyter notebook
jupyter notebook

# Open agent/detection_agent.ipynb and run all cells
# Then open agent/scoring_agent.ipynb and run all cells
```

## Repository Structure

```
agentic_underwriting/
├── agent/
│   ├── detection_agent.ipynb
│   ├── scoring_agent.ipynb
│   └── requirements.txt
├── mock_data/
│   ├── diabetes_cardiovascular/
│   │   ├── mock_application.json
│   │   ├── mock_intelliscript_rx.json
│   │   ├── mock_lab_results.json
│   │   ├── mock_mib_response.json
│   │   └── mock_rx_data.json
│   └── hypertension/
│       ├── mock_application.json
│       ├── mock_intelliscript_rx.json
│       ├── mock_lab_results.json
│       └── mock_mib_response.json
└── underwriting_manual/
    ├── hypertension.md
    ├── lab_values.md
    ├── type1_diabetes.md
    └── type2_diabetes.md
```

## Why This Matters

Traditional underwriting requires trained professionals to:
- Review multiple data sources manually
- Cross-reference underwriting guidelines
- Calculate risk scores using complex rating tables
- Document their reasoning for compliance

**This takes 30-90 minutes per application.**

This proof-of-concept shows how AI agents can perform the same analysis in seconds while:
- Maintaining consistency across all decisions
- Providing detailed audit trails
- Scaling to handle thousands of applications
- Adapting to new rules by updating markdown files

The notebooks demonstrate this end-to-end.

## What's Included

### The Notebooks (Main Focus)
- **`agent/detection_agent.ipynb`** - Impairment detection from multiple data sources
- **`agent/scoring_agent.ipynb`** - Risk scoring using underwriting guidelines

### Supporting Materials
- **`mock_data/`** - Synthetic JSON test data for two clinical scenarios
- **`underwriting_manual/`** - Markdown files with rating tables and underwriting rules
- **`agent/requirements.txt`** - Python dependencies

### Prerequisites

- Python 3.8+
- AWS account with Bedrock access (for running the notebooks)
- Jupyter Notebook or JupyterLab

## Test Cases

The repository includes synthetic data for two clinical scenarios:

1. **`diabetes_cardiovascular/`** - Complex case with Type 2 Diabetes, hypertension, and cardiovascular risk factors
2. **`hypertension/`** - Simpler case with controlled blood pressure and good lab results

Each case includes JSON files simulating real data sources:
- Application data (demographics, questionnaire answers)
- Prescription history (medications, dosages, fill dates)
- Lab results (blood work, A1C, lipid panels)
- MIB records (prior insurance applications)

**Note:** All data has been anonymized with masked company names and addresses while preserving clinical values.

## Extending This Demo

The notebooks are designed to be modified and extended:

1. **Add new impairments:** Create markdown files in `underwriting_manual/` with rating tables
2. **Test new scenarios:** Modify the mock data JSON files or create new test cases
3. **Refine agent behavior:** Adjust the system prompts in the notebooks
4. **Add new tools:** Give agents additional capabilities (e.g., database queries, API calls)

The beauty of this architecture is that updating underwriting rules only requires editing markdown files - no code changes needed.

## Technical Details

### Dependencies
- `boto3` - AWS SDK for Bedrock API access
- `strands-agents` - Agent framework for orchestrating LLM tool calls
- `numpy` - Vector similarity calculations for local knowledge base
- `lxml` - JSON parsing (legacy from XML version)

### Architecture Highlights

The notebooks demonstrate key agentic patterns:
- **Tool use:** Agents call functions to search knowledge bases and perform calculations
- **Multi-step reasoning:** Agents break complex tasks into sequential steps
- **Semantic search:** Vector embeddings find relevant guidelines
- **Structured output:** Agents produce JSON for downstream processing
- **Audit trails:** Every decision includes detailed explanations

## Note

This is demonstration code, not a production application.
