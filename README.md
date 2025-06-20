# ETLCDB Unpacker

This repository provides a tool to **unpack and convert handwritten Japanese character datasets** from the ETL Character Database (ETLCDB) into usable image files with metadata.

---

##  Project Structure

```
unpack_etlcdb/
├── ETL2_1                # ETL2 data file (binary)
├── ETL2_1_unpack/        # Output folder with extracted images and CSV
├── unpack.py             # Main script to extract characters
├── requirements.txt      # Python dependencies
├── euc_co59.dat          # Optional mapping table for character encoding
├── .gitignore
└── README.md             # This file
```

---

##  Getting Started

###  Requirements

- Python 3.9 or newer
- pip (Python package installer)

###  Install Dependencies

Run the following command to install the required Python packages:

```bash
pip install -r requirements.txt
```

---

##  Unpacking Instructions

To unpack a dataset file (e.g., `ETL2_1`), run:

```bash
python unpack.py ETL2_1
```

This will:
- Create a folder named `ETL2_1_unpack/`
- Save extracted grayscale PNG images (one per character)
- Generate a `metadata.csv` file containing the character label and other info

---

##  Command Line Usage

You can customize how the script runs:

### View Help

```bash
python unpack.py --help
```

###  Example with options

```bash
python unpack.py ETL2_1 --output_dir extracted_images --fields codepoint label writer
```

| Option        | Description                                 |
|---------------|---------------------------------------------|
| `--output_dir`| Specify a custom output folder              |
| `--fields`    | Choose which metadata fields to write       |

---

##  Output Format

The script produces:

```
ETL2_1_unpack/
├── 00000.png
├── 00001.png
├── ...
└── metadata.csv
```

### Example `metadata.csv`:

```csv
index,codepoint,label,writer
0,0x30A2,ア,writer_01
1,0x30AB,カ,writer_01
...
```

- Each image corresponds to a line in the CSV (filename = line index).
- Images are grayscale and preprocessed for training or analysis.

---

## 📚 About the ETL Dataset

- Developed by AIST (Japan)
- Contains handwritten **kana** and **kanji** characters
- Different ETL versions (ETL1–ETL9) use different binary layouts
- More info: [ETLCDB official site](http://etlcdb.db.aist.go.jp/)

---

##  Use Cases

- Build Japanese OCR pipelines
- Train models on kana or kanji recognition
- Compose word-level datasets from character images
- Data augmentation for Japanese handwritten text research

---

## 🧪 Example Use with PyTorch

You can easily build a PyTorch `Dataset` using the extracted images and `metadata.csv` (not included here — let us know if needed).

---

##  Notes

- File format varies between ETL datasets (e.g., ETL8G, ETL9G). This script may need adjustment for those.
- All paths must be correct relative to the working directory.
- Images are extracted from 4-bit binary format and converted to 8-bit grayscale.

---

##  License

The ETLCDB datasets are provided by **AIST** and are intended for academic research. Use them in compliance with [AIST's license](http://etlcdb.db.aist.go.jp/).

This unpacking script is released under the MIT License.

---

##  Support

For questions or issues, feel free to open an issue or contact the maintainer.
