
---

# **Airline-Data-Pipeline-Automatione**  
### **Seamless Data Processing from S3 to Redshift with AWS Services**  

## **📌 Project Overview**  
The **Automated Airline Data Ingestion Pipeline** is a fully automated workflow that ingests, processes, and loads airline booking data into **Amazon Redshift** for analysis. The pipeline is designed to handle **large volumes of airline data** efficiently while ensuring **error handling and notifications** at every stage.  
![Architecture](https://github.com/user-attachments/assets/c5e3c63c-aa7c-45fa-9dfc-1553e81f216d)
🔹 **Trigger:** The process starts when a new airline booking data file is uploaded to **Amazon S3**.  
🔹 **Orchestration:** AWS **Step Functions** manage the entire workflow, ensuring smooth execution.  
🔹 **Processing:** AWS **Glue Crawlers** catalog the data, and **AWS Glue ETL Jobs** transform and load it into **Amazon Redshift**.  
🔹 **Notifications:** AWS **SNS (Simple Notification Service)** provides alerts on success or failure.  

---

# **📊 High-Level Workflow**  
## **1️⃣ Data Upload**  
✈️ Raw airline booking data files are uploaded to a specific **Amazon S3 bucket**.  

## **2️⃣ Event Trigger**  
📌 **AWS EventBridge** detects the file upload and triggers an **AWS Step Function**, starting the ingestion process.  

## **3️⃣ Data Crawling**  
🔍 **AWS Glue Crawler** scans the new data, updates metadata, and stores schema details in the **Glue Data Catalog**.  

## **4️⃣ ETL Processing**  
🛠 **AWS Glue ETL Job** processes, transforms, and enriches the data before **loading it into Amazon Redshift**.  

## **5️⃣ Data Storage**  
📊 The processed data is stored in **Amazon Redshift**, making it available for analytics and querying.  

## **6️⃣ Notifications & Error Handling**  
📩 AWS **SNS** sends email notifications for **successful runs or errors** during ingestion.  

---

# **🏗️ System Architecture**  
### **📌 Architecture Components and Flow**  

🗂️ **Amazon S3:** Stores raw airline data.  
📡 **EventBridge:** Detects new file uploads and triggers the pipeline.  
🛠️ **Step Functions:** Manages the entire data ingestion workflow.  
📖 **AWS Glue Crawler:** Reads the data, updates metadata in the **Glue Data Catalog**.  
⚙️ **AWS Glue ETL Job:** Transforms and enriches data for analysis.  
📊 **Amazon Redshift:** Stores the final processed dataset for querying.  
📢 **AWS SNS:** Sends real-time alerts on pipeline success or failure.  
🛡 **AWS CloudTrail:** Logs API calls for security and troubleshooting.  

---

# **🔧 Prerequisites for Deployment**  
Before setting up the pipeline, ensure the following AWS resources and configurations are available:  

✅ **AWS Account** with access to **S3, Glue, Step Functions, Redshift, SNS, and EventBridge**.  
✅ **AWS CLI** installed and configured with the required IAM permissions.  
✅ **Amazon Redshift Cluster** set up with a JDBC connection for data ingestion.  
✅ **SNS Topic** created to receive success and failure notifications via email.  

---

# **🛠️ Step-by-Step Implementation**  

## **Step 1: Setting Up the S3 Bucket**  
📌 Create an S3 bucket to store **airline booking data** files.  
📌 Enable **event notifications** on the bucket to detect **new file uploads**.  

## **Step 2: Configuring EventBridge**  
📡 Set up an **EventBridge rule** to listen for **PUT events** in the S3 bucket.  
📡 Configure it to trigger the **AWS Step Function** whenever a new file is uploaded.  

## **Step 3: Orchestrating with Step Functions**  
🛠 Create an **AWS Step Function workflow** to manage the pipeline’s execution.  
🔀 Define a **Choice State** to handle different scenarios (e.g., success vs. failure).  

## **Step 4: Configuring AWS Glue Crawler**  
🔍 Set up an **AWS Glue Crawler** to:  
   - Scan the new data in S3  
   - Update the **Glue Data Catalog** with schema metadata  

## **Step 5: Running the AWS Glue ETL Job**  
⚙️ Develop an **AWS Glue ETL job** that:  
   - Reads and **transforms raw airline data**  
   - Applies **data cleaning and enrichment**  
   - Loads the transformed data into **Amazon Redshift**  

## **Step 6: Storing Data in Redshift**  
📊 Create a **Redshift table** to store processed data.  
📌 Load transformed data from the Glue ETL job into **Redshift via JDBC connection**.  

## **Step 7: Setting Up Notifications**  
📩 Configure **AWS SNS** to send:  
   - ✅ **Success notifications** when data is successfully ingested.  
   - ❌ **Failure notifications** if errors occur during ingestion.  

---

# **🚨 Error Handling & Fault Tolerance**  

### **🛠 AWS Glue Crawler Failures**  
🚨 **Scenario:** Schema mismatch, file access issues, or missing files.  
📌 **Action:** Step Function detects failure and sends an SNS **failure notification**.  
📊 **Logs:** AWS CloudTrail provides detailed error logs for troubleshooting.  

### **⚙️ AWS Glue ETL Job Failures**  
🚨 **Scenario:** Data transformation errors, missing dependencies, or script failures.  
📌 **Action:** Step Function routes execution to a **failure path** and sends an SNS alert.  
📊 **Logs:** CloudTrail logs provide debugging details.  

### **📡 General Workflow Failures**  
🚨 **Scenario:** API call failures, misconfigured EventBridge rules, or IAM permission issues.  
📌 **Action:** Step Function triggers an SNS failure notification.  
📊 **Logs:** CloudTrail logs API activity for analysis.  

---

# **📈 Execution Flow & Monitoring**  

## ✅ **Successful Execution**  
![execution_successfull](https://github.com/user-attachments/assets/46f29c94-bc06-40c2-b625-61000d32e46f)

📌 Step Function executes all steps **sequentially**:  
✅ **S3 Upload → EventBridge Trigger → Glue Crawler → ETL Job → Redshift Ingestion**  
📩 **SNS sends a success notification.**  

## ❌ **Failure Execution**  
![failed_execution](https://github.com/user-attachments/assets/e9e4bd4e-2d53-4a8e-81f4-501e92043c51)

🚨 If an error occurs:  
❌ Step Function **routes execution to the failure path**.  
📩 SNS **sends a failure notification** with details.  
📊 Logs can be analyzed using **AWS CloudTrail**.  

---

# **📌 Usage & How to Trigger the Pipeline**  

🔹 Simply **upload a new airline booking file** to the designated S3 bucket.  
🔹 The **automated workflow** triggers immediately.  
🔹 Processed data is **stored in Redshift**, ready for **querying & analysis**.  
🔹 **Real-time notifications** keep users informed about the pipeline’s success or failure.  

---

# **🚀 Key Benefits of This Pipeline**  

✅ **Fully Automated Workflow:** No manual intervention required.  
✅ **Scalable & Efficient:** Handles large volumes of airline booking data seamlessly.  
✅ **Robust Error Handling:** Prevents data loss and ensures quick failure recovery.  
✅ **Real-Time Notifications:** Immediate alerts via **AWS SNS**.  
✅ **Secure & Auditable:** API activity tracked with **AWS CloudTrail**.  
✅ **Optimized for Analytics:** Data structured in **Amazon Redshift** for fast querying.  

---

# **🎯 Conclusion**  

This **Automated Airline Data Ingestion Pipeline** ensures **seamless ingestion, transformation, and storage** of airline booking data in **Amazon Redshift**. Leveraging **AWS Step Functions, Glue, Redshift, and SNS**, it offers **end-to-end automation with real-time monitoring and fault tolerance**.  

💡 **Deploy this pipeline to streamline airline data processing and enable powerful data-driven insights!** 🚀
