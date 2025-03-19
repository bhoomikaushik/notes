# SRE TRAINING (DAY 21) - NUMPY, PANDAS & SQLALCHEMY

## 1. Introduction to NumPy
NumPy is a powerful numerical computing library in Python that provides support for large, multi-dimensional arrays and matrices, along with a collection of mathematical functions to operate on these arrays.

## 2. Creating NumPy Arrays
```python
import numpy as np

# Creating a 1D array
arr1 = np.array([1, 2, 3, 4, 5])
print("1D Array:", arr1)

# Creating a 2D array
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print("2D Array:\n", arr2)
```

## 3. Array Operations
```python
# Basic arithmetic operations
arr = np.array([10, 20, 30, 40])
print("Addition:", arr + 5)
print("Multiplication:", arr * 2)
```

## 4. Indexing and Slicing
```python
arr = np.array([10, 20, 30, 40, 50])
print("Element at index 2:", arr[2])
print("Sliced array:", arr[1:4])
```

## 5. Reshaping Arrays
```python
arr = np.arange(1, 10)
reshaped_arr = arr.reshape(3, 3)
print("Reshaped 3x3 Array:\n", reshaped_arr)
```

## 6. Statistical Functions
```python
arr = np.array([10, 20, 30, 40, 50])
print("Mean:", np.mean(arr))
print("Standard Deviation:", np.std(arr))
print("Sum:", np.sum(arr))
```

## 7. Working with Excel Files using Pandas
Pandas provides an easy interface to read and modify Excel files.

### 7.1 Reading an Excel File
```python
import pandas as pd

# Reading an Excel file
excel_data = pd.read_excel("data.xlsx")
print("Excel Data:\n", excel_data.head())
```

### 7.2 Editing and Saving an Excel File
```python
# Modifying a column
excel_data["NewColumn"] = excel_data["ExistingColumn"] * 2

# Saving the modified file
excel_data.to_excel("modified_data.xlsx", index=False)
print("Excel file updated and saved!")
```

# Setting Up SQLite with SQLAlchemy in WSL & Windows

## 1️⃣ Creating a Database Directory
To keep things organized, create a dedicated directory for your database in WSL:
```bash
mkdir -p ~/databases
```
This ensures the `databases` folder exists in your home directory.

## 2️⃣ Moving the SQLite Database File
If you already have a database file (`data.db`), move it to this directory:
```bash
mv /home/your_user/basic-module/data.db ~/databases/
```

## 3️⃣ Verifying the Database File
Check if the database file exists and has the correct permissions:
```bash
ls -l ~/databases/data.db
```
If you face permission issues, run:
```bash
chmod 777 ~/databases/data.db
```

## 4️⃣ Navigating to the Project Directory
Change to the directory where your Python script is stored:
```bash
cd ~/alchemy_practice2
```

## 5️⃣ Installing Required Packages
Ensure Python and SQLAlchemy are installed:
```bash
sudo apt update
sudo apt install python3-pip
pip3 install sqlalchemy
```

## 6️⃣ Writing the Python Script
Create a Python script (e.g., `main.py`) to connect SQLAlchemy with SQLite:
```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

# Define database path
db_path = "sqlite:////home/bhoomikaushik/databases/mydatabase.db"
engine = create_engine(db_path, echo=True)

SessionLocal = sessionmaker(bind=engine)
Base = declarative_base()

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True, index=True)
    name = Column(String, index=True)

Base.metadata.create_all(engine)
```
### 📝 Explanation of the Script
- **Database Path:** The database is stored at `/home/bhoomikaushik/databases/mydatabase.db`.
- **Engine Creation:** `create_engine()` initializes a connection to the SQLite database.
- **Session:** `SessionLocal = sessionmaker(bind=engine)` creates a session for interacting with the database.
- **Base Class:** `Base = declarative_base()` is the base class for defining table structures.
- **User Table:**
  - `id`: Primary key (Integer, unique for each user).
  - `name`: String field with an index for optimized queries.
- **Table Creation:** `Base.metadata.create_all(engine)` ensures the `users` table is created in the database.

## 7️⃣ Running the Python Script
Execute the script to create the database and table:
```bash
python3 main.py
```

## 8️⃣ Accessing SQLite Database in WSL
Open SQLite CLI and check the tables:
```bash
sqlite3 ~/databases/mydatabase.db
.tables
```
To view user records:
```sql
SELECT * FROM users;
```

## 9️⃣ Accessing SQLite Database from Windows
1. **Using Windows Command Prompt**
   ```sh
   sqlite3 C:\\Users\\bhoomikaushik\\alchemy_practice2\\mydatabase.db
   ```

   
3. **Using DB Browser for SQLite**
   - Download [DB Browser](https://sqlitebrowser.org/dl/)
   - Accessed at `C:\Users\bhoomikaushik\alchemy_practice2\mydatabase.db`


## 🔟 Exiting SQLite CLI
To exit SQLite:
```sql
.exit
```

## ✅ Summary
- Created a **database directory** (`~/databases/`)
- Installed **SQLAlchemy**
- Wrote a Python script to **create a table**
- **Ran the script** and inserted data
- Accessed SQLite from both **WSL & Windows**
- Explained how the script works


# Pandas Setup and Execution Guide

## Prerequisites

- Python installed (check using `python3 --version`)
- Virtual Environment support (`venv`)
- VS Code, Jupyter Notebook, or Terminal access

## 1️⃣ Setting Up a Virtual Environment

Run the following commands:

```bash
# Navigate to your project directory
cd /mnt/c/Users/bhoomikaushik/pandas

# Create a virtual environment
python3 -m venv venv

# Activate the virtual environment
source venv/bin/activate
```


## 2️⃣ Installing Pandas

```bash
pip install pandas
```

Check if Pandas is installed correctly:

```bash
python -c "import pandas as pd; print(pd.__version__)"
```

