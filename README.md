# A Fusion-Based Multiomics Approach for Enhanced Accuracy in Non-Small Cell Lung Cancer Biomarker Discovery

<img width="1525" height="1043" alt="Graphical_abstract_revised" src="https://github.com/user-attachments/assets/3fca8604-06d8-4dd0-82dc-52540560ca27" />

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

<img width="2745" height="2548" alt="Fig1_revised" src="https://github.com/user-attachments/assets/ffe655d8-40f5-4955-8044-bfc6fa9205b3" />

The above image is the graphical representation of the methodology followed in the manuscript. The experiment could be executed as follows:
1. Copy the datasets to your desired directory (in code:  ```Z:\multiomics based manuscript\datasets\...```).
2. Replace the path in code with your directory path.
3. Create a directory to dump the results (in code: ```Z:\multiomics based manuscript\results_for_xena_rna_cnv_only\...```). Replace the path in code with your directory path in ```dump_all_results()``` method.
4. ```good_seeds``` is the list of seed values you need to iterate the experiment.
5. Each model could be run separately. To run all the models at once, select the ```Run all``` command in the jupyter notebook.

## Results
| Model/Approach 	|   Accuracy   	|    AUROC    	| Precision (PPV) 	| Recall (Sensitivity) 	| Specificity 	|   F1-Score  	|     NPV     	|
|:--------------:	|:------------:	|:-----------:	|:---------------:	|:--------------------:	|:-----------:	|:-----------:	|:-----------:	|
|     XGB-RNA    	|  0.954±0.001 	|  0.991±0.00 	|   0.942±0.002   	|      0.97±0.001      	| 0.938±0.002 	| 0.956±0.001 	| 0.968±0.001 	|
|     XGB-CNV    	| 0.892±0.005 	| 0.953±0.001 	|   0.891±0.003   	|      0.899±0.008     	| 0.885±0.003 	| 0.895±0.005 	| 0.894±0.008 	|
|   XGB-Fusion   	|  0.958±0.001 	| 0.982±0.001 	|   0.947±0.002   	|      0.972±0.003     	| 0.943±0.003 	| 0.959±0.001 	|  0.97±0.003 	|
|     SVC-RNA    	|  0.951±0.00  	|  0.987±0.00 	|   0.928±0.001   	|       0.98±0.0       	| 0.921±0.001 	|  0.954±0.00 	|  0.977±0.0  	|
|     SVC-CNV    	|  0.92±0.002  	|  0.96±0.00  	|    0.90±0.003   	|      0.944±0.001     	| 0.894±0.003 	| 0.924±0.001 	| 0.939±0.001 	|
|   SVC-Fusion   	|  0.952±0.00  	|  0.98±0.00  	|   0.938±0.001   	|      0.971±0.001     	| 0.932±0.002 	|  0.954±0.00 	| 0.969±0.001 	|
|     MLP-RNA    	|  0.80±0.069  	|  0.90±0.06  	|   0.786±0.125   	|      0.893±0.117     	| 0.703±0.230 	| 0.822±0.042 	| 0.892±0.095 	|
|     MLP-CNV    	|  0.904±0.004 	| 0.958±0.003 	|   0.907±0.004   	|      0.906±0.008     	| 0.902±0.005 	| 0.907±0.004 	| 0.902±0.007 	|
|   MLP-Fusion   	|  0.919±0.011 	| 0.968±0.004 	|   0.917±0.006   	|      0.926±0.019     	| 0.912±0.006 	| 0.921±0.012 	| 0.922±0.019 	|
|   TabNet-RNA   	|  0.698±0.038 	| 0.782±0.046 	|   0.733±0.065   	|      0.655±0.048     	| 0.743±0.084 	|  0.69±0.032 	|  0.673±0.03 	|
|   TabNet-CNV   	|  0.831±0.012 	| 0.926±0.005 	|   0.891±0.015   	|      0.764±0.038     	| 0.902±0.020 	| 0.823±0.016 	| 0.786±0.024 	|
|  TabNet-Fusion 	|  0.848±0.01  	| 0.925±0.006 	|   0.903±0.017   	|      0.788±0.032     	|  0.911±0.02 	| 0.841±0.014 	| 0.805±0.021 	|

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




































