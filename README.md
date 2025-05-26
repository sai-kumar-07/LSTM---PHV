# Bi-LSTM for Human-Dengue Protein-Protein Interaction Prediction

This repository presents a deep learning approach for predicting protein-protein interactions between dengue virus and human proteins using Bidirectional Long Short-Term Memory (BiLSTM) networks. Our model achieved an impressive **92.4% AUC score** on the test set, demonstrating the effectiveness of sequence-based neural architectures for understanding host-pathogen interactions. The research successfully identified biologically relevant pathways, including the Glycosphingolipid biosynthesis pathway known to be exploited by dengue virus for host cell entry, validating the biological significance of our computational predictions.

## Abstract

Protein–protein interactions between viral and human proteins play a vital role in the development and progression of infectious diseases. Viruses such as the dengue virus often exploit host cell processes by interacting with crucial human proteins, aiding in viral replication, immune system evasion, and the onset of disease symptoms. Gaining insight into these interactions is essential to understand host-pathogen relationships, disruptions in cellular signaling pathways, and identifying potential targets for antiviral therapies.

In this work, protein sequences are encoded using k-mers and processed by separate BiLSTM models—one for human and one for dengue proteins—to generate embeddings. These embeddings are then combined and fed into a fully connected neural network trained on labeled interaction data to predict interactions.

Our model achieved an **AUC score of 92.4%** on the test set. Additionally, the Glycosphingolipid biosynthesis – lacto and neolacto series pathway was enriched in the result of pathway enrichment analysis. This pathway is known to be targeted by the dengue virus for host cell entry, supporting the biological relevance of our predictions.


## Dataset Construction

### Sequence Similarity Filtering
- **Tool Used**: `cdhit` tool for sequence redundancy removal
- **Threshold**: Proteins with >90% similarity were excluded to prevent overfitting
- **Output**: Non-redundant protein sequences for both human and dengue datasets

### K-mer Representation
- **Approach**: 4-mer decomposition of protein sequences
- **Format**: CSV file with protein labels and corresponding 4-mers
- **Word Embedding**: CBOW Word2Vec model training on k-mer sequences

### Negative Sample Preparation
Negative samples were systematically generated based on subcellular localization principles:
- **Rationale**: Proteins in different subcellular compartments are less likely to interact
- **Data Source**: Subcellular localization information for both human and dengue proteins
- **Balancing**: Number of negative samples matched to positive samples

### Word2Vec Model Configuration
- **Architecture**: Continuous Bag of Words (CBOW)
- **Embedding Dimension**: 128
- **Training Iterations**: 100
- **Implementation**: `w2v_R.ipynb`

## Dataset Files

### Positive Interactions (`Positive_Den_Human.txt`)
Sample entries showing confirmed dengue-human protein interactions:

1 E interacts with 917 CD3G AIY68806.1_Envelope_DV1
1 E Binds to 30835 CD209 AIY68806.1_Envelope_DV1
2 C Upregulates 1191 CLU NP_739591.2_Capsid_DV2
2 NS4B inhibits interferon (IFN)-induced host 6772 STAT1 NP_739589.2_NS4B_DV2


### Negative Interactions (`Neg_Den_Human.txt`)
Sample entries for non-interacting protein pairs:

BAV37877.1_capsid_DV1 COL2A1
BAV37877.1_capsid_DV1 ENGASE
AIY68806.1_Envelope_DV1 SUCO
URC21202.1_NS5_DV1 STEAP3


## Methodology

### Step 1: Protein Embedding Generation (`Pre lstm reg.ipynb`)

1. **K-mer Embeddings Loading**
   - Load pre-trained embeddings from `kmers_embedding_human_dengue.txt`
   - **Download Link**: [K-mer Embeddings](https://drive.google.com/file/d/1sUM9RPoDaWUbB3mPZ-bBMyKpT46v9WPG/view?usp=sharing)
   - Consider top 100 k-mers for computational efficiency

2. **BiLSTM Training**
   - Train separate BiLSTM models for human (`Humans.csv`) and dengue (`Dengue.csv`) proteins
   - **Input**: 100×128 k-mer embeddings per protein
   - **Output**: 1×128 merged protein embedding
   - Save trained models for reuse

### Step 2: Interaction Prediction (`FC lstm reg.ipynb`)

- **Architecture**: Fully connected neural network
- **Input**: Concatenated protein embeddings from Step 1 + interaction labels from `interactions.csv`
- **Task**: Binary classification for protein-protein interaction prediction
- **Performance**: 92.4% AUC score achieved

### Step 3: Evaluation and Biological Analysis

#### Primary Evaluation (`Eval.ipynb`)
- **Dataset**: `random_int_1.txt` - Random protein interaction pairs
- **Purpose**: Model performance assessment on unseen data

#### Secondary Evaluation (`Eval 2.ipynb`)
- **Dataset**: `unknown_pair_den_human_One.txt` - Novel protein pairs
- **Purpose**: Discovery of potential biological markers and pathways

## Key Results

### Model Performance
- **AUC Score**: 92.4% on test set
- **Architecture**: BiLSTM + Fully Connected Network
- **Feature Representation**: K-mer based protein encoding

### Biological Validation
- **Pathway Enrichment**: Glycosphingolipid biosynthesis – lacto and neolacto series pathway
- **Biological Relevance**: This pathway is known to be targeted by dengue virus for host cell entry
- **Significance**: Validates the biological accuracy of computational predictions

## Installation and Usage

### Prerequisites
pip install tensorflow
pip install keras
pip install pandas
pip install numpy
pip install scikit-learn
pip install matplotlib
pip install seaborn


### Running the Pipeline

1. **Train Word2Vec Model**:

2. **Generate Protein Embeddings**:


3. **Train PPI Prediction Model**:


4. **Evaluate Results**:


## Data Download

The pre-trained k-mer embeddings can be downloaded from:
🔗 **[K-mer Embeddings Download](https://drive.google.com/file/d/1sUM9RPoDaWUbB3mPZ-bBMyKpT46v9WPG/view?usp=sharing)**

## File Descriptions

| File | Purpose |
|------|---------|
| `w2v_R.ipynb` | Word2Vec model training for k-mer embeddings |
| `Pre lstm reg.ipynb` | BiLSTM training for protein sequence embeddings |
| `FC lstm reg.ipynb` | Fully connected network for interaction prediction |
| `Eval.ipynb` | Model evaluation on random interactions |
| `Eval 2.ipynb` | Biological marker discovery evaluation |
| `interactions.csv` | Processed interaction dataset for training |
| `Humans.csv` | Unique human protein sequences |
| `Dengue.csv` | Unique dengue virus protein sequences |
| `additional_fv_human.txt` | Additional human protein features (optional) |
| `additional_fv_den.txt` | Additional dengue protein features (optional) |

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

**Note**: The additional feature vectors (`additional_fv_human.txt` and `additional_fv_den.txt`) are available but were not used in the final model as they did not improve performance significantly.

