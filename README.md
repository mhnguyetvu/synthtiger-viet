# 🇻🇳 SynthTIGER-VIET

A Vietnamese adaptation of the [SynthTIGER](https://github.com/clovaai/synthtiger) engine for generating synthetic training data for text recognition tasks. This project helps create high-quality image-text pairs tailored to Vietnamese OCR systems (e.g., [OpenOCR](https://github.com/Topdu/OpenOCR)).

---

## 📦 Features

- Generate large-scale synthetic Vietnamese OCR datasets
- Customize fonts, corpus, background styles, and distortions
- Automatically produce training label files compatible with OpenOCR
- Supports augmentation for low-resource or noisy text settings

---

## 🛠 Installation

```bash
git clone https://github.com/mhnguyetvu/synthtiger-viet.git
cd synthtiger-viet
pip install -r requirements.txt
```

---

## 🗂 Directory Structure

```
synthtiger-viet/
├── synthgen/                    # Core image/text generation logic
├── font-full-800/              # Vietnamese fonts
├── corpus/                     # Vietnamese text corpora
│   └── vietnamese_corpus.txt   # Cleaned and curated sentences
├── output_vi/                  # Output folder for generated images and labels
├── config_vi.yml               # YAML config controlling generation options
├── generate.py                 # Main script for generating synthetic data
└── README.md
```

---

## ⚙️ Usage

### 🔤 Step 1: Prepare the corpus

Place a clean corpus file in `corpus/vietnamese_corpus.txt`.  

---

### 🖼 Step 2: Run the generator

```bash
python generate.py --config config_vi.yml
```

This will create:

- Synthetic images in `output_vi/images/`
- Training label file in `output_vi/rec_gt_train.txt`

---

## 🧩 Integration with OpenOCR

To use the generated data for fine-tuning [OpenOCR](https://github.com/Topdu/OpenOCR):

Update your `repsvtr_ch.yml` config:

```yaml
Train:
  dataset:
    name: SimpleDataSet
    data_dir: ../synthtiger-viet/output_vi/
    label_file_list: ["../synthtiger-viet/output_vi/rec_gt_train.txt"]

Eval:
  dataset:
    name: SimpleDataSet
    data_dir: ../synthtiger-viet/output_vi/
    label_file_list: ["../synthtiger-viet/output_vi/rec_gt_test.txt"]
```

> 📌 Tip: You can split your generated data into `train` and `test` sets manually or script it using `train_test_split()` from `sklearn`.

---

## 📚 TODO

- [ ] Support Vietnamese text detection box generation
- [ ] Add UI for easier config editing
- [ ] Upload pretrained models on synthetic + real Vietnamese datasets

---

## 🙋‍♀️ Author

Created by [Nguyệt Vũ](https://github.com/mhnguyetvu)  
Feel free to contribute or open an issue!

---

## 📄 License

This project is MIT licensed. Font files and corpus contents belong to their respective owners.
