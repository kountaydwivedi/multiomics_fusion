# A Fusion-Based Multiomics Approach for Enhanced Accuracy in Non-Small Cell Lung Cancer Biomarker Discovery

<img width="4766" height="3259" alt="Graphical Abstract" src="https://github.com/user-attachments/assets/ddfae9d4-10a2-4ed5-80e0-a7f226bf5f87" />

This repository contains the implementation codes for our study entitled “A Fusion-Based Multiomics Approach for Enhanced Accuracy in Non-Small Cell Lung Cancer Biomarker Discovery”. Here is the [link](https://doi.org/10.1101/2025.05.02.25326847) to the medRxiv version of the manuscript.

**Authors:** [Kountay Dwivedi](https://orcid.org/0000-0001-5439-0567), [Amirreza Mahbod](https://orcid.org/0000-0001-5042-1442), [Rupert C. Ecker](https://orcid.org/0000-0002-1095-8592), [Klara Janjić](https://orcid.org/0000-0002-8057-3567)

---
## Setup Environment
```
conda env create -f multiomics_fusion
conda activate multiomics_fusion
pip install torch==2.5.1 torchvision==0.21.0 torchaudio==2.6.0 --index-url https://download.pytorch.org/whl/cu124
pip install pytorch-tabnet
```
Pytorch: v2.5.1;<br>
CUDA: v12.4;<br>
Python: v3.12.3<br>
Install ```pytorch-tabnet``` to employ the transformer-based TabNet model for fusion.

## Directory Structure
The repository comprises two folders: ```code``` and ```datasets\with_common_patients_processed```
<br>```code\models_training.ipynb```: Main implementation notebook.
<br>```code\make_volcano_from_47_genes.ipynb```: Notebook to plot volcano plot (redundant).
<br>```code\compute feature importance-reliefF.ipynb```: Notebook to compute feature importance score via ReliefF method.

<br>```datasets\with_common_patients_processed\csv_cnv_common_luad.csv```: CSV with CNV data for common patients across adenocarcinoma (ADC)
<br>```datasets\with_common_patients_processed\csv_cnv_common_lusc.csv```: CSV with CNV data for common patients across squamous cell carcinoma (SCC)
<br>```datasets\with_common_patients_processed\csv_rna_common_luad.csv```: CSV with RNA data for common patients across adenocarcinoma (ADC)
<br>```datasets\with_common_patients_processed\csv_rna_common_lusc.csv```: CSV with RNA data for common patients across squamous cell carcinoma (SCC)

## Running the code

<img width="8578" height="7963" alt="Figure 1" src="https://github.com/user-attachments/assets/bc7cd14e-d8ef-4881-bd9f-872ecb9a1282" />

The above image is the graphical representation of the methodology followed in the manuscript. The experiment could be executed as follows:
1. Copy the datasets to your desired directory (in code:  ```Z:\multiomics based manuscript\datasets\...```).
2. Replace the path in code with your directory path.
3. Create a directory to dump the results (in code: ```Z:\multiomics based manuscript\results_for_xena_rna_cnv_only\...```). Replace the path in code with your directory path in ```dump_all_results()``` method.
4. ```good_seeds``` is the list of seed values you need to iterate the experiment.
5. Each model could be run separately. To run all the models at once, select the ```Run all``` command in the jupyter notebook.

## Results
| Model/Approach | Accuracy    | F1-Score    | AUROC       |
|----------------|-------------|-------------|-------------|
| XGB-RNA        | 0.958±0.0   | 0.959±0.0   | 0.991±0.0   |
| XGB-CNV        | 0.890±0.002 | 0.890±0.002 | 0.953±0.002 |
| **XGB-Fusion**     | **0.961±0.0**   | **0.961±0.0**   | **0.982±0.001** |
| SVC-RNA        | 0.951±0.001 | 0.951±0.0   | 0.987±0.0   |
| SVC-CNV        | 0.921±0.002 | 0.920±0.003 | 0.960±0.001 |
| **SVC-Fusion**     | **0.954±0.001** | **0.954±0.0**   | **0.980±0.0**   |
| MLP-RNA        | 0.852±0.012 | 0.852±0.045 | 0.935±0.023 |
| MLP-CNV        | 0.900±0.004 | 0.900±0.002 | 0.956±0.002 |
| **MLP-Fusion**     | **0.920±0.004** | **0.920±0.0**   | **0.971±0.002** |
| TabNet-RNA     | 0.734±0.016 | 0.733±0.007 | 0.834±0.036 |
| TabNet-CNV     | 0.836±0.009 | 0.836±0.023 | 0.930±0.005 |
| **TabNet-Fusion**  | **0.850±0.009** | **0.848±0.009** | **0.931±0.008** |

The accuracy of fusion-based approach outperforms models trained on individual omics types.

## Citation
medRxiv citation:
```
@article{dwivedi2025fusion,
  title={A Fusion-Based Multiomics Classification Approach for Enhanced Gene Discovery in Non-Small Cell Lung Cancer},
  author={Dwivedi, Kountay and Mahbod, Amirreza and Ecker, Rupert C and Janji{\'c}, Klara},
  journal={medRxiv},
  pages={2025--05},
  year={2025},
  publisher={Cold Spring Harbor Laboratory Press}
}
```

---




































