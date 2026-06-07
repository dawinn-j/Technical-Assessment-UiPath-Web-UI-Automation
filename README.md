# Technical Assessment: UiPath Web UI Automation

UiPath Web UI Automation for Technical Assessment on [DemoQA] (https://demoqa.com/automation-practice-form) — includes test data generation, form validation, and result logging.

---

## Prerequisites

| Requirement | Version |
|---|---|
| UiPath Studio | 2026.0.194 STS |
| UiPath.UIAutomation.Activities | ≥ 24.10 |
| UiPath.System.Activities | ≥ 24.10 |
| UiPath.Excel.Activities | ≥ 2.22 |
| Google Chrome | Latest |
| UiPath Chrome Extension | Enabled |

> Install the Chrome extension via **UiPath Studio → Tools → UiPath Extensions → Chrome**

---

## How to Run

1. Clone the repo and open the folder in UiPath Studio
2. Place test data in `Data/Input/Input_Mockup_Data.xlsx`
3. Open `Main.xaml` and press **Run File**
4. Results will be saved to `Data/Output/Output_Report.xlsx`

---

## Assumptions and Known Limitations

**Assumptions**
- Internet connection is available and DemoQA is accessible
- Test data in Excel follows the column format defined in `Input_Mockup_Data.xlsx`
- Chrome browser is installed and the UiPath extension is enabled

**Known Limitations**
- Only runs on Windows (UiPath Studio limitation)

---

## Design Notes

### Selector Strategy

The automation is split into two sub-tasks:

- **01_Get_Input_File** — Reads the Excel input file from Sheet1 into a DataTable for processing
- **02_Fill_Practice_Form** — Iterates through each row in the DataTable, validates the data against the following rules, then fills the DemoQA form and logs the result:
  - Email must match a valid format
  - Mobile number must contain 10 digits only
  - First Name and Last Name must not be empty

Only rows passing all validations are submitted to the form. Each result is recorded to the output file.

### Error Handling Approach

- Each row is wrapped in a Try/Catch block. If an unexpected error occurs, the error message is logged and the automation continues to the next row.

---

## Folder Structure

```
├── Data/
│   └── Input/
│   ├── Input_Mockup_Data.xlsx      # Mock input test data
│   └── Output/
│       └── Output_Report.xlsx      # Results after a run
├── Exceptions_Screenshots/         # Auto-saved screenshots on failure
├── Framework/                      # Reusable workflows
├── Process/                        # Core process workflows
│   ├── 01_Get_Input_File.xaml
│   └── 02_Fill_Practice_Form.xaml
├── Main.xaml                       # Entry point
├── project.json
└── README.md
```

---

## Sample Data

| File | Description |
|---|---|
| `Data/Input/Input_Mockup_Data.xlsx` | Mock data for testing |
| `Data/Output/Output_Report.xlsx` | Expected output after running with sample input |