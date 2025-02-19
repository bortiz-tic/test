<div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/66fb2886-0a66-41a8-abb3-a1d08296c19f" alt="Iowa Clinic Logo Green" width="500"/>
</div>

# Data Pipeline - ETL for Coder Scorecard

## Overview
This project is a data pipeline that automates the extraction, transformation, and loading (ETL) of data from multiple sources. The pipeline processes data from:
- Ingenious Med
- PrecisionBI (PBI)

## ETL Location
The ETL processes are located in the following directory:
`T:\Analytics\Automation\Python Modules\Production\Rev Cycle Scorecard\CoderScorecard`

## File Structure and Description
```bash
project/
├── pipeline
│   ├── PipelineStep1
│       ├── output
│           ├── output
│           ├── FinanceScorecardPipelineStep1.py
│   ├── PipelineStep2
│       ├── FinanceScorecardPipelineStep2.py
│   ├── rev_cycle_coder_scorecard_pipeline.log
├── DDL
│   ├── rev_cycle_coder_scorecard_ddl.sql
├── xwalk
│   ├── finance_scorecard_coder_scorecard_xwalk_pipeline.py
│   ├── finance_scorecard_coder_scorecard_xwalk_pipeline.log
├── README.md
```

### pipeline
**PipelineStep1** contains a Python file that processes step 1 of the pipeline. The output subdirectory contains 2 CSV files that are passed to step 2 of the pipeline. **PipelineStep2** contains a Python file that processes step 2 of the pipeline.

### DDL
Directory that contains a SQL file that defined the data definition of the resultant tables of the pipeline.

### xwalk
The `finance_scorecard_coder_scorecard_xwalk_pipeline.py` file processes changes to the crosswalk. The `finance_scorecard_coder_scorecard_xwalk_pipeline.log` file logs the activities of the xwalk pipeline

## Pipeline Workflow

### Pipeline Steps (Overview)
1. **Crosswalk**: Every Friday at 4pm CST
2. **FinanceScorecardPipelineStep1**: Every Sunday at 12pm CST
3. **FinanceScorecardPipelineStep2**: Every Monday at 12pm CST

### Pipeline Steps (Detail)
1. **Crosswalk**:
     - If there are coders hired, then Shelly Kimmel replaces the following file, including ONLY the new coders names.
		- `T:\Revenue Cycle\Revenue Cycle Scorecard\Coder Scorecard\Weekly Update\crosswalk_users_names_TEMPLATE.xlsx`
2. **Data Ingestion (Step 1)**:
    - This step is executed on the Remove Destkop Task Automater every Sunday at 12:00pm.
    - This step executes the following .py file
		- `T:\Analytics\Automation\Python Modules\Production\Rev Cycle Scorecard\CoderScorecard\pipeline\PipelineStep1\FinanceScorecardPipelineStep1.py`
	- Step 1 Input
		- PBI Data
	- Step 1 Output
		- 2 csv files that are fed into step 2.
3. **Data Ingestion and transformation (Step 2):**
	- This step is executed every Monday at 12:00 pm. 
	- This step executes the following .py file
		- `T:\Analytics\Automation\Python Modules\Production\Rev Cycle Scorecard\CoderScorecard\pipeline\PipelineStep2\FinanceScorecardPipelineStep2.py`
	- Step 2 Input
		- The 2 csv files from step 1.
		- An Ingenious Med file that Shelly Kimmel places in `T:\Revenue Cycle\Revenue Cycle Scorecard\Coder Scorecard\Weekly Update` every Monday Morning. 
	- Step 2 Output
		- Finalized data that is loaded into `analytics_prod.revcycle.coder_scorecard`
  
## Prerequisites
Before running the pipeline, ensure the following are installed and configued:
- Python 3.8+
- Access to Analytics01 VM
- Permissions to read/write to the specified directories

## Installation
To set up the pipeline, follow these steps:
1. Clone the repository:
```bash
git clone <repo here>
```
2. Navigate to the project directory:
```bash
cd ./CoderScorecard
```

## Usage
To run the pipeline, execute the folliwng command:
```bash
python file.py
```

## Troubleshooting
What would be some potential troubleshooting situations and how would we fix them? Logging, libraries, permissions, etc?

## Contact Information
For questions or support, please contact:
- Analytics Email: AnalyticsRequest@iowaclinic.com
- IT: helpdesk@iowaclinic.com
