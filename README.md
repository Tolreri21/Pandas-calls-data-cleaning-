# Customer Call List Data Cleaning

This project involves cleaning a customer call list dataset using Python, Pandas, and Jupyter Notebook. The dataset, stored in `Customer Call List.xlsx`, contains customer information such as names, phone numbers, addresses, and contact preferences. The goal is to clean and prepare the data for further use by addressing duplicates, inconsistencies, and missing values.

## Dataset
- **File**: `Customer Call List.xlsx`
- **Columns**:
  - `CustomerID`: Unique identifier for each customer
  - `First_Name`: Customer's first name
  - `Last_Name`: Customer's last name
  - `Phone_Number`: Customer's phone number
  - `Address`: Customer's address
  - `Paying Customer`: Indicates if the customer is paying (Y/Yes, N/No, or N/a)
  - `Do_Not_Contact`: Indicates if the customer should not be contacted (Y/Yes, N/No, or NaN)
  - `Not_Useful_Column`: A redundant column with no meaningful data

## Cleaning Process
The following data cleaning operations were performed in the Jupyter Notebook (`Untitled2.ipynb`):

1. **Load the Dataset**:
   - Imported the Excel file into a Pandas DataFrame using `pd.read_excel()`.

2. **Remove Duplicates**:
   - Eliminated duplicate rows using `df.drop_duplicates(inplace=True)`, reducing the dataset from 21 to 20 rows by removing a duplicate entry for Anakin Skywalker.

3. **Drop Unnecessary Column**:
   - Removed the `Not_Useful_Column` as it contained no valuable information using `df.drop(columns="Not_Useful_Column", inplace=True)`.

4. **Clean Last Names**:
   - Stripped unwanted characters (e.g., `...`, `_`, `/`) from the `Last_Name` column using `str.strip()` to standardize names (e.g., `...Potter` → `Potter`, `Flenderson_` → `Flenderson`).

5. **Standardize Phone Numbers**:
   - Removed non-numeric characters (e.g., `/`, `|`) from the `Phone_Number` column using `str.replace()` with a regular expression.
   - Formatted phone numbers to a consistent `XXX-XXX-XXXX` format using a custom function and `apply()`.
   - Replaced invalid entries (`N/a`, `NaN`) with empty strings for further processing.

6. **Split Address into Columns**:
   - Split the `Address` column into `Street Address`, `State`, and `Zipcode` using `str.split(expand=True)`.
   - Handled missing or inconsistent address components by filling with empty strings.

7. **Standardize Paying Customer and Do_Not_Contact**:
   - Replaced `Yes` with `Y` and `No` with `N` in the `Paying Customer` and `Do_Not_Contact` columns using `str.replace()` for consistency.
   - Replaced `N/a` in `Paying Customer` with `N` to align with the binary format.

8. **Remove Do_Not_Contact Customers**:
   - Dropped rows where `Do_Not_Contact` was `Y` to exclude customers who should not be contacted, reducing the dataset to 16 rows.

9. **Handle Missing Do_Not_Contact Values**:
   - Replaced empty or `NaN` values in `Do_Not_Contact` with `N` to assume contact is allowed unless specified otherwise.

10. **Remove Rows Without Phone Numbers**:
    - Dropped rows where `Phone_Number` was empty or missing using `df.dropna(subset=["Phone_Number"], inplace=True)`, resulting in a final dataset of 10 rows.

11. **Remove Zipcode Column**:
    - Dropped the `Zipcode` column as it was mostly empty or irrelevant using `df.drop(columns="Zipcode", inplace=True)`.

12. **Reset Index**:
    - Reset the DataFrame index to ensure consecutive numbering after row deletions using `df.reset_index(drop=True)`.

## Final Dataset
The cleaned dataset contains 10 rows and 8 columns:
- `CustomerID`
- `First_Name`
- `Last_Name`
- `Phone_Number`
- `Paying Customer`
- `Do_Not_Contact`
- `Street Address`
- `State`

All phone numbers are formatted consistently, names are cleaned, and only customers who can be contacted with valid phone numbers remain.

## Tools Used
- **Python**: Programming language
- **Pandas**: Data manipulation and cleaning
- **Jupyter Notebook**: Interactive environment for coding and visualization

## How to Run
1. Ensure Python and Pandas are installed (`pip install pandas openpyxl`).
2. Place `Customer Call List.xlsx` in the specified directory (`C:\Users\TOLK\Downloads\` or update the path in the notebook).
3. Open `Untitled2.ipynb` in Jupyter Notebook.
4. Run all cells sequentially to replicate the cleaning process.

## Output
The final cleaned DataFrame is displayed in the notebook and can be exported to a new file (e.g., CSV or Excel) if needed by adding `df.to_csv('cleaned_customer_list.csv')`.

## GitHub Usage
To use this repository:
1. Clone the repository to your local machine.
2. Ensure the required dependencies (`pandas`, `openpyxl`) are installed.
3. Update the file path in `Untitled2.ipynb` to point to your local `Customer Call List.xlsx`.
4. Run the notebook to perform the data cleaning.
5. The cleaned dataset can be saved or used for further analysis.
