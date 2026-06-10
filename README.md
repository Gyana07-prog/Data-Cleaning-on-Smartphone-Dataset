# 📱 Smartphone Dataset — Data Cleaning Project

A comprehensive **data cleaning and wrangling** project that transforms a raw smartphone specifications dataset (1,020 entries) into a well-structured, analysis-ready format. The project identifies and resolves **20 data quality issues** and **7 tidiness issues** across 11 original columns, producing a final cleaned dataset with **31 enriched columns** and **980 records**.

---

## 📂 Project Structure

```
Smartphone Dataset/
│
├── smartphones - smartphones.csv          # Raw source dataset (1,020 records × 11 columns)
├── .ipynb                                 # Jupyter Notebook with full cleaning pipeline
├── cleaned_smartphone_data1.csv           # Stage 1: Initial quality fixes
├── cleaned_smartphone_data2.csv           # Stage 2: Processor & SIM splitting
├── cleaned_smartphone_data3.csv           # Stage 3: RAM & battery splitting
├── cleaned_smartphone_data4.csv           # Stage 4: Display & camera splitting
├── cleaned_smartphone_data5.csv           # Stage 5: Final cleaned dataset (memory card & OS)
└── README.md                             # This file
```

---

## 📊 Dataset Overview

| Property       | Raw Dataset                | Cleaned Dataset             |
| -------------- | -------------------------- | --------------------------- |
| **Records**    | 1,020                      | 980                         |
| **Columns**    | 11                         | 31                          |
| **File**       | `smartphones - smartphones.csv` | `cleaned_smartphone_data5.csv` |
| **Duplicates** | 0                          | 0                           |

### Original Columns

| Column      | Description                                      |
| ----------- | ------------------------------------------------ |
| `model`     | Smartphone model name                            |
| `price`     | Price in INR (₹) with commas and currency symbol |
| `rating`    | Rating score (out of 100)                        |
| `sim`       | SIM and connectivity details                     |
| `processor` | Processor name, cores, and clock speed           |
| `ram`       | RAM and internal storage combined                |
| `battery`   | Battery capacity and charging details            |
| `display`   | Screen size, resolution, refresh rate            |
| `camera`    | Front and rear camera specifications             |
| `card`      | Memory card support details                      |
| `os`        | Operating system and version                     |

### Final Cleaned Columns (31 total)

| Column                     | Type    | Description                              |
| -------------------------- | ------- | ---------------------------------------- |
| `index`                    | int     | Original row index reference             |
| `brand_name`               | str     | Extracted & normalized brand name        |
| `model`                    | str     | Phone model name                         |
| `price`                    | int     | Price in INR (numeric)                   |
| `rating`                   | float   | Rating score (60–89 scale)               |
| `sim`                      | str     | SIM & connectivity info                  |
| `has_5g`                   | bool    | Whether the phone supports 5G           |
| `has_nfc`                  | bool    | Whether the phone has NFC               |
| `has_ir_blaster`           | bool    | Whether the phone has IR Blaster        |
| `processor`                | str     | Full processor string                    |
| `processor_name`           | str     | Processor chipset name                   |
| `processor_brand`          | str     | Processor brand (e.g., snapdragon)       |
| `num_cores`                | str     | Number of cores and clock speed          |
| `processor_speed`          | str     | CPU clock speed                          |
| `ram`                      | str     | Original RAM string                      |
| `ram_capacity`             | str     | RAM size (e.g., 6 GB)                    |
| `internal_storage`         | str     | Internal storage (e.g., 128 GB)          |
| `battery`                  | str     | Original battery string                  |
| `battery_capacity`         | str     | Battery capacity (e.g., 5000 mAh)       |
| `fast_charging`            | str     | Fast charging wattage (e.g., 67W)        |
| `display`                  | str     | Original display string                  |
| `screen_size`              | str     | Screen size in inches                    |
| `resolution`               | str     | Display resolution (e.g., 1080 x 2400 px)|
| `refresh_rate`             | str     | Refresh rate (e.g., 120 Hz)              |
| `camera`                   | str     | Original camera string                   |
| `num_rear_cameras`         | int     | Count of rear cameras                    |
| `num_front_cameras`        | int     | Count of front cameras                   |
| `card`                     | str     | Original memory card string              |
| `extended_memory_available`| int     | Whether expandable storage is supported  |
| `extended_upto`            | str     | Max expandable storage capacity          |
| `os`                       | str     | Operating system (normalized)            |

---

## 🔍 Data Assessment

### Quality Issues Identified (20)

| #  | Column      | Issue                                                                                 | Category      |
| -- | ----------- | ------------------------------------------------------------------------------------- | ------------- |
| 1  | `model`     | Inconsistent brand naming (e.g., "OPPO" vs "Oppo")                                   | Consistency   |
| 2  | `price`     | Contains currency symbol `₹`                                                         | Validity      |
| 3  | `price`     | Contains commas between digits                                                        | Validity      |
| 4  | `price`     | Namotel phone has unrealistic price of ₹99                                            | Accuracy      |
| 5  | `rating`    | 141 missing values                                                                    | Completeness  |
| 6  | `processor` | Incorrect/shifted values for some Samsung & feature phones                            | Validity      |
| 7  | `model`     | iPod present in row 756 (not a smartphone)                                            | Validity      |
| 8  | `ram`       | Incorrect values in 24 rows (data shifted across columns)                             | Validity      |
| 9  | `battery`   | Incorrect values in 33 rows                                                           | Validity      |
| 10 | `display`   | Refresh rate sometimes missing                                                        | Completeness  |
| 11 | `display`   | Incorrect values in 27 rows                                                           | Validity      |
| 12 | Various     | Foldable phone info scattered across wrong columns                                    | Validity      |
| 13 | `camera`    | Inconsistent notation (Dual/Triple/Quad, `&` separator)                               | Consistency   |
| 14 | `camera`    | Incorrect values in 64 rows                                                           | Validity      |
| 15 | `card`      | Sometimes contains OS and camera info instead                                         | Validity      |
| 16 | `os`        | Sometimes contains Bluetooth and FM radio info                                        | Validity      |
| 17 | `os`        | Incorrect values in specific rows (324, 378)                                          | Validity      |
| 18 | `os`        | Contains version names (e.g., "Lollipop") instead of version numbers                 | Consistency   |
| 19 | Various     | Missing values in `camera`, `card`, and `os` columns                                  | Completeness  |
| 20 | `price`     | Data type is string instead of numeric                                                | Validity      |

### Tidiness Issues Identified (7)

| #  | Column      | Issue                                                          |
| -- | ----------- | -------------------------------------------------------------- |
| 1  | `sim`       | Should split into `has_5g`, `has_nfc`, `has_ir_blaster`        |
| 2  | `ram`       | Should split into `ram_capacity` and `internal_storage`        |
| 3  | `processor` | Should split into `processor_name`, `num_cores`, `processor_speed` |
| 4  | `battery`   | Should split into `battery_capacity` and `fast_charging`       |
| 5  | `display`   | Should split into `screen_size`, `resolution`, `refresh_rate`  |
| 6  | `camera`    | Should split into `num_rear_cameras` and `num_front_cameras`   |
| 7  | `card`      | Should split into `extended_memory_available` and `extended_upto` |

---

## 🛠️ Cleaning Pipeline

### Stage 1 → `cleaned_smartphone_data1.csv`
**Initial quality fixes** (1,020 → 982 records, 12 columns)

- Removed `₹` symbol and commas from `price`, converted to integer
- Added `index` column referencing original row numbers
- Identified rows with shifted/invalid data across `processor`, `ram`, `battery`, `display`, and `camera` columns
- Removed problematic rows (feature phones, iPod, and devices with severely misaligned data)
- Removed the Namotel phone with ₹99 price (accuracy issue)

### Stage 2 → `cleaned_smartphone_data2.csv`
**Brand extraction, processor & SIM splitting** (982 records, 20 columns)

- Extracted `brand_name` from `model` column (normalized to lowercase)
- Fixed brand name inconsistencies (e.g., unified "OPPO"/"Oppo" variations)
- Split `sim` column into boolean flags: `has_5g`, `has_nfc`, `has_ir_blaster`
- Split `processor` into: `processor_name`, `processor_brand`, `num_cores`, `processor_speed`

### Stage 3 → `cleaned_smartphone_data3.csv`
**RAM, storage & battery splitting** (980 records, 24 columns)

- Split `ram` into `ram_capacity` and `internal_storage`
- Split `battery` into `battery_capacity` and `fast_charging`
- Handled edge cases where fast charging info was missing

### Stage 4 → `cleaned_smartphone_data4.csv`
**Display & camera splitting** (980 records, 29 columns)

- Split `display` into `screen_size`, `resolution`, and `refresh_rate`
- Parsed `camera` to extract `num_rear_cameras` and `num_front_cameras`
- Handled foldable phones and unusual camera configurations

### Stage 5 → `cleaned_smartphone_data5.csv`
**Memory card & OS cleanup — Final dataset** (980 records, 31 columns)

- Split `card` into `extended_memory_available` (boolean) and `extended_upto`
- Normalized `os` column (cleaned version names, removed extraneous Bluetooth/FM info)
- Final validation and export

---

## 🧰 Technologies Used

| Tool             | Purpose                                    |
| ---------------- | ------------------------------------------ |
| **Python 3**     | Programming language                       |
| **Pandas**       | Data manipulation and cleaning             |
| **NumPy**        | Numerical operations                       |
| **Jupyter Notebook** | Interactive development environment    |

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy jupyter
```

### Run the Notebook

```bash
jupyter notebook .ipynb
```

> **Note:** The notebook uses an absolute file path to read the source CSV. Update the path in the `pd.read_csv()` call if you move the project to a different directory.

---

## 📈 Key Statistics

| Metric                          | Value     |
| ------------------------------- | --------- |
| Records removed (invalid)       | ~40       |
| Quality issues fixed            | 20        |
| Tidiness issues resolved        | 7         |
| New columns created             | 20        |
| Price range (cleaned)           | ₹958 – ₹1,69,000 |
| Rating range                    | 60 – 89   |
| Brands in dataset               | 30+       |
| Missing ratings                 | ~14%      |

---

## 📝 Key Observations

- **Data shifting** was the most complex issue — feature phones and non-standard devices had their column values shifted by 1–3 positions, requiring careful row-by-row correction or removal.
- **Foldable phones** (e.g., Vivo X Fold, Oppo Find N2) had display and camera info in unexpected columns due to additional specifications.
- The dataset covers a wide range from basic feature phones (₹958) to premium flagships (₹1,69,000), making it useful for market segmentation analysis.

---

## 📄 License

This project is for educational and analytical purposes. The raw dataset is sourced from publicly available smartphone specifications data.
