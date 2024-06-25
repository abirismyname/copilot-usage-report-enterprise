# Copilot Usage Report - Enterprise Level
Export the Copilot seat assignments for an Enterprise that are currently being billed

> Note: This Action uses the [List all Copilot seat assignments for an Enterprise](https://docs.github.com/en/rest/copilot/copilot-user-management?apiVersion=2022-11-28#list-all-copilot-seat-assignments-for-an-enterprise), which is in public Beta and subject to change

## PAT Token
Create a Classic personal access tokens with `read:enterprise` scope.

Pass this token as an input to the action - GITHUB_TOKEN


## Action in workflow

Include the copilot-usage-report action in your workflow. 

**1. Sample workflow 1: Export to CSV**

```
    name: Copilot Usage Report export to CSV 

    on:
      workflow_dispatch:

    jobs:
      first-job:
        runs-on: ubuntu-latest
        
        steps:
        - name: Copilot usage
            uses: copilot-usage-report-enterprise@main
            with:        
            GITHUB_TOKEN: ${{secrets.ENT_TOKEN}}
            ent_name: 'octodemo'
            file_path: data/Copilot-Usage-Report.csv
        
        - name: Upload Copilot Usage Report
            uses: actions/upload-artifact@v3
            with:
            name: Copilot Usage Report
            path: data/Copilot-Usage-Report.csv      
```

**1. Sample workflow 2: Export to JSON**

```
    name: Copilot Usage Report export to JSON

    on:
      workflow_dispatch:

    jobs:
      first-job:
        runs-on: ubuntu-latest
        
        steps:
        - name: Copilot usage
            uses: copilot-usage-report-enterprise@main
            with:        
            GITHUB_TOKEN: ${{secrets.ENT_TOKEN}}
            ent_name: 'octodemo'
            file_path: data/Copilot-Usage-Report.json
        
        - name: Upload Copilot Usage Report
            uses: actions/upload-artifact@v3
            with:
            name: Copilot Usage Report
            path: data/Copilot-Usage-Report.json      
```

## Parameters

| Name                           | Required  | Description                                                           |
|--------------------------------|------------|----------------------------------------------------------------------|
| GITHUB_TOKEN                 | Yes | PAT Token for access    |
| ent_name                       | Yes | GitHub Organization Name                                      |
| file_path                       | Yes | CSV or JSON file path                                   |

## Exported Fields
Following fields are included in the Copilot Usage Report
- User
- Created At
- Updated At
- Last Acivity At
- Last Acivity Editor
- Pending Cancellation Date
- Team

## Report
Copilot usage report is added as a build artifact in the workflow. You can download the report from the workflow run page.

# License

The scripts and documentation in this project are released under the [MIT License](./LICENSE)
