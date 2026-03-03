# Azure-Data-Engineering-Pipeline---Metadata-Driven-ETL

I've built this project focusing on production-readiness, covering edge cases through a metadata-driven ETL architecture.




<img width="983" height="546" alt="Azure_DE_Ecom_Project drawio (1)" src="https://github.com/user-attachments/assets/46cef73e-7cdb-4423-850e-beba00d7a7a7" />


## 🎯 Key Features

- **Metadata-Driven** – Single pipeline dynamically processes multiple tables via configuration  
- **Medallion Architecture** – Bronze (raw) → Silver (cleaned) → Gold (aggregated)  
- **SCD Type 2** – Full historical tracking for dimension tables  
- **Incremental Loading** – Watermark-based extraction pattern  
- **Schema Evolution** – Handles schema drift without breaking downstream layers  
- **Edge Case Handling** – Late arrivals, reruns, failure recovery  
- **Observability** – Execution logging, watermark tracking, audit trail  



## 🏗️ Architecture Overview

Metadata stored in Azure SQL drives a dynamic Azure Data Factory pipeline that orchestrates:

1. Data ingestion into Bronze (ADLS Gen2, Delta format)  
2. Transformation and SCD Type 2 processing in Databricks (PySpark)  
3. Curated Gold layer for analytics consumption  

The pipeline design avoids hardcoding and scales by simply adding new configuration entries.



## 🔄 End-to-End Flow

1. ADF reads active table configurations from metadata tables  
2. Dynamically determines full vs incremental load  
3. Extracts data from source systems  
4. Writes raw data to Bronze (Delta Lake)  
5. Databricks transforms data into Silver (cleaned + SCD2 applied)  
6. Aggregated data published to Gold  



## 🛠️ Tech Stack

- **Orchestration:** Azure Data Factory  
- **Storage:** Azure Data Lake Storage Gen2  
- **Processing:** Azure Databricks (PySpark)  
- **Metadata Store:** Azure SQL Database  
- **Storage Format:** Delta Lake (ACID, schema evolution, time travel)  



## ⚠️ Real-World Scenarios Handled

- Safe pipeline restarts without duplicate data  
- Watermark-based incremental consistency  
- Late-arriving dimension records  
- Schema drift handling  



## 📈 Scalability Considerations

- Easily extensible to new source systems  
- Modular pipeline design driven entirely by metadata  
- Delta Lake ensures reliability and transactional consistency  
- Separation of orchestration and transformation layers  

---
