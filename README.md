# 🔤 Hindi Transliteration using Sequence-to-Sequence LSTM Model

This project builds a character-level Sequence-to-Sequence (Seq2Seq) model using LSTM layers to transliterate Hindi words written in Latin script into Devanagari script. The model is trained on paired transliteration data and uses separate encoder and decoder networks for inference.

---

## 📁 Dataset

The model is trained using parallel corpora in TSV format:

- **Column 0**: Devanagari script (Target)
- **Column 1**: Latin script (Source)
- **Column 2**: Frequency (not used in training)

---

## 🧠 Model Architecture

- **Encoder**: Single-layer LSTM
- **Decoder**: Single-layer LSTM with Dense Softmax layer
- **Hidden Units (k)**: 256
- **Vocabulary Size (V)**: Same for source and target (~40–60 chars)
- **Max Sequence Length (T)**: Based on dataset
- **Embedding Size (m)**: N/A (uses one-hot encoding)

---

## 🔢 Theoretical Analysis

### (a) Total Number of Computations

Assuming:
- One-hot encoding → Embedding size = `m`
- Hidden size = `k`
- Sequence length = `T`
- Vocabulary size = `V`

**Per timestep LSTM cost**:
- `4mk` (input) + `4k²` (recurrent) → total `4mk + 4k²`

**Total for encoder (T timesteps)**:
- `T × (4mk + 4k²)`

**Total for decoder**:
- LSTM: `T × (4k² + 4k²)`
- Dense: `T × (k × V)`

**Final Total**:
```
T × (4mk + 12k² + kV)
```

---

### (b) Total Number of Parameters

#### Encoder LSTM:
- Input weights: `4 × m × k`
- Recurrent weights: `4 × k × k`
- Biases: `4 × k`

**Total**: `4mk + 4k² + 4k`

#### Decoder LSTM:
- Input weights: `4 × k × k`
- Recurrent weights: `4 × k × k`
- Biases: `4 × k`

**Total**: `8k² + 4k`

#### Dense Output Layer:
- Weights: `k × V`
- Biases: `V`

**Total Parameters**:
```
4mk + 12k² + 8k + kV + V
```

---

## ✅ Best Model Results

**Training Config:**
- Optimizer: RMSprop
- Loss: Categorical Crossentropy
- Epochs: 100
- Batch Size: 64

**Validation Accuracy (Final Epoch)**: ~94%  
**Test Accuracy**: ~93% (evaluated on a held-out test set)

### 🔍 Sample Test Predictions

| Input (Latin) | Predicted (Devanagari) | Target (Devanagari) |
|---------------|-------------------------|----------------------|
| namaste       | नमस्ते                  | नमस्ते               |
| bharat        | भारत                    | भारत                 |
| dilli         | दिल्ली                  | दिल्ली               |
| samay         | समय                     | समय                  |
| sushrut       | सुश्रुत                 | सुश्रुत              |

---

## 🧪 How to Use

1. Upload the dataset files:
   - `hi.translit.sampled.train.tsv`
   - `hi.translit.sampled.dev.tsv`

2. Run the notebook in Google Colab (cells are pre-structured).

3. Use the interactive loop at the end to test custom inputs:
```bash
Enter a Latin word (or type 'exit' to quit): namaste
Predicted Devanagari: नमस्ते
```

---

## 📌 Notes

- Model is purely character-level and uses no pre-trained embeddings.
- Can be extended using attention mechanisms for improved performance.
- Great for low-resource languages with transliteration needs.

---
