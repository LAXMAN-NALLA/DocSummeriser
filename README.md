# 📄 AI-Powered Document Analyzer

**Enterprise-Grade Document Intelligence Platform**

A sophisticated document analysis solution that leverages advanced AI to automatically classify, extract, and analyze various document types. Built for business professionals who need quick, accurate, and actionable insights from their document collections.

## 🚀 Key Capabilities

### **Multi-Modal Analysis**
- **Single Document Analysis**: Deep analysis of individual documents with detailed insights
- **Batch Processing**: Analyze multiple documents individually for quality control
- **Consolidated Analysis**: Cross-document analysis providing comprehensive insights and recommendations

### **AI-Powered Intelligence**
- **Smart Classification**: Automatically identifies document types (Invoices, Contracts, Financial Statements, etc.)
- **Intelligent Extraction**: Extracts key information, dates, amounts, and entities
- **Actionable Recommendations**: Provides specific, detailed recommendations with exact next steps
- **Multi-Language Support**: Processes documents in various languages

### **Enterprise Features**
- **Hybrid Text Extraction**: Combines specialized libraries with AWS Textract OCR
- **Scalable Architecture**: FastAPI backend with async processing
- **Professional UI**: Clean, intuitive Streamlit interface
- **Comprehensive Error Handling**: Robust error management and logging

## 📋 Supported Document Types

| Format | Type | Processing Method | Use Cases |
|--------|------|------------------|-----------|
| **PDF** | Digital & Scanned | pdfplumber + AWS Textract | Contracts, Reports, Invoices |
| **DOCX** | Word Documents | python-docx | Business Documents, Proposals |
| **XLSX/CSV** | Spreadsheets | pandas | Financial Data, Reports |
| **PNG/JPG/JPEG** | Images | AWS Textract OCR | Scanned Documents, Photos |

## 🛠️ System Requirements

### **Minimum Requirements**
- **Python**: 3.8 or higher
- **Memory**: 4GB RAM (8GB recommended for large documents)
- **Storage**: 1GB free space
- **Internet**: Required for OpenAI API calls

### **API Requirements**
- **OpenAI API Key**: Required for AI analysis
- **AWS Credentials**: Optional, for OCR functionality on scanned documents

## ⚡ Quick Start

### **1. Environment Setup**
   ```bash
# Clone the repository
   git clone <repository-url>
   cd oDoc_analyser-main

# Create virtual environment
   python -m venv venv
   
# Activate virtual environment
# Windows:
   venv\Scripts\activate
# macOS/Linux:
   source venv/bin/activate

# Install dependencies
   pip install -r requirements.txt
   ```

### **2. Configuration**
Create a `.env` file in the project root:
   ```bash
# Required - OpenAI Configuration
   OPENAI_API_KEY=your_openai_api_key_here
   OPENAI_MODEL=gpt-4o
   
# Optional - AWS Configuration (for OCR)
   AWS_ACCESS_KEY_ID=your_aws_access_key_here
   AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key_here
   AWS_REGION=us-east-1
   ```

### **3. Launch Application**

#### **Local Development**
```bash
# Terminal 1: Start API Backend
uvicorn main:app --reload

# Terminal 2: Start Web Interface
streamlit run app.py
```

**Access the application at:** `http://localhost:8501`

#### **Production Deployment**
The application is deployed on Render and accessible at:
- **API Base URL**: `https://inbox-backend-cf4n.onrender.com`
- **Health Check**: `https://inbox-backend-cf4n.onrender.com/health`

**Production Features:**
- ✅ **Always Available**: 24/7 API access
- ✅ **Auto-Scaling**: Handles multiple concurrent requests
- ✅ **SSL Security**: HTTPS encryption for all requests
- ✅ **Global CDN**: Fast response times worldwide
- ✅ **Automatic Fallback**: Streamlit UI automatically uses production API when available

### **Quick Test (Production API)**
Test the production API immediately:
```bash
# Test health endpoint
curl https://inbox-backend-cf4n.onrender.com/health

# Test with Postman (see API Testing Guide below)
```

## 🎯 How to Use

### **Single Document Analysis**
Perfect for individual document review and classification.

1. **Upload**: Select a single document (PDF, DOCX, XLSX, CSV, or image)
2. **Analyze**: Click "Analyze Files" - the system automatically detects it's a single file
3. **Review**: Get detailed analysis including:
   - Document type classification
   - Language detection
   - Comprehensive summary with specific details
   - Actionable recommendations with exact next steps
   - Key extracted information

### **Multiple Documents - Consolidated Analysis**
Ideal for analyzing related documents together (contracts, invoices, reports from the same project).

1. **Upload**: Select multiple related documents (up to 10 files)
2. **Analyze**: Click "Analyze Files" - the system automatically performs consolidated analysis
3. **Review**: Get comprehensive insights including:
   - **Comprehensive Summary**: Detailed overview of all documents combined
   - **Key Findings**: Specific discoveries across the document collection
   - **Detailed Recommendations**: Actionable next steps with exact details
   - **Priority Actions**: Most urgent items requiring immediate attention

### **Analysis Modes Comparison**

| Mode | Best For | Output | Processing Time |
|------|----------|--------|----------------|
| **Single File** | Individual document review | Detailed analysis per document | 10-30 seconds |
| **Consolidated** | Related document collections | Cross-document insights | 30-90 seconds |

## 🧪 API Testing Guide

### **Testing with Postman**

#### **Step 1: Health Check**
Test if the API is running:
```
GET https://inbox-backend-cf4n.onrender.com/health
```
**Expected Response:**
```json
{
  "status": "ok"
}
```

#### **Step 2: Single Document Analysis**
Analyze one document:
```
POST https://inbox-backend-cf4n.onrender.com/analyze
```
**Body Configuration:**
- **Type**: `form-data`
- **Key**: `file` (File type)
- **Value**: Select your document file

#### **Step 3: Multiple Documents Analysis**
Analyze multiple documents together:
```
POST https://inbox-backend-cf4n.onrender.com/analyze-consolidated
```
**Body Configuration:**
- **Type**: `form-data`
- **Key**: `files` (File type) - **⚠️ Important: Use "files" (plural)**
- **Value**: Select multiple document files

#### **Postman Collection Setup**
1. **Create New Collection**: "Document Analyzer API"
2. **Add Environment Variable**: 
   - Variable: `base_url`
   - Value: `https://inbox-backend-cf4n.onrender.com`
3. **Create Requests**:
   - Health Check: `{{base_url}}/health`
   - Single Analysis: `{{base_url}}/analyze`
   - Consolidated Analysis: `{{base_url}}/analyze-consolidated`

### **Expected Response Format**

#### **Single Document Response**
```json
{
  "filename": "document.pdf",
  "document_type": "Invoice",
  "analysis": {
    "language": "English",
    "detailed_summary": "Invoice #12345 for €1,250.00...",
    "actionable_recommendations": [
      "Pay invoice #12345 for €1,250.00 by December 15th",
      "Contact vendor regarding payment terms"
    ],
    "key_details": {
      "Invoice_Number": "12345",
      "Amount": "€1,250.00",
      "Due_Date": "2024-12-15"
    }
  },
  "status": "success"
}
```

#### **Consolidated Analysis Response**
```json
{
  "total_files": 3,
  "successful_files": 3,
  "failed_files": 0,
  "file_info": [
    {
      "filename": "invoice1.pdf",
      "document_type": "Invoice",
      "text_length": 1250
    }
  ],
  "consolidated_analysis": {
    "comprehensive_summary": "Analysis of 3 documents...",
    "key_findings": [
      "Total outstanding amount: €3,750.00",
      "All invoices due within 30 days"
    ],
    "detailed_recommendations": [
      "Process payment for invoice #12345 by December 15th",
      "Review contract terms for renewal"
    ],
    "priority_actions": [
      "Urgent: Pay overdue invoice #12345"
    ]
  },
  "status": "success"
}
```

## 🔧 Technical Architecture

### **API Endpoints**

#### **Production Endpoints (Render)**
| Endpoint | Method | Purpose | URL |
|----------|--------|---------|-----|
| `/health` | GET | System health check | `https://inbox-backend-cf4n.onrender.com/health` |
| `/analyze` | POST | Single document analysis | `https://inbox-backend-cf4n.onrender.com/analyze` |
| `/analyze-consolidated` | POST | Multi-document analysis | `https://inbox-backend-cf4n.onrender.com/analyze-consolidated` |

#### **API Testing with Postman**

**1. Health Check**
- **Method**: GET
- **URL**: `https://inbox-backend-cf4n.onrender.com/health`
- **Expected Response**: `{"status": "ok"}`

**2. Single Document Analysis**
- **Method**: POST
- **URL**: `https://inbox-backend-cf4n.onrender.com/analyze`
- **Body Type**: `form-data`
- **Key**: `file` (File type)
- **Value**: Select your document file

**3. Multiple Documents Analysis (Consolidated)**
- **Method**: POST
- **URL**: `https://inbox-backend-cf4n.onrender.com/analyze-consolidated`
- **Body Type**: `form-data`
- **Key**: `files` (File type) - **Important: Use "files" (plural)**
- **Value**: Select multiple document files

#### **Postman Setup Steps**
1. Open Postman
2. Create a new request
3. Set method to POST
4. Enter the URL: `https://inbox-backend-cf4n.onrender.com/analyze-consolidated`
5. Go to Body tab
6. Select `form-data`
7. Add key: `files` (make sure it's "files" not "file")
8. Change type to "File" for the key
9. Click "Select Files" and choose your documents
10. Send the request

### **System Architecture**
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Streamlit UI  │───▶│   FastAPI API   │───▶│  OpenAI GPT-4   │
│   (Frontend)    │    │   (Backend)     │    │   (AI Engine)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │
                                ▼
                       ┌─────────────────┐
                       │  Text Extraction│
                       │  (Hybrid OCR)   │
                       └─────────────────┘
```

### **Configuration Options**

| Variable | Description | Required | Default | Impact |
|----------|-------------|----------|---------|--------|
| `OPENAI_API_KEY` | OpenAI API key for AI analysis | ✅ Yes | - | Core functionality |
| `OPENAI_MODEL` | AI model version | No | `gpt-4o` | Analysis quality |
| `AWS_ACCESS_KEY_ID` | AWS access key | No | - | OCR for scanned docs |
| `AWS_SECRET_ACCESS_KEY` | AWS secret key | No | - | OCR for scanned docs |
| `AWS_REGION` | AWS region | No | - | OCR processing location |

### **OCR Capabilities**
- **With AWS**: Full OCR support for scanned documents and images
- **Without AWS**: Digital document processing only (PDF, DOCX, XLSX, CSV)

## 💼 Business Use Cases

### **Financial Services**
- **Invoice Processing**: Automatically extract amounts, due dates, and vendor information
- **Financial Statement Analysis**: Analyze balance sheets and P&L statements
- **Compliance Review**: Identify regulatory requirements and compliance gaps

### **Legal & Contract Management**
- **Contract Analysis**: Extract key terms, dates, and obligations
- **Legal Document Review**: Identify critical clauses and potential issues
- **Evidence Processing**: Analyze multiple legal documents for case preparation

### **Business Operations**
- **Project Documentation**: Review multiple project files for comprehensive insights
- **Vendor Management**: Analyze contracts and invoices from multiple suppliers
- **Report Consolidation**: Combine insights from multiple business reports

### **Research & Development**
- **Literature Review**: Analyze multiple research papers for comprehensive insights
- **Technical Documentation**: Process multiple technical documents for project understanding
- **Competitive Analysis**: Analyze competitor documents and reports

## 🛡️ Security & Reliability

### **Data Security**
- **No Data Storage**: Documents are processed in memory and immediately deleted
- **Temporary Files**: All temporary files are automatically cleaned up
- **API Security**: Secure API endpoints with proper error handling

### **Error Handling**
- **Comprehensive Validation**: File type and size validation
- **Graceful Degradation**: System continues working even if some services fail
- **Detailed Logging**: Complete audit trail for troubleshooting
- **Retry Logic**: Automatic retry for transient failures

### **Performance**
- **Async Processing**: Non-blocking operations for better performance
- **Parallel Processing**: Multiple documents processed simultaneously
- **Memory Management**: Efficient memory usage for large documents

## 🔧 Development & Maintenance

### **Code Structure**
```
oDoc_analyser-main/
├── main.py              # FastAPI backend with API endpoints
├── app.py               # Streamlit frontend interface
├── openai_service.py    # OpenAI integration and AI processing
├── textract_service.py  # Text extraction and OCR services
├── prompts.py           # AI prompts and templates
├── requirements.txt     # Python dependencies
├── Dockerfile           # Container configuration
└── README.md           # This documentation
```

### **Development Setup**
```bash
# Install development dependencies
pip install pytest pytest-asyncio

# Run tests
pytest

# Run with development mode
uvicorn main:app --reload --log-level debug
```

## 🚨 Troubleshooting

### **Common Issues & Solutions**

| Issue | Symptoms | Solution |
|-------|----------|----------|
| **API Not Running** | "API is not running" error | Start FastAPI: `uvicorn main:app --reload` |
| **OpenAI API Errors** | Analysis fails with API error | Check API key and billing status |
| **AWS OCR Issues** | Scanned documents fail | Verify AWS credentials and region |
| **File Upload Fails** | Upload rejected | Check file type and size limits |
| **Slow Processing** | Long wait times | Large documents take longer; consider file size |

### **Monitoring & Logs**
- **API Health**: Check `http://localhost:8000/health`
- **Logs**: Monitor terminal output for detailed processing information
- **Performance**: Processing time varies by document size and complexity

## 📞 Support & Contact

### **Getting Help**
1. **Check Documentation**: Review this README and troubleshooting section
2. **Check Logs**: Review terminal output for error details
3. **API Status**: Verify all services are running correctly

### **System Requirements Verification**
- ✅ Python 3.8+ installed
- ✅ OpenAI API key configured
- ✅ Virtual environment activated
- ✅ Dependencies installed
- ✅ Both services running (API + UI)

---

## 📊 Summary

**The AI-Powered Document Analyzer** is a comprehensive solution for businesses that need to process and analyze documents efficiently. With its dual-mode analysis (single and consolidated), enterprise-grade security, and powerful AI capabilities, it provides actionable insights that help organizations make informed decisions quickly.

**Key Benefits:**
- ⚡ **Fast Processing**: 10-90 seconds per analysis
- 🎯 **Accurate Results**: AI-powered classification and extraction
- 🔒 **Secure**: No data storage, temporary processing only
- 📈 **Scalable**: Handles multiple documents simultaneously
- 💼 **Business-Ready**: Professional interface and comprehensive reporting
