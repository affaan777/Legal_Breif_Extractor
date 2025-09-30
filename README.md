# Legal Brief Key Items Extractor

A dynamic NLP-powered tool for automatically extracting and analyzing key legal arguments from court briefs with precise page references and importance scoring.

## Overview

This Jupyter notebook application uses natural language processing to identify the top 10 most significant legal arguments from amicus briefs and other legal documents. Unlike manual extraction methods, this tool dynamically scores and ranks arguments based on multiple legal importance indicators.

## Problem Statement

Legal proceedings require thorough document analysis. Attorneys need tools that can efficiently:
- Extract critical arguments from lengthy legal briefs
- Provide precise page references for quick access
- Score arguments by legal importance
- Present both supporting and contextual information
- Save time in case preparation

This tool addresses these needs by automating the extraction and analysis process.

## Features

### Dynamic Extraction
- **No Hardcoding**: Automatically identifies key arguments using NLP
- **Multi-Factor Scoring**: Evaluates sentences based on:
  - Legal citations (statutes, regulations, case law)
  - Modal verb strength (violate, prohibit, require)
  - Argument indicators (FDA, states, public interest)
  - Subject relevance (case-specific terms)
  - Procedural importance (injunction, relief)

### Comprehensive Analysis
- Extracts top 10 key items with importance rankings
- Automatic categorization by legal topic
- Page-level reference tracking
- Score transparency and breakdown
- Statistical summaries

### Multiple Export Formats
- Excel workbook (multi-sheet with summary and categories)
- CSV files for critical arguments
- JSON export capability
- Pandas DataFrames for further analysis

## Technology Stack

- **Python 3.12+**
- **PyPDF2**: PDF text extraction
- **Pandas**: Data organization and analysis
- **NLTK**: Natural language processing and sentence tokenization
- **OpenPyXL**: Excel file generation

## Installation

### Prerequisites
```bash
pip install PyPDF2 pandas openpyxl nltk
```

### NLTK Data
The notebook automatically downloads required NLTK resources:
- `punkt_tab`: Sentence tokenizer
- `stopwords`: English stopwords corpus

## Usage

### Step 1: Prepare Your PDF
Place your legal brief PDF in the same directory as the notebook, or provide the full path:
```python
PDF_FILE_PATH = "Amicus Brief on Behalf of Mississippi, Alabama, Alaska, Arkansas etc....pdf"
```

### Step 2: Run Cells Sequentially
Execute cells 1-10 in order:

**Cell 1**: Import libraries and download NLTK data  
**Cell 2**: Load PDF and extract text  
**Cell 3**: Define DynamicLegalExtractor class  
**Cell 4**: Initialize the extractor  
**Cell 5**: Extract top 10 key items  
**Cell 6**: View score breakdown  
**Cell 7**: Analyze category distribution  
**Cell 8**: Review page distribution  
**Cell 9**: Export results to Excel/CSV  
**Cell 10**: View final summary  

### Step 3: Review Results
The tool generates:
- Console output with ranked arguments
- `dynamic_legal_analysis.xlsx` - Complete analysis workbook
- `key_items_dynamic.csv` - Quick reference CSV

## Output Structure

### Key Items DataFrame
Each extracted item includes:
- `rank`: Position (1-10)
- `category`: Auto-assigned legal category
- `importance`: Critical/High/Medium
- `page`: PDF page number
- `total_score`: Aggregated importance score
- `text`: Full argument text
- Score breakdowns by component

### Excel Workbook Sheets
1. **Key Items**: All extracted arguments with metadata
2. **Summary**: Statistics and metrics
3. **Categories**: Distribution breakdown

## Scoring Algorithm

Arguments are scored using weighted factors:

| Factor | Weight | Description |
|--------|--------|-------------|
| Legal Citations | 2.0 | Presence of statutes, regulations, case law |
| Modal Strength | 2.0 | Strong legal verbs (violate, prohibit) |
| Argument Indicators | 1.5 | Key legal actors (FDA, states, Congress) |
| Subject Relevance | 1.0 | Case-specific terminology |
| Procedural Terms | 0.5 | Process words (injunction, motion) |

**Minimum threshold**: 3.0 total score  
**Critical threshold**: 8.0+ total score  
**High priority**: 5.0-7.9 total score

## Customization

### Adjust Scoring Weights
Modify the `score_sentence()` method in Cell 3:
```python
scores['legal_citation'] += 3  # Increase citation importance
```

### Add Domain-Specific Terms
Update keyword lists:
```python
key_subjects = ['mifepristone', 'abortion', 'your_term_here']
```

### Change Extraction Count
Extract more or fewer items:
```python
key_items_df = extractor.extract_key_items(top_n=20)
```

## Example Output

```
DYNAMIC EXTRACTION - TOP 10 KEY ITEMS
=====================================================================================

rank  category              importance  page  total_score  text
1     Legal Violation       Critical    8     12.5         The FDA's challenged...
2     Constitutional Auth   Critical    1     11.0         Dobbs v. Jackson...
3     Federal Criminal Law  Critical    10    10.5         Federal law (18 U.S.C...
...
```

## Case Study: Alliance for Hippocratic Medicine v. FDA

This tool was developed to analyze the amicus brief in this case, which involves:
- FDA approval of mifepristone
- State authority post-Dobbs decision
- Federal preemption issues
- Public interest considerations

The dynamic extraction successfully identified critical arguments regarding FDA regulatory violations, Comstock Act provisions, and state enforcement burdens.

## Limitations

- Requires PDF text extraction (scanned PDFs need OCR preprocessing)
- English language only
- Optimized for U.S. legal documents
- Scoring algorithm may need domain-specific tuning
- Cannot interpret legal merit, only importance indicators

## Future Enhancements

- [ ] Support for multiple brief comparison
- [ ] Argument relationship mapping
- [ ] Citation network analysis
- [ ] Machine learning model training on legal corpus
- [ ] Interactive visualization dashboard
- [ ] Support for additional document formats (DOCX, TXT)

## Project Structure

```
legal-brief-analyzer/
├── README.md
├── legal_brief_analyzer.ipynb
├── Amicus Brief on Behalf of Mississippi....pdf
├── dynamic_legal_analysis.xlsx (generated)
├── key_items_dynamic.csv (generated)
└── requirements.txt
```

## Requirements File

```txt
PyPDF2>=3.0.0
pandas>=2.0.0
openpyxl>=3.1.0
nltk>=3.8.0
```

## Troubleshooting

### PDF Not Found
Ensure the PDF filename matches exactly, including spaces and special characters.

### NLTK Download Issues
Manually download NLTK data:
```python
import nltk
nltk.download('punkt_tab')
nltk.download('stopwords')
```

### Empty Results
Check if PDF text extraction was successful. Some PDFs may be image-based and require OCR.

### Score Too Low
Adjust the minimum threshold in `extract_key_items()`:
```python
if total_score >= 2:  # Lower threshold
```

## License

This project is provided for educational and professional legal analysis purposes.

## Contributing

Contributions are welcome. Key areas for improvement:
- Additional legal domain patterns
- Alternative scoring algorithms
- Support for other jurisdictions
- Performance optimization for large documents

## Contact

For questions or suggestions about this legal analysis tool, please open an issue in the project repository.

## Acknowledgments

Developed to assist attorneys in case preparation by automating the extraction and analysis of key legal arguments from court briefs and legal documents.

---

**Note**: This tool is designed to assist legal professionals but does not replace human legal analysis and judgment. Always verify extracted arguments and page references against source documents.
