# 🌐 Spot the Fake: AI-Powered Fraud Detection System

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28+-red.svg)](https://streamlit.io)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 🎯 Problem Statement

Digital fraud is evolving rapidly with sophisticated fake websites, phishing domains, and malicious apps that closely mimic legitimate brands. Traditional detection methods are reactive and rely on user reports, leaving a critical gap in proactive protection.

## 💡 Our Solution

A **hybrid AI system** that combines three powerful detection methods:

1. **🤖 ML-Based Phishing Detection** - Advanced feature engineering + LGBM
2. **🧠 LLM Content Analysis** - Contextual understanding via Mistral
3. **👁️ Computer Vision Similarity** - Brand impersonation detection

## 🏗️ System Architecture

```
Input (URL/Image) → Processing → [ML + LLM + CV] → Ensemble → Final Verdict
```

## 🔄 Processing Flow

Each analysis completes in under 30 seconds with parallel execution:

```mermaid
graph TD
    A[User Input] --> B{Input Type?}
    B -->|URL| C[URL Processor]
    B -->|Local Image| D[File Processor]
    
    C --> E[DNS/HTTP Validation]
    C --> F[Screenshot Capture]
    D --> G[Brand Name Extraction]
    
    E --> H[Feature Extraction]
    F --> I[Image Normalization]
    G --> I
    
    H --> J[Module 1: ML Detection]
    I --> K[Module 2: CV Similarity]
    F --> L[Module 3: LLM Analysis]
    
    J --> M[Ensemble Fusion]
    K --> M
    L --> M
    
    M --> N[Final Verdict + Explainability]
    N --> O[Streamlit Dashboard]
    
    style A fill:#e1f5fe
    style N fill:#c8e6c9
    style O fill:#fff3e0

### Multi-Modal Analysis Pipeline:
- **Structural Analysis**: 30+ URL features, DNS patterns, domain characteristics
- **Content Analysis**: Web scraping + NLP via local LLM
- **Visual Analysis**: Screenshot comparison with brand references

## 🚀 Key Features

### ✨ Core Capabilities
- **Real-time Website Scanning** - Instant fraud detection
- **Brand Impersonation Detection** - Visual similarity analysis
- **Explainable AI** - SHAP plots + natural language reasoning
- **Multi-modal Fusion** - Weighted ensemble for robust decisions

### 🔧 Technical Highlights
- **Automated Screenshots** - Selenium-based capture with retry logic
- **Fuzzy Brand Matching** - RapidFuzz for domain-brand association
- **Advanced OCR** - Tesseract with preprocessing for text extraction
- **Robust Error Handling** - Graceful degradation when modules fail

## 📁 Project Structure

```
spot-the-fake/
├── app1.py                 # Website similarity analysis
├── app2.py                 # ML + LLM phishing detection  
├── everything.py           # Combined Streamlit interface
├── phishing_lgbm.pkl       # Pre-trained ML model package
├── Brands/                 # Reference brand screenshots
│   ├── paypal_ref.png
│   ├── amazon_ref.png
│   └── ...
├── User/                   # User screenshot storage
├── requirements.txt        # Python dependencies
└── README.md              # This file
```

## 🛠️ Installation & Setup

### Prerequisites
- Python 3.8+
- Chrome browser (for Selenium)
- Tesseract OCR

### Quick Start
```bash
# Clone repository
git clone https://github.com/yourusername/spot-the-fake.git
cd spot-the-fake

# Install dependencies
pip install -r requirements.txt

# Install Ollama (for LLM analysis)
# Visit: https://ollama.ai/download
ollama pull mistral

# Install Tesseract OCR
# Windows: Download from GitHub releases
# macOS: brew install tesseract
# Linux: sudo apt install tesseract-ocr

# Run the application
streamlit run everything.py
```

### Dependencies
```txt
streamlit
selenium
scikit-learn
lightgbm
shap
opencv-python
Pillow
imagehash
pytesseract
beautifulsoup4
rapidfuzz
requests
ollama
matplotlib
numpy
pandas
```

## 🎮 Usage

### Web Interface
1. Launch the Streamlit app: `streamlit run everything.py`
2. Enter a suspicious URL in the input field
3. Get instant analysis with:
   - ML confidence scores
   - LLM contextual analysis
   - Visual similarity results
   - Combined final verdict

### API Usage (Command Line)
```python
from app2 import classify_content
from app1 import check_website

# Analyze URL for phishing
result = classify_content("https://suspicious-site.com")
print(f"Verdict: {result['final_verdict']}")

# Check visual similarity
similarity = check_website("https://fake-paypal.com")
print(f"Similarity Score: {similarity['score']}")
```

## 🔬 Technical Deep Dive

### Module 1: ML Phishing Detection (`app2.py`)
- **Features**: URL length, special characters, suspicious keywords, TLD patterns
- **Model**: LightGBM ensemble with probability calibration
- **Explainability**: SHAP TreeExplainer for feature importance
- **Performance**: Sub-second inference with detailed reasoning

### Module 2: Website Similarity Analysis (`app1.py`)
- **Image Hashing**: pHash + dHash for structural similarity
- **Color Analysis**: 3D histogram correlation
- **Text Extraction**: OCR with preprocessing + TF-IDF similarity
- **Fuzzy Matching**: RapidFuzz for brand name variations

### Module 3: Ensemble Integration (`everything.py`)
- **Weighted Fusion**: Configurable weights for each module
- **Adaptive Thresholding**: Context-aware decision boundaries
- **Real-time Interface**: Streamlit dashboard with visualizations

## 📊 Performance Metrics

### Detection Capabilities:
- **Phishing URLs**: High accuracy with SHAP explainability
- **Brand Impersonation**: Visual similarity detection
- **Content Analysis**: Natural language fraud indicators
- **Real-time Processing**: < 30 seconds total analysis time

### Robustness Features:
- DNS/HTTP validation before analysis
- Screenshot retry mechanisms
- Graceful degradation for missing modules
- Comprehensive error handling

## 🎨 User Experience

### Dashboard Features:
- **Input Validation**: Real-time URL checking
- **Progress Indicators**: Visual feedback during analysis
- **Detailed Results**: Component-wise breakdowns
- **Explainable AI**: Why decisions were made

### Visualization Components:
- SHAP feature importance plots
- Similarity score breakdowns
- Contribution weight charts
- Risk level indicators

## 🌟 Innovation Highlights

### Novel Contributions:
1. **First Multi-Modal Fusion** for fraud detection
2. **Brand Impersonation Detection** via computer vision
3. **Local LLM Integration** for privacy-preserving analysis
4. **Explainable Ensemble** with transparent decision making

### Technical Achievements:
- Automated brand-domain fuzzy matching
- Multi-hash image similarity algorithm
- Robust web automation with error recovery
- Real-time analysis pipeline

## 🚀 Future Roadmap

### Immediate (Post-Hackathon):
- [ ] Browser extension development
- [ ] Mobile app for iOS/Android
- [ ] REST API for third-party integration
- [ ] Expanded brand reference database

### Long-term Vision:
- [ ] Real-time threat intelligence feeds
- [ ] Deep learning models for advanced evasion
- [ ] Multi-language content analysis
- [ ] Blockchain-based reputation scoring

## 🏆 Hackathon Impact

### Problem Solved:
✅ **Proactive Detection** - No more waiting for user reports  
✅ **Multi-Modal Analysis** - Comprehensive fraud assessment  
✅ **Real-time Processing** - Instant website scanning  
✅ **Explainable Results** - Transparent AI decisions  

### Business Applications:
- **Financial Institutions**: Customer protection
- **E-commerce Platforms**: Seller verification
- **Corporate Security**: Employee phishing prevention
- **Browser Vendors**: Built-in fraud protection

## 👥 Team

- *Harsh Jain*
- *Rishiraj Gupta*
- *Nikhil Singh*
- *Sumit Kothari*

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Hackathon organizers for the inspiring challenge
- Open-source community for the amazing tools
- Security researchers for fraud pattern insights

---

## 🎬 Demo Video

[![Demo Video]()

**Watch our complete system demonstration and technical walkthrough!**

---

**Built with ❤️ for a safer digital world**
