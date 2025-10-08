# QA Packet Validator - Python Version

**Author**: Adam Morien  
**Maintainer**: Adam Morien  
**Version**: 1.0  
**License**: MIT  
**Repository**: https://github.com/amorien-aem/qa_packet_validator_py

## Description

QA Packet Validator is a web-based application built with Flask that validates QA packet PDFs for required fields, numerical ranges, and consistency. It generates CSV, Excel, and dashboard visualizations to assist in quality assurance processes.

This is the Python version compatible with Render deployment environment.

## Features

- PDF field extraction
- Anomaly and critical issue detection
- Excel and CSV report generation
- Dashboard visualization with matplotlib
- Web interface for easy file upload and validation
- Progress tracking for long-running validations
- OCR support for scanned PDFs using Tesseract

## Technology Stack

- **Flask**: Web framework
- **PyMuPDF (fitz)**: PDF processing
- **pandas**: Data manipulation
- **openpyxl**: Excel file generation
- **matplotlib**: Dashboard visualization
- **pytesseract**: OCR for scanned PDFs
- **Pillow**: Image processing
- **gunicorn**: Production WSGI server

## Local Development

### Prerequisites

- Python 3.11.9
- Tesseract OCR (for OCR functionality)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/amorien-aem/qa_packet_validator_py.git
cd qa_packet_validator_py
```

2. Install Python dependencies:
```bash
pip install -r requirements.txt
```

3. Install Tesseract OCR:
   - **Ubuntu/Debian**: `sudo apt-get install tesseract-ocr`
   - **macOS**: `brew install tesseract`
   - **Windows**: Download installer from https://github.com/UB-Mannheim/tesseract/wiki

### Running Locally

Run the Flask development server:
```bash
python app/app.py
```

The application will be available at `http://localhost:3000`

## Deployment on Render

This application is configured for deployment on Render.com.

### Deployment Options

#### Option 1: Docker Deployment (Recommended)
The repository includes a `Dockerfile` and `render.yaml` configured for Docker deployment:
- Tesseract OCR is automatically installed in the container
- All dependencies are managed within the Docker image

#### Option 2: Native Python Deployment
Use the `Procfile` for native Python deployment:
- The `render-build.sh` script installs system dependencies (Tesseract)
- Python dependencies are installed from `requirements.txt`

### Environment Variables

The application uses the following environment variable:
- `PORT`: The port number for the web server (automatically set by Render)

## Usage

1. Navigate to the application URL
2. Click "Choose File" and select a PDF file to validate
3. Click "Upload and Validate"
4. Monitor the upload and validation progress bars
5. Once complete, click the "Download CSV" link to get the validation results

## File Structure

```
qa_packet_validator_py/
├── app/
│   ├── app.py              # Main Flask application
│   ├── templates/
│   │   └── index.html      # HTML template (inline in app.py)
│   ├── uploads/            # Uploaded PDF files (gitignored)
│   └── exports/            # Generated reports (gitignored)
├── requirements.txt        # Python dependencies
├── runtime.txt            # Python version specification
├── Dockerfile             # Docker configuration
├── render.yaml            # Render deployment configuration
├── Procfile               # Process file for native deployment
├── render-build.sh        # Build script for Render
└── README.md              # This file
```

## Validation Features

The validator checks for:

### Required Fields
- Customer information (Name, P.O. Number, Part Number, Revision)
- OEM information (Part Number, Lot Number, Date Code, Cage Code)
- AEM information (Part Number, Lot Number, Date Code, Cage Code)
- Quality documentation (FAI Form 3, Test Reports, DPA, etc.)
- Part details (Number, Lot, Date, Resistance, Dimension, Test Result)

### Numerical Validations
- **Resistance**: Must be between 95-105
- **Dimension**: Must be between 0.9-1.1

### Consistency Checks
- Part Number consistency across pages
- Lot Number consistency across pages
- Date consistency across pages

## Output Files

For each validated PDF, the application generates:
1. **CSV Report**: `[filename]_validation_summary.csv` - List of all anomalies
2. **Excel Report**: `[filename]_validation_summary.xlsx` - Formatted table with anomalies
3. **Dashboard**: `[filename]_dashboard.png` - Bar chart showing field presence across pages

## License

MIT License - See LICENSE file for details
