# 🛠️ Getting Started with Microsoft Fabric and dbt: Build a Sample Warehouse and Transform Data Natively

Microsoft Fabric now lets you build and transform data pipelines using **dbt**—all within the Fabric web experience. No external adapters, no CLI, no Airflow. Just SQL, a warehouse, and a streamlined UI.

This guide walks you through:
- Creating a sample Data Warehouse in Fabric
- Building a dbt item to transform your data
- Running and validating your models—all natively in Fabric

---

## ✅ Prerequisites
Before you begin, make sure you have:
- Access to a Microsoft Fabric workspace
- Contributor permissions in the workspace


---

## 🧱 Step 1: Create a Sample Data Warehouse
1. In your Fabric workspace, click **+ New** → **Sample Warehouse**.
2. Name your warehouse (e.g., `warehouse-test`) and choose a lakehouse or dataset to connect.
3. Sample data will be create that we will transform later in dbt

---

## 📦 Step 2: Create a dbt Item
1. Click **+ New** → **dbt project**.
2. Name your project (e.g., `dbt-project`) and select the warehouse you just created.
3. You’ll see the dbt interface with:
   - `Explorer (Left)`: Manage files and folders
   - `Main Panel (Center)`: Start building or import a dbt project
   - `Settings (Right)`: Configure schema and thread count
![dptPanel](dbtPanel.png)

---

## Step 3: Build Your dbt Project

##### 1.Create Your Folder Structure
When you create a new dbt item in Fabric, it only gives you a blank canvas. You’ll need to manually add the following:

```
dbt/
├── models/
│   └── my_model.sql
├── schema.yml
├── dbt_project.yml
```
##### 2.  Add Required Folders and Files:
Click `New` in the `Explorer` to create new files and folders
![pic](buildFolder.png)
   - `models/`: Folder to store your SQL models.
   - `my_model.sql`: A sample transformation query.
   - `schema.yml`: Defines tests and documentation for your models.
   - `dbt_project.yml`: Core configuration file for your dbt project.

##### 3. Populate Files
`dbt_project.yml` Tells dbt how to run your project.
```
name: 'fabric_demo'
version: '1.0'
profile: 'fabric'
model-paths: ['models']
```

`schema.yml` Defines metadata and tests for your models.
```
version: 2

models:
  - name: my_model
    description: "A simple model for demo purposes"
    columns:
      - name: id
        description: "Unique identifier"
        tests:
          - not_null
          - unique
```
`models\mymodel.sql` A basic transformation query that transforms some data found in the sample warehouse we created earlier.
```
SELECT
  DateID,
  Date,
  DateBKey
FROM
  Date
```

---

## ⚙️ Step 4: Configure and Run
- In the Settings panel:
  - Select your warehouse connection that we created earlier `warehouse-test`
  - Set your schema name, in this case we use dbo
  - Adjust thread count (default: 4)
- Click **Run** to execute your models
- View input, ouput, and potential errors directly in the UI in the `Job output` section

---

## 🌟 Why This Matters
- No external setup or adapters needed
- Fully integrated with Fabric’s compute and security
- Visual lineage and Git integration
- Ideal for SQL-savvy data engineers and analysts
