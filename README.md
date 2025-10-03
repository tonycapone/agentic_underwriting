# Agentic Underwriting System

This repository contains a proof-of-concept implementation of an agentic underwriting system for life insurance applications. The system uses AI agents built with the Strands framework to analyze insurance applications, detect medical impairments, and calculate risk scores.

## Quickstart

```bash
# Clone the repository
git clone https://github.com/tonycapone/agentic_underwriting.git
cd agentic_underwriting

# Install dependencies
pip install -r agent/requirements.txt

# Launch Jupyter notebook
jupyter notebook
```

### Running the Agents

1. **Detection Agent**: Open `agent/detection_agent.ipynb` and run all cells
   - Change `mock_data_path` to use different test cases: 
     - `../mock_data/diabetes_cardiovascular`
     - `../mock_data/hypertension`

2. **Scoring Agent**: Open `agent/scoring_agent.ipynb` and run all cells
   - Edit the `impairments_payload` variable to test different scenarios

## Repository Structure

```
agentic_underwriting/
├── agent/                          # AI agent implementations
│   ├── detection_agent.ipynb  # Impairment detection agent
│   ├── scoring_agent.ipynb # Risk scoring agent
│   └── requirements.txt            # Dependencies
├── mock_data/                      # Sample data for testing
│   ├── diabetes_cardiovascular/    # Sample case: Diabetes + cardiovascular
│   │   ├── mock_application.xml    # Application XML
│   │   ├── mock_intelliscript_rx.xml # Prescription history
│   │   ├── mock_lab_results.xml    # Lab test results
│   │   ├── mock_mib_response.xml   # Medical Information Bureau response
│   │   └── mock_rx_data.csv        # Prescription data in CSV format
│   └── hypertension/               # Sample case: Hypertension
└── underwriting_manual/            # Reference materials for scoring
    ├── hypertension.md             # Guidelines for hypertension
    ├── lab_values.md               # Reference ranges for lab tests
    ├── type1_diabetes.md           # Guidelines for Type 1 Diabetes
    └── type2_diabetes.md           # Guidelines for Type 2 Diabetes
```

## System Overview

This system demonstrates an AI-driven approach to life insurance underwriting using agents to:

1. **Detect impairments** from multiple data sources (applications, prescription history, lab results, MIB records)
2. **Score the risk** associated with each impairment based on underwriting guidelines
3. **Generate an overall risk assessment** to support underwriting decisions

The implementation uses the Strands agent framework to create specialized AI agents that can process structured data and follow underwriting guidelines.

## Getting Started

### Prerequisites

- Python 3.8+
- AWS account with Bedrock access (optional, for hosted knowledge base)
- Basic understanding of life insurance underwriting concepts

### Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/tonycapone/agentic_underwriting.git
   cd agentic_underwriting
   ```

2. Install dependencies:
   ```bash
   pip install -r agent/requirements.txt
   ```

### Usage

#### 1. Impairment Detection Agent

The detection agent (`detection_agent.ipynb`) identifies medical impairments from application data by:

- Parsing XML feeds from multiple sources
- Detecting potential impairments (e.g., diabetes, hypertension)
- Extracting relevant scoring factors for each impairment
- Outputting a structured JSON payload for risk scoring

To run the detection agent:

1. Open the notebook in Jupyter:
   ```bash
   jupyter notebook agent/detection_agent.ipynb
   ```

2. Configure the notebook:
   - Set the `mock_data_path` to point to one of the sample cases
   - Optionally configure a Bedrock Knowledge Base ID if using hosted knowledge base

3. Run the notebook cells to see the agent detect impairments from the selected case

#### 2. Risk Scoring Agent

The scoring agent (`scoring_agent.ipynb`) calculates risk scores for detected impairments by:

- Referencing underwriting guidelines for each impairment
- Evaluating the severity of each condition based on scoring factors
- Calculating debits and credits according to rating tables
- Producing a final risk assessment score

To run the scoring agent:

1. Open the notebook in Jupyter:
   ```bash
   jupyter notebook agent/scoring_agent.ipynb
   ```

2. Configure the notebook:
   - You can modify the `impairments_payload` variable to test different scenarios

3. Run the notebook cells to see the agent evaluate the risk score

## Knowledge Base

The `underwriting_manual` directory contains markdown files with underwriting guidelines for various impairments:

- Rating tables with debits/credits based on severity factors
- Required evidence documentation
- Postpone/decline criteria
- Treatment considerations

The system can use these files directly as a local knowledge base or reference them through an AWS Bedrock Knowledge Base.

## Test Cases

The repository includes mock data for multiple test scenarios:

1. **Diabetes + Cardiovascular**: Applicant with Type 2 Diabetes and cardiovascular risk factors
2. **Hypertension**: Applicant with a history of high blood pressure

Each case includes XML files simulating different data sources that would be available to an underwriter.

## Development

To extend this proof of concept:

1. Add new impairment guidelines to the knowledge base
2. Create additional test cases with relevant data
3. Refine the agent prompts and tools to handle more complex scenarios
4. Implement workflow automation to process cases sequentially

## Dependencies

- `boto3` - AWS SDK for Python
- `lxml` - XML processing library
- `strands-agents` - Agent framework for AI systems
- `numpy` - Numerical computing library
- `scipy` - Scientific computing library

## License

This repository is for demonstration purposes only. All rights reserved.
