Part 2: Template Creation for Data Extraction
Approach:

Developed a Python script to generate a JSON template for data extraction.
Used nested dictionaries to represent the structure of the invoice.
Included rules for extracting both header information and table data.

Challenges:

Balancing specificity of rules with flexibility to handle variations.
Representing complex table structures in JSON format.

Solution:

Implemented flexible regex-based rules for key fields.
Used a hierarchical structure in the JSON to represent different sections of the invoice.
Included fallback rules for fields that might have multiple representations.

Key Code Section:

def create_extraction_template():
    template = {
        "header": {
            "Invoice Number": {
                "rule": "Find pattern matching '(?:Invoice|Bill)\\s*(?:No|Number|#)[:.]?\\s*(\\S+)' and extract the captured group",
                "fallback": "Find first occurrence of a pattern like 'INV-\d+' or '#\d+'"
            },
            # ... other header fields ...
        },
        "line_items": {
            "table_start": {
                "rule": "Find line containing at least 3 of ['Description', 'Quantity', 'Unit Price', 'Amount', 'Total']",
                "fallback": "Find first line after header section with tabular structure"
            },
            # ... table extraction rules ...
        },
        # ... summary section ...
    }
    return json.dumps(template, indent=2)
