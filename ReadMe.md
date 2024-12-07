# **Azure Data Factory Transformation - Sales Data Transformation**

---

### **Business Objective:**

The objective of this project is to transform sales data from multiple rows with a single `ID` into a more readable and analytical columnar format using Azure Data Factory (ADF). The transformation process uses the Pivot transformation to change the rows into columns based on product names and corresponding sales. This transformation will enable easier analysis of sales performance across different products for each unique `ID`.

**Example:**

| ID | Product   | Sales |
|----|-----------|-------|
| 1  | Book      | 10    |
| 1  | Pen       | 20    |
| 1  | Paper     | 30    |

After Pivot transformation:

| ID | Book | Pen | Paper |
|----|------|-----|-------|
| 1  | 10   | 20  | 30    |

**This transformation is essential for businesses looking to efficiently analyze sales data across multiple products and categories.**

---

### **Procedure:**

#### 1. **Create Resource Group:**
   - A new Resource Group was created in Azure to manage and organize resources like the storage account, data factory, and other Azure storage services.
   
#### 2. **Create Storage Account:**
   - A Storage Account was created in Azure to store the input and output data. 
   - Created containers inside the Storage Account to store raw data files and transformation output.

#### 3. **Upload Data:**
   - Sample data for products and sales is uploaded into the storage container in a CSV or Parquet format.

#### 4. **Create Azure Data Factory (ADF) Instance:**
   - An instance of Azure Data Factory was created using Azure Portal.
   - Configured to interact with the storage account and perform ETL (Extract, Transform, Load) operations.

#### 5. **Create Data Flow:**
   - A Data Flow was created in ADF studio to perform the transformation.
   - The Pivot transformation was used to restructure the data (converting rows to columns).

#### 6. **Linked Service Configuration:**
   - Configured a Linked Service in ADF to connect to the Azure Blob Storage where data is stored.
   - This connection is used as a source and sink in the Data Flow to read input and write output data.

#### 7. **Pivot Transformation:**
   - The Pivot transformation was applied to convert product names into columns and aggregate the sales corresponding to each product.
   - The unique `ID` was used as the pivot key, while the `Product` field was pivoted into separate columns like "Book", "Pen", "Paper", etc., and the `Sales` field was aggregated.

   **Explanation of Pivot Logic:**
   - The Pivot transformation allows you to turn distinct values in one column (e.g., Product) into multiple columns. 
   - For each unique `ID`, the sales values are distributed across these new columns based on the product name.

#### 8. **Create Sink:**
   - The Sink in the data flow was set up to output the transformed data into another container in the Azure Storage Account.
   - The data was saved as a CSV/Parquet file in the specified container.

#### 9. **Data Flow Debugging:**
   - Debug mode was enabled to test the data flow before running the actual pipeline. 
   - This allowed for real-time validation and ensured the transformation logic was working as expected.

#### 10. **Create Pipeline:**
   - A Pipeline was created in ADF to orchestrate the data flow.
   - The pipeline included activities to run the data flow and manage the overall workflow.
   
   **Explanation of Pipeline:**
   - The pipeline connects the data flow to the source and sink linked services and manages execution.
   - It triggers data extraction, transformation, and loading into the destination storage.

#### 11. **Validate Pipeline Connections:**
   - Verified all linked services (storage accounts, blob containers) and datasets are connected and functional.
   
#### 12. **Trigger Pipeline Using Add Trigger:**
   - A trigger was added to schedule or manually initiate the pipeline.
   - Triggers can be time-based (e.g., daily, weekly) or event-based (e.g., file arrival).

#### 13. **Monitor Pipeline:**
   - ADF provides a monitoring interface where you can track the execution of the pipeline, check for any failures, and get detailed logs of the transformation process.
   - The monitor tool is used to ensure the pipeline runs successfully and to troubleshoot any issues.

#### 14. **Check Data in Blob Storage:**
   - After the pipeline execution, check the transformed data in the Blob Storage container.
   - Verify that the data has been successfully written to the output file in the expected format (CSV/Parquet).

---

### **Tools and Technologies:**

- **Azure Data Factory (ADF):** For orchestrating ETL operations and transforming the data.
- **Azure Blob Storage:** For storing raw input data and output data.
- **Pivot Transformation in ADF Data Flow:** To reshape the data from rows to columns based on a pivot key (e.g., `Product` to columns).
- **Azure Portal:** For managing resources such as Storage Accounts and ADF instances.
- **Debugging and Monitoring in ADF Studio:** For testing and tracking pipeline execution.
- **Linked Services and Datasets:** To configure connections between ADF and Azure Blob Storage.

---

### **Contributions:**

- **Initial Setup and Resource Creation:** Setup of Azure Resource Group, Storage Accounts, Containers, and ADF instance.
- **Data Transformation Logic:** Development of the Data Flow using the Pivot transformation to convert row data into columnar format.
- **Pipeline Development and Orchestration:** Creation and orchestration of ADF Pipelines to automate the data flow process.
- **Testing and Debugging:** Running tests and debugging the Data Flow to ensure data transformations are accurate.
- **Monitoring and Optimization:** Monitoring the pipeline execution for issues and optimizing performance.

---

### **Folder Structure:**

```
Azure-ADF-Pivot-Transformation/
│
├── data/                   # Folder for sample data
│   ├── input_data.csv      # Raw data uploaded to Azure Blob Storage
│   └── output_data.csv     # Transformed data saved in Azure Blob Storage
│
├── src/                    # ADF Pipeline and Data Flow JSONs
│   ├── pipeline.json       # Pipeline configuration
│   ├── data_flow.json      # Data Flow configuration
│   └── linked_service.json # Linked Service configurations
│
└── README.md               # Project documentation
```

---

## Contributing
Feel free to fork the repository and contribute by adding more transformations or optimizations.

## License
This project is licensed under the MIT License.

