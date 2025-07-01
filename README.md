# Sprocket Data Cleaning Project

## Project Overview

This project is based on the **KPMG Data Analytics Virtual Internship** hosted on [**Forage**](https://www.theforage.com/dashboard), designed to simulate real-world tasks faced by analysts. The simulation is structured into three parts, and this report covers the **first phase**, which focuses on assessing and cleaning the data provided by the client.

---

### Client Background

Sprocket Central Pty Ltd is a trusted KPMG client that sells premium bicycles and cycling accessories aimed at a broad range of riders. To sharpen their marketing strategy, the company’s team is exploring ways to better understand their customer base through data.

They believe the customer datasets they've collected hold valuable insights that could help them tailor their marketing efforts, especially toward high-value customers. But before any meaningful analysis can happen, the data needs to be carefully reviewed and cleaned to ensure it's accurate, complete, and reliable.

---

## Project Goal

The goal of this phase is to identify all data quality issues in the provided datasets and take appropriate cleaning steps. The cleaning work is grouped under six core data quality dimensions:

* **Accuracy**
* **Consistency**
* **Completeness**
* **Relevancy**
* **Uniqueness**
* **Validity**

The result is a set of clean, analysis ready datasets that can confidently support the next steps in customer segmentation and marketing analysis.

---

## Datasets
- **Customer Demographics**
- **Transactions**
- **New Customer List**
- **Customer Address**

---

## 1. Accuracy

### Issue
- DOB `1843-12-21` for customer Jephthah Bachmann is likely an error.

### Action
- Corrected to `1943-12-21` (consistent with max observed age in dataset).
<img width="959" alt="image" src="https://github.com/user-attachments/assets/c973f865-063d-42fc-9380-1add55bcd7b5" />

---

## 2. Consistency

### Issues
- Gender formats inconsistent (`F`, `Femal`, `M`, `U`).
- Product first sold date format inconsistent.
- Gender `U` in New Customer List unclear.

### Actions
- Normalized gender: `F → Female`, `Femal`→ Female`, `M → Male`, `U → Unsure`.
- Standardized all date columns to `datetime` format.
- Changed `U` in gender to `Unsure`.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/1fe54057-614a-4d25-b230-f0b47dc23de3" />

<img width="960" alt="image" src="https://github.com/user-attachments/assets/16080e52-ce73-470b-ba74-15658cbb8c09" />

<img width="960" alt="image" src="https://github.com/user-attachments/assets/479d8a3f-39b8-4a62-897f-bf80b49587c8" />

---

## 3. Completeness

### Issues
- Customer Demographics: **1045** blanks (Last Name, DOB, Job Title, Tenure).
- Transactions: **1542** blanks (Online_order, Brand, Product_line, etc.).
- New Customer List: **152** blanks (Last Name, DOB, Job Title).

### Actions
- Filled `Last Name`, `Job Title` blanks with `'n/a'`.
- Filled `Tenure` with `0` (assumed to be in years).
- Filled categorical product info with `'n/a'` or `0` as needed.
- Left `DOB` blanks intact due to relevance to analysis.

<img width="958" alt="image" src="https://github.com/user-attachments/assets/28fc333f-5cfd-448f-86da-ffbc4394fce7" />


<img width="960" alt="Screenshot 2025-06-30 162629" src="https://github.com/user-attachments/assets/a3225810-519a-4b64-ba47-31b1863eecdd" />

---

## 4. Relevancy

### Issues
- Deceased customers present in Customer Demographics.
- Default column full of anonymous values.

### Actions
- Removed two deceased customers.
- Dropped the default column.

<img width="960" alt="image" src="https://github.com/user-attachments/assets/dfcd79b7-cf52-4623-a76a-d4680dcd8adf" />

---

## 5. Uniqueness

### Issue
- New Customer List had no unique identifier.

### Action
- Added a custom `Index` column for uniqueness.

<img width="960" alt="image" src="https://github.com/user-attachments/assets/4a43040a-5856-4408-873a-e6877bda1c35" />

---

## 6. Validity

### Issues
- Numerical fields in text format (columns `post code`, `property valuation`, `past 3 years purchases`).
- Inconsistent decimal precision in `Value` column.
- State abbreviations used inconsistently.

### Actions
- Converted the fields to numeric types.
- Standardized decimal places in `Value` column.
- Expanded all state abbreviations to full names.

<img width="960" alt="image" src="https://github.com/user-attachments/assets/6e0228b5-e8be-42fd-8d16-2df4dc905e7f" />


<img width="960" alt="image" src="https://github.com/user-attachments/assets/6b61e842-bb71-48da-b01b-00f370769407" />

---

## Enhancements

- Added `age` and `age_group` columns for segmentation.
- Ensured all datasets are analysis-ready and cleaned for business insight generation.

<img width="960" alt="image" src="https://github.com/user-attachments/assets/f941b69f-ab58-4346-81cb-bfde3d69b1c0" />


<img width="960" alt="image" src="https://github.com/user-attachments/assets/9150b602-5674-4df8-ad9b-8cbb40636f9d" />

---

## Recommendations

1. **Data Validation Rules:** Implement form-level and field-level validation at the point of entry.
2. **Automated Monitoring:** Introduce data quality monitoring tools to track missing values and anomalies.
3. **Standardized Templates:** Use controlled vocabularies and dropdowns during data entry to prevent format inconsistencies.
4. **Regular Audits:** Schedule periodic data quality audits to maintain a high standard of data integrity.
5. **Imputation Strategy:** Where possible, use statistical or ML-based imputation instead of nulls or placeholders.

