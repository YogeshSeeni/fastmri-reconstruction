# fastMRI Reconstruction Experiments

This repository contains a series of notebooks and experiment logs for training neural networks on the [fastMRI](https://fastmri.org/) dataset. The goal is to explore different architectures for accelerated magnetic resonance image reconstruction. The project proceeds through several stages ranging from data preparation to final model comparisons.

## Project Steps

1. **Data Wrangling**  
   The notebook `data-wrangling.ipynb` (and its exported `data-wrangling.html`) demonstrates how the raw fastMRI files were loaded and converted into a format suitable for training. This step includes extracting slices from the provided k-space data and normalizing the resulting images.

2. **Baseline U-Net Training**  
   `baseline_unet.ipynb` establishes a reference by training a standard U-Net on the prepared dataset. Results of the best checkpoint are stored under `unet_baseline_single_experiment` and summarized in `unet_baseline_single_experiment/unet_baseline_single_experiment_summary.csv`.

3. **Transformer Variants**  
   Early experimentation with attention-based models is captured in `TransformerVariants.ipynb` and `Transformer_Variant_Tests.ipynb`. These notebooks explore different transformer blocks for image reconstruction.

4. **BT-U-Net Experiments**  
   The notebook `BT_Unet_Training.ipynb` trains a modified U-Net that incorporates transformer layers. Training logs and saved checkpoints reside in the `runs_bt_unet_experiment` directory with metrics summarized in `runs_bt_unet_experiment/bt_unet_experiment_summary.csv`.

5. **Swin U-Net Development**  
   Several notebooks refine a Swin-transformer based U-Net:
   - `Swin_UNET_Overfit.ipynb` performs a quick overfitting test to verify the implementation.
   - `Swin_UNET_Tuning.ipynb` searches hyperparameters such as learning rate and window size. Runs are saved in `runs_swin_tuning`.
   - `Swin_UNET_Retrain.ipynb` retrains promising configurations, recording results in `runs_retrain_compare`.
   - `Swin_UNET_Final_Training.ipynb` carries out the final training using the selected hyperparameters. Final checkpoints are found in `runs_swin_final`.

6. **Model Testing**  
   `Test_Models.ipynb` provides inference utilities for evaluating trained models on validation data. The `unet_output` directory stores example reconstructions from the baseline network.

7. **Comparison Summary**  
   The file `all_models_comparison_summary.csv` collects metrics across the main experiments for easy reference. It lists the validation loss, PSNR, SSIM, and corresponding checkpoint path for each trained model.

## Repository Layout

```
.
├── *.ipynb                        # Jupyter notebooks used throughout the project
├── runs_*                         # Folders with training logs and model checkpoints
├── unet_baseline_single_experiment
├── unet_output                    # Sample reconstructions from the baseline U-Net
├── all_models_comparison_summary.csv
└── README.md
```

Each `runs_*` folder corresponds to a particular set of experiments and contains tensorboard logs and saved `.pth` files.

## Getting Started

While the notebooks were developed in the fastMRI environment, they can run on any machine with PyTorch installed. Clone this repository and open the notebooks in Jupyter or JupyterLab. Training will require the fastMRI dataset, which can be downloaded from the [official site](https://fastmri.org/).

## Results

The best Swin U-Net models achieve validation PSNR above 62 dB and SSIM around 0.72, outperforming the baseline U-Net which reaches roughly 58 dB PSNR. Detailed numbers can be found in `all_models_comparison_summary.csv`.

