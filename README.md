# Employee Salary Prediction with PySpark

A Big Data Processing school project (EGT305) that builds an end-to-end ML pipeline to predict employee salaries using PySpark.

### Project Overview
- **Course:** EGT305 - Big Data Processing Platforms & Applications
- **Assignment:** AY2026S1
- **Objective:** Predict employee salary using PySpark ML models
- **Stack:** PySpark (Spark SQL + Spark ML), Python, Matplotlib

---

### Project Structure
```
Data Processing Project/
├── EGT305_Assignment.ipynb    # Main notebook (all code)
├── EGT305_Report.pdf          # Written report
├── EGT305_Pipeline.pdf        # Pipeline documentation
├── EGT305_Presentation.pptx   # Presentation deck
├── Employee_dataset.csv       # Employee data (input)
├── Employee_salaries.csv      # Salary data (input)
├── requirements.txt           # Python dependencies
├── LICENSE                    # MIT license
└── README.md                  # This file
```

---

### Prerequisites

#### Python Environment
- Python 3.8 or higher
- pip (Python package manager)

#### Java (Required for PySpark)
PySpark requires Java to run. Install OpenJDK 11:

```bash
# Download and install OpenJDK 11 from:
# https://adoptium.net/temurin/releases/?version=11

# Or using Chocolatey:
choco install temurin11
```

---

### Local Setup (VS Code - Windows)

1. **Open PowerShell and navigate to project:**
```powershell
cd "path\to\Data Processing Project"
```

2. **Create virtual environment:**
```powershell
python -m venv venv
```

3. **Activate virtual environment:**
```powershell
venv\Scripts\activate
```

4. **Install dependencies:**
```powershell
# Install required dependencies
pip install -r requirements.txt
```

5. **Open in VS Code:**
   - Install **Python** extension
   - Install **Jupyter** extension
   - Open the project folder
   - Open `EGT305_Assignment.ipynb`

---

### Google Colab Setup

1. Upload `EGT305_Assignment.ipynb` to Google Colab
2. Upload both CSV files to Colab's file storage
3. The notebook will auto-install dependencies

---

### Dataset Description

**Employee_dataset.csv:**

| Column | Type | Description |
|--------|------|-------------|
| jobId | String | Unique job identifier |
| companyId | String | Company identifier |
| jobRole | String | Job title (CEO, CFO, JUNIOR, etc.) |
| education | String | Education level (HIGH_SCHOOL, BACHELORS, MASTERS, DOCTORAL) |
| major | String | Field of study |
| industry | String | Industry sector |
| yearsExperience | Integer | Years of work experience |
| distanceFromCBD | Integer | Distance from Central Business District (km) |

**Employee_salaries.csv:**

| Column | Type | Description |
|--------|------|-------------|
| jobId | String | Unique job identifier |
| salaryInThousands | Integer | Annual salary in SGD (thousands) |

---

### Data Cleaning Steps

The notebook performs the following cleaning operations:

1. **Remove duplicate observations** - Drop duplicate jobId entries
2. **Filter invalid entries** - Remove rows with jobRole = "SCAMMER"
3. **Handle missing data:**
   - Drop rows with nulls in critical columns (jobId, companyId, jobRole)
   - Fill numeric nulls with median values
   - Fill categorical nulls with 'UNKNOWN' or 'NONE'
4. **Fix outliers** - Remove values outside IQR bounds for distanceFromCBD
5. **Merge datasets** - Inner join on jobId
6. **Remove salary outliers** - Remove extreme salary values using IQR method

---

### ML Models Implemented

| Model | Type | When to Use |
|-------|------|-------------|
| Linear Regression | Baseline | When interpretability is key |
| Random Forest | Ensemble | For feature importance analysis |
| GBT Regressor | Boosting | For maximum predictive performance |

---

### Running the Notebook

**Local (Jupyter):**
```powershell
# Start Jupyter Notebook
jupyter notebook

# Or JupyterLab
jupyter lab
```

Then navigate to `EGT305_Assignment.ipynb` and run all cells.

---

### Troubleshooting

**"JAVA_HOME not set" error:**
```powershell
# PowerShell
$env:JAVA_HOME = "C:\Program Files\Eclipse Adoptium\jdk-11.x.x.x"

# Command Prompt
set JAVA_HOME=C:\Program Files\Eclipse Adoptium\jdk-11.x.x.x
```

**PySpark version issues:**
```powershell
pip install pyspark==3.4.1
```

**Memory errors:**
- Reduce `spark.sql.shuffle.partitions` in the notebook
- Or increase Spark driver memory:
```python
spark = SparkSession.builder.config("spark.driver.memory", "4g").getOrCreate()
```

**pyspark.pandas import error:**
- Ensure you have PySpark 3.2+ and pyarrow installed
```powershell
pip install pyspark>=3.2 pyarrow>=12.0.0
```

**"PySpark does not yet fully support pandas >= 3.0.0" warning:**
- PySpark 4.x does not yet fully support pandas 3.x. Install pandas < 3.0.0 (the notebook
  suppresses this FutureWarning automatically):
```powershell
pip install "pandas>=2.2,<3"
```

**PySpark pandas plotting error (plotly required):**
- PySpark 4.x uses plotly as the default plotting backend
```powershell
pip install plotly>=5.0.0
```

---

### Resources

- [PySpark Documentation](https://spark.apache.org/docs/latest/api/python/)
- [PySpark ML Guide](https://spark.apache.org/docs/latest/ml-guide.html)
- [Download OpenJDK](https://adoptium.net/)
- [Google Colab](https://colab.research.google.com/)

---

### License

This project is released under the [MIT License](LICENSE). Originally created for educational purposes.
