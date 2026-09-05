# 99 Data Shop

99 Data Shop is a Python notebook that combines production planning, manpower
analysis, muster processing, and cannibalization reporting tools in one
interactive workspace.

The notebook uses forms, dropdown menus, file uploads, and downloadable reports
to help users work with production data without editing the underlying Python
code.

## Notebook functions

### 1. Production Hours

The Production Hours section estimates the labor hours required to complete
work for different equipment or band types.

Supported options include:

- LBT
- Band 4
- Band 5/6
- Band 7
- Band 8
- Band 9/10

After the user selects an option, the notebook displays the fields required for
that calculation. Depending on the selected band, these fields can include:

- Number of benches
- Number of shifts
- Production target
- Month

The entered values are passed to a trained prediction model, which returns an
estimated number of production hours.

### 2. Manpower Throughput

The Manpower Throughput section estimates production capacity based on
available personnel.

The user enters the average number of people available, and the notebook uses a
trained capacity model to calculate the expected throughput. Results can be
cleared so another value can be entered and calculated.

### 3. Muster

The Muster section cleans, combines, and categorizes muster reports.

It is designed to:

- Accept uploaded muster workbooks
- Extract workbooks from an uploaded ZIP file
- Identify and use the latest corrected copy of a report
- Standardize report dates and worksheet data
- Combine multiple cleaned reports into one workbook
- Categorize muster records with a trained model
- Calculate average counts by category

Muster files should cover no more than one year, and files from different years
should not be mixed in the same upload.

The section can generate:

- `combined_cleaned_muster.xlsx`
- `categorized_muster.xlsx`
- `avg_category_count.xlsx`

### 4. Cannibalization

The Cannibalization section creates source lists and part counts from
cannibalization report data.

Supported gear types include:

- 910
- LBT
- UEU

The tool uses a ZIP file containing cannibalization reports, an uploaded AWP
list, and reference data to:

- Read and organize report files
- Match part numbers against reference dictionaries
- Cross-reference parts and equipment data
- Count matching parts
- Consolidate the results into an Excel report

The expected report archive is named `cann_files.zip`.

## Development functions

The notebook also includes development cells used to prepare data and test new
models.

### Midband cannibalization processing

This function reads midband parts data and reference dictionaries, then
organizes the results for cannibalization analysis.

### Distribution model

This function trains an experimental prediction model from an Excel dataset. It
compares actual and predicted values, displays a chart, saves the trained model,
and allows the user to enter a count for a sample prediction.

### Cleanup and notebook repair

Maintenance cells are included for clearing temporary Colab files and repairing
the notebook's Python environment. These cells are intended for troubleshooting
and are not part of the normal workflow.

## How the notebook works

The notebook is organized into separate sections for each tool. Users can run
only the section they need.

In general, each section follows this process:

1. Run the section's main code cell.
2. Wait for its controls to appear.
3. Select the appropriate equipment or report type.
4. Enter values or upload the requested files.
5. Run the calculation or processing function.
6. Review or download the generated results.

The notebook downloads the trained models and reference files needed by its
main tools when those sections are initialized.

## Platform

99 Data Shop was designed as a Google Colab notebook and uses Colab's upload,
download, and interactive display functions. For the intended experience, open
`99.ipynb` in Google Colab and run the section you want to use.

The notebook uses Python libraries including pandas, NumPy, scikit-learn,
Joblib, ipywidgets, matplotlib, requests, and openpyxl.
