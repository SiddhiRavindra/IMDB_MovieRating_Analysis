# IMDb Data Engineering Project

A comprehensive end-to-end data engineering solution for IMDb movie data using Azure Data Factory, Alteryx, Snowflake, and Power BI. This project implements ETL/ELT pipelines with dimensional modeling to deliver actionable insights for movie analytics.

## 📋 Project Overview

This project builds a complete data pipeline that processes IMDb movie data through multiple stages - from raw data profiling to business-ready analytics dashboards. The solution leverages cloud-native Azure services and modern data warehousing with Snowflake.

### Key Technologies

- **Azure Data Factory (ADF)**: Orchestration and data movement
- **Alteryx**: Data profiling and advanced data cleaning
- **Snowflake**: Cloud data warehouse for dimensional data
- **DBeaver**: SQL development and database management
- **Power BI**: Business intelligence and visualization
- **Azure Data Lake Storage**: Scalable data storage

## 🎯 Project Objectives

Transform raw IMDb movie data into analytics-ready insights through:
- Comprehensive data profiling and quality assessment
- Advanced data cleansing and standardization
- Star schema dimensional modeling
- Automated ETL/ELT pipeline orchestration
- Interactive business intelligence dashboards

## 🏗️ Architecture

```
Data Sources (IMDb) 
       ↓
   Alteryx (Profiling & Cleaning)
       ↓
Azure Data Factory (Orchestration)
       ↓
   Snowflake (Star Schema)
       ↓
   Power BI (Dashboards)
```

## 📊 Pipeline Stages

### 1. Data Profiling (Alteryx)
**Purpose**: Understand data structure, quality, and patterns

- Analyze data distributions and statistics
- Identify missing values and outliers
- Assess data quality metrics
- Generate profiling reports
- Document data characteristics

**Key Outputs**:
- Data quality scorecards
- Column-level statistics
- Pattern recognition reports
- Recommendations for cleaning

### 2. Data Cleaning (Alteryx & ADF)
**Purpose**: Cleanse and standardize raw IMDb data

**Cleaning Operations**:
- Remove duplicate records
- Handle missing/null values
- Standardize date formats
- Clean text fields (titles, descriptions)
- Validate data types
- Filter invalid records
- Normalize naming conventions

**Technologies**: 
- Alteryx for complex transformations
- ADF for scalable cloud processing

### 3. Snowflake Integration
**Purpose**: Connect to Snowflake for dimensional data storage

**Components**:
- Snowflake linked service configuration
- Secure credential management
- Connection pooling and optimization
- Multi-environment support (Dev/Test/Prod)

**Storage Strategy**:
- Stage tables for raw data
- Dimensional tables for analytics
- Fact tables for metrics

### 4. Star Schema Design (ER Modeling)
**Purpose**: Design optimal dimensional model for analytics

**Dimensional Model**:

**Fact Tables**:
- `FactMovieDetails`: Core movie metrics and relationships
- `FactBoxOffice`: Revenue and financial performance
- `FactRatings`: User ratings and reviews

**Dimension Tables**:
- `DimMovie`: Movie attributes (title, year, runtime)
- `DimGenre`: Movie genres and categories
- `DimDirector`: Director information
- `DimActor`: Cast member details
- `DimDate`: Time dimension for temporal analysis
- `DimStudio`: Production company details

### 5. Dimensional Schema Creation (DBeaver & Snowflake)
**Purpose**: Implement star schema in Snowflake

**Implementation Steps**:
1. Create database and schemas
2. Define dimension tables with surrogate keys
3. Create fact tables with foreign keys
4. Implement slowly changing dimensions (SCD Type 2)
5. Add constraints and indexes
6. Set up data retention policies

**SQL Scripts**:
```sql
-- Example: Create Movie Dimension
CREATE TABLE DimMovie (
    MovieKey INT AUTOINCREMENT PRIMARY KEY,
    MovieID VARCHAR(20) UNIQUE,
    Title VARCHAR(500),
    ReleaseYear INT,
    Runtime INT,
    Language VARCHAR(50),
    Country VARCHAR(100),
    EffectiveDate DATE,
    ExpirationDate DATE,
    IsCurrent BOOLEAN
);
```

### 6. ADF Pipeline Development
**Purpose**: Automate data loading into Snowflake dimensions and facts

**Pipeline Components**:
- **IMDB Pipeline**: Main orchestration pipeline
- **Data Flow**: Transformation logic
- **Staging Activities**: Load to stage tables
- **Dimension Loading**: SCD implementation
- **Fact Loading**: Incremental and full loads
- **Error Handling**: Retry logic and notifications

**Key Features**:
- Parameterized pipelines for flexibility
- Incremental loading strategies
- Data validation checks
- Logging and monitoring
- Trigger-based execution

### 7. Power BI Dashboard
**Purpose**: Deliver business insights through interactive visualizations

**Dashboard Components**:
- Movie performance metrics
- Genre analysis and trends
- Director and actor performance
- Box office revenue analytics
- Rating distributions
- Temporal trends and patterns

**Key Metrics**:
- Total movies by genre
- Average ratings by year
- Top-grossing movies
- Actor/Director rankings
- Release trends over time

## 📁 Project Structure

```
├── dataflow/                    # ADF data transformation flows
│   └── dataflowfactmovietestfinal
├── dataset/                     # Dataset definitions
│   └── SnowflakeV2Table: SnowflakeFactMovieDetails
├── factory/                     # Factory configuration
│   └── ADF settings and metadata
├── linkedService/               # Connection configurations
│   ├── AzureDataLakeStorage    # ADLS connection
│   └── (Snowflake connections)
├── pipeline/                    # Orchestration pipelines
│   └── IMDB                    # Main IMDb pipeline
└── publish_config.json         # Publishing configuration
```

## 🚀 Getting Started

### Prerequisites

- **Azure Subscription** with Data Factory access
- **Snowflake Account** (Standard or higher)
- **Alteryx Designer** (for data profiling/cleaning)
- **DBeaver** or similar SQL client
- **Power BI Desktop** (for dashboard development)
- **Azure Data Lake Storage Gen2**

### Setup Instructions

#### 1. Clone the Repository
```bash
git clone https://github.com/SiddhiRavindra/your-repo-name.git
cd your-repo-name
```

#### 2. Configure Azure Resources

**Create Azure Data Factory**:
```bash
az datafactory factory create \
  --resource-group <resource-group> \
  --factory-name <factory-name> \
  --location <location>
```

**Set up Azure Data Lake Storage**:
```bash
az storage account create \
  --name <storage-account-name> \
  --resource-group <resource-group> \
  --location <location> \
  --sku Standard_LRS \
  --kind StorageV2 \
  --hierarchical-namespace true
```

#### 3. Configure Snowflake

**Create Database and Schema**:
```sql
-- In Snowflake
CREATE DATABASE IMDB_DW;
CREATE SCHEMA IMDB_DW.STAGING;
CREATE SCHEMA IMDB_DW.DIMENSIONS;
CREATE SCHEMA IMDB_DW.FACTS;

-- Create warehouse
CREATE WAREHOUSE IMDB_WH 
  WITH WAREHOUSE_SIZE = 'MEDIUM'
  AUTO_SUSPEND = 300
  AUTO_RESUME = TRUE;
```

#### 4. Set Up Linked Services

**Configure Snowflake Connection in ADF**:
- Navigate to ADF Studio
- Create new Linked Service for Snowflake
- Enter connection details:
  - Account identifier
  - Database name
  - Warehouse name
  - Username/Password (use Key Vault)

#### 5. Deploy ADF Pipelines

1. Import ARM templates or use ADF Studio
2. Validate all linked services
3. Update pipeline parameters
4. Test with debug runs
5. Publish to ADF

#### 6. Run Initial Load

```bash
# Trigger the IMDB pipeline manually
az datafactory pipeline create-run \
  --resource-group <resource-group> \
  --factory-name <factory-name> \
  --pipeline-name IMDB
```

## 🔄 Data Flow Process

### End-to-End Pipeline

1. **Extract**: Pull raw IMDb data from source
2. **Profile**: Analyze data quality in Alteryx
3. **Clean**: Apply cleaning rules and transformations
4. **Stage**: Load cleaned data to Snowflake staging
5. **Transform**: Apply business logic and create dimensions
6. **Load**: Populate fact and dimension tables
7. **Validate**: Run data quality checks
8. **Visualize**: Refresh Power BI dashboards

### Incremental Loading Strategy

- **Full Load**: Initial data load (one-time)
- **Incremental Load**: Daily/weekly updates
- **Change Data Capture**: Track modifications
- **SCD Type 2**: Maintain historical dimension changes

## 📊 Data Model

### Star Schema Overview

**Fact Table** (FactMovieDetails):
- Foreign keys to all dimensions
- Measures: revenue, votes, ratings
- Grain: One row per movie

**Dimensions**:
- DimMovie (Movie attributes)
- DimGenre (Genre hierarchy)
- DimDirector (Director SCD Type 2)
- DimActor (Cast information)
- DimDate (Time dimension)
- DimStudio (Production companies)

## 🛠️ Development Workflow

### Alteryx Workflow
1. Connect to data sources
2. Run data profiling tools
3. Apply cleansing transformations
4. Export cleaned data
5. Document transformation logic

### ADF Development
1. Create data flows in ADF Studio
2. Define source and sink datasets
3. Add transformation activities
4. Configure error handling
5. Test with debug mode
6. Publish changes

### Snowflake Development
1. Design star schema in ER tool
2. Write DDL scripts in DBeaver
3. Implement SCD logic
4. Create views and stored procedures
5. Set up access controls

## 📈 Monitoring & Maintenance

### ADF Monitoring
- Pipeline run history
- Activity-level metrics
- Data flow performance
- Error logs and alerts

### Snowflake Monitoring
```sql
-- Query history
SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.QUERY_HISTORY
WHERE DATABASE_NAME = 'IMDB_DW'
ORDER BY START_TIME DESC;

-- Warehouse usage
SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.WAREHOUSE_METERING_HISTORY
WHERE WAREHOUSE_NAME = 'IMDB_WH';
```

### Data Quality Checks
- Row count validation
- NULL value checks
- Referential integrity validation
- Business rule validation

## 🔒 Security Best Practices

- **Azure Key Vault**: Store all credentials
- **Managed Identity**: Use for ADF authentication
- **Snowflake Roles**: Implement RBAC
- **Network Security**: Configure private endpoints
- **Data Encryption**: Enable at-rest and in-transit
- **Audit Logging**: Track all data access

## 📊 Power BI Integration

### Dashboard Features
- Interactive movie explorer
- Genre performance analysis
- Director/Actor rankings
- Revenue trend analysis
- Rating distributions
- Release timeline visualization

### Connecting to Snowflake
```
Data Source: Snowflake
Server: <account>.snowflakecomputing.com
Database: IMDB_DW
Warehouse: IMDB_WH
Authentication: Username/Password or SSO
```

## 🧪 Testing

### Unit Testing
- Test individual ADF activities
- Validate data flow transformations
- Check SQL scripts in DBeaver

### Integration Testing
- End-to-end pipeline execution
- Cross-system data validation
- Performance benchmarking

### Data Quality Testing
- Completeness checks
- Accuracy validation
- Consistency verification
- Timeliness monitoring

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit changes (`git commit -m 'Add new feature'`)
4. Push to branch (`git push origin feature/enhancement`)
5. Open a Pull Request

## 📚 Documentation

### Additional Resources
- [Azure Data Factory Documentation](https://docs.microsoft.com/azure/data-factory/)
- [Snowflake Documentation](https://docs.snowflake.com/)
- [Alteryx Documentation](https://help.alteryx.com/)
- [Star Schema Best Practices](https://www.kimballgroup.com/)
- [Power BI Documentation](https://docs.microsoft.com/power-bi/)


---

**Built with Azure Data Factory, Snowflake, and Power BI** | **IMDb Analytics Pipeline**
