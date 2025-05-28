# Triage AI - Medical Triage Engine

An AI-powered medical triage system that analyzes free-text clinical inputs to provide real-time risk stratification and care recommendations. Built with Google's Gemini 2.0 Flash for healthcare professionals.

## 🚨 Important Disclaimer

This tool is designed to **assist** healthcare professionals in triage decisions, not replace clinical judgment. It is NOT a diagnostic tool and should never be used as the sole basis for medical decisions. Always prioritize patient safety and clinical expertise.

## ✨ Features

- **Real-time Analysis**: Process clinical text in under 2 seconds
- **Structured Output**: Returns triage level, red flags, and suggested actions
- **Safety-First Design**: Defaults to urgent triage on errors
- **Batch Processing**: Analyze multiple cases simultaneously
- **JSON Integration**: Easy integration with existing healthcare systems
- **Color-Coded Display**: Visual urgency indicators for quick scanning

## 📋 Triage Levels

The system classifies patients into four triage levels:

- 🔴 **EMERGENT**: Immediate attention required - life-threatening condition
- 🟡 **URGENT**: Prompt evaluation needed - potential for deterioration  
- 🔵 **SEMI_URGENT**: Timely assessment required - stable but concerning
- 🟢 **ROUTINE**: Standard evaluation - no immediate risk identified

## 🚀 Quick Start

### Prerequisites

1. Python 3.7+
2. Google Gemini API key ([Get one here](https://makersuite.google.com/app/apikey))
3. Google Colab or local Python environment

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/triage-ai.git
cd triage-ai

# Install dependencies
pip install requests
```

### Basic Usage

```python
from triage_engine import MedicalTriageEngine

# Initialize with your API key
API_KEY = "your-gemini-api-key"
engine = MedicalTriageEngine(API_KEY)

# Analyze clinical text
clinical_text = """
52yo female with 2 hours of substernal chest pressure, 
radiating to left arm. Diaphoresis and mild SOB. 
Pain 7/10, not relieved by rest.
"""

result = engine.analyze_clinical_text(clinical_text)
print(engine.format_result_display(result))
```

### Output Example

```
🟡 ============================================================
MEDICAL TRIAGE ASSESSMENT
============================================================

⚡ TRIAGE LEVEL: URGENT
   Prompt evaluation needed - potential for deterioration
   
📊 CONFIDENCE: 85.0%

🚨 RED FLAGS IDENTIFIED:
   • Substernal chest pressure with radiation to left arm
   • Associated diaphoresis
   • Pain not relieved by rest
   • Classic cardiac presentation

📋 SUGGESTED ACTIONS:
   ✓ Immediate ECG
   ✓ Cardiac enzyme panel (troponin, CK-MB)
   ✓ Chest X-ray
   ✓ Aspirin administration if not contraindicated
   ✓ Cardiology consultation

💭 CLINICAL REASONING:
   Patient presents with classic signs of acute coronary syndrome...

⏰ Analysis Timestamp: 2024-01-15T14:32:15.123456
============================================================
```

## 🔧 Advanced Usage

### Batch Processing

```python
# Process multiple cases
cases = [
    "68yo male, sudden right-sided weakness, slurred speech",
    "28yo female, mild headache x 3 days, no other symptoms",
    "45yo male, severe abdominal pain, rigid abdomen, fever"
]

results = engine.batch_analyze(cases)
for i, result in enumerate(results):
    print(f"Case {i+1}: {result.triage_level}")
```

### JSON Integration

```python
# Input from your EHR/system
patient_data = {
    "patient_id": "12345",
    "clinical_text": "45yo male, worst headache of life...",
    "source": "ED triage"
}

# Process and get JSON output
result = engine.analyze_clinical_text(patient_data["clinical_text"])
json_output = engine.to_json(result)
print(json_output)
```

### Google Colab Setup

```python
# One-line setup for Colab
from triage_engine import setup_colab
engine = setup_colab()  # Returns configured engine
```

## 📊 API Response Structure

```json
{
    "triage_level": "URGENT",
    "confidence": 0.85,
    "red_flags": [
        "Chest pressure with cardiac features",
        "Diaphoresis",
        "Pain radiating to arm"
    ],
    "suggested_actions": [
        "Immediate ECG",
        "Cardiac enzymes",
        "Cardiology consultation"
    ],
    "reasoning": "Classic presentation of acute coronary syndrome...",
    "timestamp": "2024-01-15T14:32:15.123456"
}
```

## 🏥 Use Cases

- **Emergency Department Triage**: Rapid initial assessment of walk-in patients
- **Telemedicine Screening**: Risk stratification for virtual consultations
- **EMS Handoff Analysis**: Processing paramedic reports for receiving teams
- **Nursing Triage Lines**: Supporting phone-based triage decisions
- **Clinical Documentation**: Analyzing consultation notes for urgency

## ⚙️ Configuration

### Custom Triage Levels

```python
# Modify triage levels for your institution
engine.triage_levels = {
    "CRITICAL": "Immediate resuscitation required",
    "EMERGENT": "See within 15 minutes",
    "URGENT": "See within 30 minutes",
    "LESS_URGENT": "See within 60 minutes",
    "NON_URGENT": "See within 120 minutes"
}
```

### Model Parameters

```python
# Adjust for your needs
engine.generation_config = {
    "temperature": 0.1,      # Lower = more consistent
    "max_output_tokens": 1024,
    "top_p": 0.95
}
```

## 🔐 Security & Compliance

- **Data Privacy**: No patient data is stored by the system
- **API Security**: Use environment variables for API keys
- **HIPAA**: Ensure your Gemini API usage complies with healthcare regulations
- **Audit Trail**: All analyses are timestamped for record-keeping

```python
# Secure API key handling
import os
API_KEY = os.environ.get('GEMINI_API_KEY')
```

## 📈 Performance

- Average response time: 1-2 seconds
- Supports batch processing up to 100 cases
- Gemini 2.0 Flash optimized for speed and accuracy
- Low API costs (~$0.001 per triage)

## 🤝 Contributing

Contributions are welcome! Please read our contributing guidelines and submit pull requests to our repository.

### Development Setup

```bash
# Clone and setup development environment
git clone https://github.com/yourusername/triage-ai.git
cd triage-ai
pip install -r requirements-dev.txt
python -m pytest tests/
```

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## ⚠️ Medical Disclaimer

This software is not FDA-approved and should not be used as a medical device. It is intended for research and development purposes only. Healthcare providers must use their clinical judgment and follow institutional protocols. The authors and contributors assume no liability for clinical decisions made using this tool.

## 🙏 Acknowledgments

- Built with Google's Gemini 2.0 Flash API
- Developed in collaboration with emergency medicine physicians
- Inspired by the need for rapid, consistent triage decisions

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/neuron-cloud/triage-ai/issues)
- **Documentation**: [Full Documentation](https://neuron-cloud.github.io/triage-ai)
- **Email**: mwdelgardo@gmail.com

---

**Remember**: This tool assists but never replaces clinical judgment. When in doubt, always err on the side of patient safety.
