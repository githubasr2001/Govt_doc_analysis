# Panchayat Raj Document Processor

A Python-based Natural Language Processing (NLP) tool for extracting and analyzing information from Panchayat Raj documents using spaCy.

## Features

- Custom NER (Named Entity Recognition) model for government document processing
- Automated extraction of key information including:
  - Budget amounts
  - Dates
  - File numbers
  - Account heads
  - Department names
  - Official designations
  - Technical terms
- PDF text extraction
- Training data preparation from XML documents
- Model training and persistence
- Structured information extraction and JSON output

## Prerequisites

```bash
python >= 3.6
spacy
PyPDF2
```

## Installation

1. Clone the repository
2. Install the required packages:
```bash
pip install spacy PyPDF2
```
3. Create the necessary directories:
```bash
mkdir trained_models
```

## Project Structure

```
.
├── trained_models/          # Directory for storing trained models
├── PanchayatRajProcessor.py # Main processing class
└── extracted_info.json      # Output file for extracted information
```

## Usage

### Basic Usage

```python
from panchayat_raj_processor import PanchayatRajProcessor

# Initialize the processor
processor = PanchayatRajProcessor()

# Train the model
processor.train_model(training_data)

# Process a document
text = processor.read_pdf("document.pdf")
results = processor.extract_information(text)
```

### Custom Entity Labels

The processor recognizes the following entity types:
- BUDGET_AMOUNT
- DATE
- FILE_NUMBER
- ACCOUNT_HEAD
- DEPARTMENT
- OFFICIAL_DESIGNATION
- TECHNICAL_TERM

## Main Components

### PanchayatRajProcessor Class

The main class that handles all processing functionality:

- `__init__(model_dir="./trained_models")`: Initializes the processor
- `read_pdf(pdf_path)`: Extracts text from PDF documents
- `read_training_data(directory)`: Reads XML training data
- `prepare_training_data(xml_documents)`: Prepares data for training
- `train_model(training_data, iterations=30)`: Trains the NER model
- `extract_information(text)`: Extracts entities from text
- `save_model(model_name="panchayat_raj_model")`: Saves trained model
- `load_model(model_name="panchayat_raj_model")`: Loads trained model
- `save_results(results, output_file="extracted_info.json")`: Saves results

## Training Data Format

Training data should be provided in XML format:

```xml
<document>
    <document_content>
        <!-- Document text content -->
    </document_content>
</document>
```

## Output Format

The processor generates structured output in JSON format:

```json
{
    "budget_amounts": [...],
    "dates": [...],
    "file_numbers": [...],
    "account_heads": [...],
    "departments": [...],
    "official_designations": [...],
    "technical_terms": [...],
    "summary": "..."
}
```

## Error Handling

The processor includes comprehensive error handling and logging:
- Logs are written with timestamps and error levels
- All major operations are wrapped in try-except blocks
- Detailed error messages are provided for debugging

## Logging

The system uses Python's built-in logging module with the following configuration:
```python
logging.basicConfig(level=logging.INFO,
                   format='%(asctime)s - %(levelname)s - %(message)s')
```



