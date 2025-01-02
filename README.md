# BNS Legal Analyzer: AI-Powered Bharatiya Nyaya Sanhita Analysis System

## Project Overview
The BNS Legal Analyzer is an advanced legal analysis system that leverages Google's Vertex AI with the Gemini 1.5 Pro model to analyze criminal cases under the Bharatiya Nyaya Sanhita (BNS) 2023. This system serves as a digital legal assistant, providing automated analysis and guidance based on the new Indian criminal code.

## Technical Stack
- **AI Model**: Gemini 1.5 Pro (gemini-1.5-pro-002)
- **Cloud Platform**: Google Cloud (Vertex AI)
- **Python Libraries**:
  - vertexai
  - gradio (for web interface)
  - base64 (for document encoding)

## Key Components

### 1. Document Processing
The system processes the BNS 2023 document (PDF) using base64 encoding:
```python
document1 = Part.from_data(
    mime_type="application/pdf",
    data=base64.b64decode(convert("/kaggle/input/indiacode/a2023-45.pdf"))
)
```

### 2. Model Configuration
The AI model is configured with specific parameters for optimal BNS analysis:

#### Generation Config
```python
generation_config = {
    "max_output_tokens": 8192,
    "temperature": 0,
    "top_p": 0.95,
}
```

#### 3. Safety Settings
All safety categories are configured to OFF to ensure unrestricted legal analysis:
- Hate Speech
- Dangerous Content
- Sexually Explicit Content
- Harassment

### 4. Error Handling
The system implements robust error handling using exponential backoff with jitter:
- Maximum retries: 5
- Base delay: 1 second
- Maximum backoff: 32 seconds
- Random jitter enabled

### 5. Legal Analysis Function
The main analysis function includes:
- BNS document processing
- Model initialization
- Response generation with BNS references
- Error handling with retries

### 6. Web Interface
A Gradio-based web interface is implemented with:
- Text input for case description
- Text output for BNS-based legal analysis
- Title and description referencing BNS 2023
- Public sharing capability

## System Instructions
The AI model is configured with specific instructions to:
1. Reference relevant BNS sections from the 2023 code
2. Ensure use of updated BNS 2023 provisions
3. Provide clear explanations of BNS terms and procedures
4. Assist legal professionals in BNS interpretation

## Usage
1. Start the BNS Legal Analyzer using the Gradio interface
2. Enter case description in the text input
3. Receive detailed legal analysis based on BNS 2023
4. Access via local URL (http://127.0.0.1:7861) or public URL

## Error Handling
The system includes:
- Exponential backoff retry mechanism
- Jitter for distributed load
- Exception handling and error reporting
- User-friendly error messages
