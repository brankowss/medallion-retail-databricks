 # Setup & Execution Guide

Follow these steps to deploy and run the pipeline in Databricks.

## 1. GitHub Connection
1. In Databricks, go to `User Settings` → `Linked Accounts`.
2. Connect via **Personal Access Token (PAT)**.

## 2. Clone Repository
1. Go to `Workspace` → `Repos` → `Add Repo`.
2. Paste this URL: `[YOUR_REPO_URL]` and clone.

## 3. Data Preparation
1. Ensure the `datasets/` folder with raw CSV files exists in the repo.  
2. If you move CSVs to a different path, update the variables in `init_lakehouse.ipynb`.

## 4. Deployment (Run Pipeline)
1. Open the **`run_all_pipeline.ipynb`** notebook in the root folder.
2. Click **Run All** to execute the entire pipeline.

## 5. Verification
- Check the `workspace.gold` database for the final tables.
- Review the **8 Tests** results in the `Final Validation` section of the notebook.
