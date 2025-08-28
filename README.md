# 🦷 Teeth Segmentation with PyTorch & MONAI

This repository provides an implementation of **tooth segmentation** using [PyTorch](https://pytorch.org/) and [MONAI](https://monai.io/).  
The experiments are conducted on the [Tufts Dental Database](http://tdd.ece.tufts.edu/), which contains 1,000 annotated panoramic dental X-ray images.

---

## 📂 Dataset & Splits
The Tufts dataset (1,000 images) is randomly divided into:
- **70%** training  
- **20%** validation  
- **10%** testing  

To generate the splits, run:
```bash
python data_split.py
````

This will create a `data.json` file containing:

* dataset file lists
* class names
* class weights (for loss balancing in segmentation tasks)

---

## 🏗 Model

The segmentation model is a **U-Net** architecture implemented using `monai.networks`.

---

## 🚀 Training

To train the model, run:

```bash
python train.py -md "<model_directory>" -d "mps" -g 0 -bs 16 -lr 1e-4 -ne 100
```

Arguments:

* `-md` : path to save the trained model
* `-d`  : device (`"mps"`, `"cuda"`, or `"cpu"`)
* `-g`  : GPU index (if using CUDA)
* `-bs` : batch size (default: 16)
* `-lr` : learning rate (default: 1e-4)
* `-ne` : number of epochs (default: 100)

The script will:

* Save the best-performing model in the specified `model_directory`
* Track training/validation performance over epochs

---

## 📊 Evaluation

To evaluate a trained model:

```bash
python evaluation.py -md "<model_directory>" -d "mps" -g 0 -bs 1
```

This script computes evaluation metrics (Dice score) on training, validation, and test sets, and stores results in:

```
evaluation_results.csv
```

---

## 🖥 GUI Inference

A simple GUI is provided for interactive use:

```bash
python gui.py
```

Features:

* Load an input image
* Visualize the segmentation prediction
* Save the predicted mask if desired

Example:
![](gui.gif)

---

## 📌 Requirements

* Python 3.8+
* PyTorch
* MONAI
* OpenCV
* PyQt5 (for GUI)

Install dependencies via:

```bash
pip install -r requirements.txt
```

---

## 📜 License

This repository is released under the MIT License.
Please ensure that use of the **Tufts Dental Database** complies with its terms of access.

---

## 🙌 Acknowledgements

* [MONAI](https://monai.io/) – Medical Open Network for AI
* [Tufts Dental Database](http://tdd.ece.tufts.edu/) – Panoramic dental X-ray dataset

