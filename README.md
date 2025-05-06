<div align="center"> <h1>Bengali Translation Evaluator</h1> </div>

<div align="center"> 

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue)](https://www.python.org/)
[![Transformers](https://img.shields.io/badge/Transformers-4.0%2B-orange)](https://huggingface.co/transformers/)
[![NLTK](https://img.shields.io/badge/NLTK-3.6%2B-green)](https://www.nltk.org/)

An interactive tool for evaluating English-to-Bengali machine translations using the NLLB (No Language Left Behind) model and METEOR evaluation metrics. 
The tool uses **Facebook's NLLB-200-1.3B** model to translate English text to Bengali.

</div>

## Features

- Translate English text to Bengali using Facebook's NLLB-200-1.3B model
- Compare machine translations against multiple human reference translations
- Calculate METEOR evaluation scores to assess translation quality
- Interactive command-line interface for easy usage

## 📋 Requirements

- Python 3.7 or higher
- transformers
- nltk
- sacrebleu

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/AHMED-SAFA/Bengali-Translation-Evaluator.git
   cd Bengali-Translation-Evaluator
   ```

2. Install the required dependencies:
   ```bash
   pip install transformers nltk sacrebleu
   ```

3. Download required NLTK data:
   ```python
   import nltk
   nltk.download('wordnet')
   nltk.download('omw-1.4')
   ```

## 💻 Usage

### Basic Usage

```python
from translator import translate_user_input

# Start the interactive translation and evaluation session
translate_user_input()
```

### Example Session

```python
--- User Input Translation with Multiple References ---

For each English input, two reference Bengali translations needed
The function will calculate METEOR scores for each reference and their average

Enter English text to translate to Bengali (or type 'exit' to quit): I am going to the market.

Step 1: Translating input text...

English: I am going to the market.
Model Translation: আমি বাজারে যাচ্ছি।

Step 2: Collecting reference translations...
Enter 1st reference Bengali translation: আমি বাজারে যাচ্ছি।
Enter 2nd reference Bengali translation: আমি হাটে যাচ্ছি।

Step 3: Calculating METEOR score for 1st reference...
Reference 1: আমি বাজারে যাচ্ছি।
METEOR Score 1: 1.0000

Step 4: Calculating METEOR score for 2nd reference...
Reference 2: আমি হাটে যাচ্ছি।
METEOR Score 2: 0.7500

Step 5: Calculating average METEOR score...
Average METEOR Score: 0.8750
Calculation: (1.0000 + 0.7500) / 2 = 0.8750

--------------------------------------------------
```

## How It Works

1. **Translation**: The tool uses **Facebook's NLLB-200-1.3B** model to translate English text to Bengali
2. **Reference Collection**: Users provide two reference translations for comparison
3. **METEOR Calculation**: The tool calculates METEOR scores between the machine translation and each reference
4. **Evaluation**: An average METEOR score is computed to evaluate overall translation quality

### Key Components

```python
def calculate_meteor(reference, hypothesis):
    """Calculate METEOR score between reference and hypothesis."""
    try:
        reference_tokens = reference.split()
        hypothesis_tokens = hypothesis.split()
        score = meteor_score([reference_tokens], hypothesis_tokens)
        return score
    except Exception as e:
        print(f"Error calculating METEOR score: {e}")
        return None
```

## 📊 METEOR Score Interpretation

The METEOR (Metric for Evaluation of Translation with Explicit ORdering) score ranges from 0 to 1:

- **1.0**: Perfect match with the reference
- **0.7-0.9**: High-quality translation
- **0.5-0.7**: Moderate-quality translation
- **Below 0.5**: Low-quality translation that may need improvement

## 🔧 Advanced Configuration

You can modify the model parameters for different translation requirements:

```python
tokenizer = AutoTokenizer.from_pretrained("facebook/nllb-200-3.3B")  # Larger model
model = AutoModelForSeq2SeqLM.from_pretrained("facebook/nllb-200-3.3B")

translation = translator(user_input, max_length=512, num_beams=5)
```

## 📚 About NLLB

The **No Language Left Behind (NLLB)** model by Meta AI is designed to provide high-quality translations across 200+ languages, 
including many low-resource languages. This project utilizes the NLLB-200-1.3B model, which offers a good balance between performance and resource requirements.


## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---
