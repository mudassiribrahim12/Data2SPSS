# Data2SPSS

**An interactive R-Shiny web application for converting data files to SPSS and other formats**

## Overview

Data2SPSS is a free, web-based R-Shiny application that automates the conversion of various data formats into SPSS-ready files and enables bidirectional conversion between multiple statistical software formats. The tool eliminates the need for manual data preparation, requires no software installation or programming skills, and is completely free to use.

Researchers across biomedical, health, social, and behavioral sciences often struggle with data preparation for SPSS Statistics. Common problems include:
- Categorical variables not recognized correctly
- Value labels lost during transfer
- Variable names with special characters causing errors
- Character encoding issues

Data2SPSS solves these problems by automatically cleaning variable names, detecting variable types, generating value labels, and handling character encoding.

## Features

### Supported Input Formats
- CSV (comma-separated values)
- TSV (tab-separated values)
- TXT (plain text)
- Microsoft Excel (.xlsx, .xls)
- Stata (.dta)
- SPSS (.sav)
- SAS (.sas7bdat)
- RData (.rdata)

### Supported Output Formats
- SPSS (.sav)
- CSV
- Excel (.xlsx)
- Stata (.dta)
- SAS (.sas7bdat)
- TSV
- TXT
- RData (.rdata)

### Key Features
- **Intelligent variable type detection**: Automatically distinguishes between continuous and categorical variables
- **Automatic value label preservation**: Maintains existing labels from Stata and SPSS files
- **Variable name cleaning**: Removes spaces, special characters, and ensures SPSS compatibility
- **Character encoding handling**: Converts all text to UTF-8 to prevent corruption
- **Bidirectional conversion**: Convert any loaded file to any supported format
- **Dark/Light theme toggle**: User preference saved locally
- **Responsive design**: Works on desktop, tablet, and mobile devices

## Live Application

Access the live application at: [https://newappstesting.shinyapps.io/Data2SPSS/]

## Installation and Local Setup

### Prerequisites
- R version 4.4 or higher
- RStudio (recommended) or any R environment

### Steps to Run Locally

1. **Download app.file from the GitHub repository**

Access the source code at: [https://github.com/mudassiribrahim12/Data2SPSS/blob/main/app.R]

2. **Install required R packages**
   
   Open R or RStudio and run:
   ```r
   # Install required packages
   install.packages(c(
     "shiny",
     "shinythemes",
     "readxl",
     "readr",
     "haven",
     "foreign",
     "rio",
     "DT",
     "dplyr",
     "labelled",
     "purrr",
     "shinyjs",
     "writexl"
   ))
   ```

3. **Run the application**
   
   In R or RStudio:
   ```r
   # Navigate to the application directory
   setwd("path/to/Data2SPSS")
   
   # Run the app
   shiny::runApp()
   ```

   Or open the `app.R` file in RStudio and click "Run App".

### Deployment Options

#### ShinyApps.io (Free)
The easiest way to deploy publicly:
1. Create an account at [shinyapps.io](https://www.shinyapps.io/)
2. Install the `rsconnect` package: `install.packages("rsconnect")`
3. Deploy:
   ```r
   rsconnect::deployApp("path/to/Data2SPSS")
   ```

#### Institutional Server
For universities or organizations, deploy on your own server using:
- **Shiny Server** (open source)
- **RStudio Connect** (commercial)
- **Docker** containerization

## Usage Guide

### Basic Workflow

1. **Open the application** in your web browser
2. **Navigate to the Data Converter tab**
3. **Click "Choose Data File"** and select your data file
4. **Review the preview panels** to verify your data loaded correctly:
   - Data Preview: First several rows of the dataset
   - Data Structure: Variable types and unique values
   - Variable Analysis: How the tool will handle each variable
5. **Click "Convert to SPSS format"**
6. **Review the SPSS Metadata panel** to confirm variable names, labels, and value labels
7. **Enter a filename** and click "Download SPSS File"

### Final Steps in SPSS Statistics

After downloading and opening the file in SPSS Statistics:

1. **Navigate to Variable View** (usually at the bottom of the SPSS window)
2. **Locate the "Measure" column**
3. **Change measure type for categorical variables:**
   - **Nominal**: Categories with no natural order (e.g., gender, treatment group)
   - **Ordinal**: Categories with meaningful order (e.g., education level, Likert scales)

> **Important**: If categorical variables are left as "Scale", SPSS may treat them as continuous numbers in statistical procedures, leading to incorrect results.

### Exporting to Other Formats

1. **Load your data** in the Data Converter tab
2. **Navigate to the Export to Other Formats tab**
3. **Select your desired output format** from the dropdown menu
4. **Review the preview** to verify the conversion
5. **Click "Download Converted File"**

## How It Works

### Variable Type Detection

The tool uses multiple criteria to distinguish between continuous and categorical variables:

- **Value labels present** → Categorical
- **Factor type** → Categorical
- **Unique values ≤ 50** → Likely categorical
- **Contains decimals** → Likely continuous
- **Range > 1000** → Likely continuous

### Variable Name Cleaning

Variable names are automatically cleaned to meet SPSS requirements:
- Spaces are removed
- Special characters are eliminated
- Names are truncated to 64 characters
- Names starting with numbers are prefixed with a letter
- Duplicate names are made unique by appending numbers

### Value Label Assignment

- **Text categorical variables**: Converted to numbers (1, 2, 3, ...) with corresponding value labels
- **Continuous variables**: Each observation assigned both a value and a label mirroring that value (e.g., 26 → "26")
- **Pre-labeled variables**: Existing labels from Stata or SPSS are preserved

## Technical Notes and Limitations

### Current Limitations

1. **Nominal vs. Ordinal**: The tool does not distinguish between nominal and ordinal categorical variables. Users must make this distinction when adjusting measure types in SPSS.

2. **Missing Values**: User-defined missing value definitions from source files are not propagated. Use SPSS to set missing values after import.

3. **File Size**: Performance depends on system resources. Very large datasets may require longer processing times.

4. **Internet Connection**: The web version requires an internet connection. Run locally for offline use.

### Performance Considerations

- For typical research datasets (up to tens of thousands of rows), processing is nearly instantaneous
- Large datasets with hundreds of thousands of rows may require more time
- For optimal performance with large files, run the application locally

## Example Dataset

An example dataset is available for testing:
[https://archive.org/download/data-2-spss-example-dataset/Data2SPSS%20Example%20dataset.xlsx]

## Project Structure

```
Data2SPSS/
├── app.R              # Main application file
├── README.md          # This file
├── LICENSE            # MIT License
└── .gitignore         # Git ignore file
```

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Priorities
- Adding support for additional file formats
- Implementing automated detection of ordinal variables
- Incorporating custom missing value handling
- Improving performance for very large datasets

## License

This project is licensed under the MIT License - see the LICENSE [https://github.com/mudassiribrahim12/Data2SPSS/blob/main/LICENSE] file for details.

## Citation

If you use Data2SPSS in your research, please cite:

```bibtex
@software{Ibrahim_Data2SPSS_2025,
  author = {Ibrahim, Mudasir Mohammed},
  title = {Data2SPSS: An interactive R-Shiny web application for converting data files to SPSS and other formats},
  year = {2026},
  url = [https://github.com/mudassiribrahim12/Data2SPSS]
}
```

## Contact

**Author:** Mudasir Mohammed Ibrahim  
**Affiliation:** Department of Internal Medicine (M3), Tamale Teaching Hospital, Tamale, Ghana  
**Email:** [mudassiribrahim30@gmail.com](mailto:mudassiribrahim30@gmail.com)

### Academic Profiles
- [ResearchGate] [https://www.researchgate.net/profile/Mudasir-Ibrahim]
- [Google Scholar] [https://scholar.google.com/citations?user=xEFzAvgAAAAJ&hl=en]
- [ORCID][https://orcid.org/0000-0002-9049-8222]

## Acknowledgments

Data2SPSS was built using several R packages including:
- [shiny](https://shiny.rstudio.com/) - Web application framework
- [shinydashboard](https://rstudio.github.io/shinydashboard/) - Dashboard layout
- [haven](https://haven.tidyverse.org/) - Import/export SPSS, Stata, and SAS files
- [readxl](https://readxl.tidyverse.org/) - Excel file import
- [writexl](https://docs.ropensci.org/writexl/) - Excel file export
- [DT](https://rstudio.github.io/DT/) - Interactive tables

## Support

For issues, questions, suggestions, or permission to deploy on personal servers:
- Contact the author via email: mudassiribrahim30@gmail.com
---

**Data2SPSS: Making data preparation faster, easier, and more reliable for researchers worldwide.**
