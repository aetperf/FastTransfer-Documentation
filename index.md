
# FastTransfer CLI

FastTransfer is a command-line interface tool designed for efficient data transfer between various database systems. It offers a wide range of options to customize the data transfer process to suit different requirements and environments.

![FastTransfer](./img/FastTransfer.jpg)

## Table of contents

- [FastTransfer CLI](#fasttransfer-cli)
- [Supported Sources](#supported-sources)
- [Supported Targets](#supported-targets)
- [Supported OS](#supported-os)
  - [Linux](#linux)
  - [Windows](#windows)
- [Limitations and connections](#limitations-and-connections)
- [Gui Wizard to generate command line](#gui-wizard-to-generate-command-line)
- [Syntax](#syntax)
- [Options explained](#options-explained)
- [Examples](#examples)
- [Installation](#installation)
- [Configuration and settings for logging](#configuration-and-settings-for-logging)
- [Wrappers](#wrappers)
- [License](#license)




## Supported Sources

Source | Windows AMD64 | Linux AMD64 | Linux ARM64
:--- | :---: | :---: | :---:
ClickHouse | ✅ | ✅ | ✅
DuckDB | ✅ | ✅ | ✅
MySQL | ✅ | ✅ | ✅
Netezza | ✅ | ✅ | ✅
ODBC | ✅ | ✅  | ✅
OLEDB | ✅ |❌  | ❌
Oracle | ✅ | ✅ | ✅
PostgreSQL | ✅ | ✅ | ✅
SQL Server | ✅ | ✅ | ✅
SAP Hana | ✅ | ✅ | ❌
Teradata | ✅ | ✅ | ❌

## Supported Targets

Target | Windows AMD64 | Linux AMD64 | Linux ARM64
:--- | :---: | :---: | :---:
ClickHouse | ✅ | ✅ | ✅
DuckDB | ✅ | ✅ | ✅
MySQL | ✅ | ✅ | ✅
Netezza | ✅ | ✅ | ✅
ODBC | ❌ | ❌  | ❌
OLEDB | ❌ |❌  | ❌
Oracle | ✅ | ✅ | ✅
PostgreSQL | ✅ | ✅ | ✅
SQL Server | ✅ | ✅ | ✅
SAP Hana | ✅ | ✅ | 
Teradata | ✅ | ✅ | 

## Supported OS

### Linux

| OS                            | Versions                    | Architectures         | 
| ----------------------------- | --------------------------- | --------------------- | 
| Alpine                        | 3.21, 3.20, 3.19, 3.18      | Arm64, x64            | 
| Azure Linux                   | 3.0                         | Arm64, x64            | 
| CentOS Stream                 | 10, 9                       | Arm64, x64            | 
| Debian                        | 12                          | Arm64, x64            | 
| Fedora                        | 41, 40                      | Arm64, x64            | 
| openSUSE Leap                 | 15.6                        | Arm64, x64            | 
| Red Hat Enterprise Linux      | 10, 9, 8                    | Arm64, x64            | 
| SUSE Enterprise Linux         | 15.6                        | Arm64, x64            | 
| Ubuntu                        | 24.10, 24.04, 22.04, 20.04  | Arm64, x64            | 

Here is a page that documents how to check the certificate on Linux : [check linux certificate](./security/check_certificate_linux.md).

### Windows

| OS                            | Versions                    | Architectures         | 
| ----------------------------- | --------------------------- | --------------------- | 
| Nano Server                   | 2025, 2022, 2019            | x64                   |
| Windows                       | 11 24H2 (IoT), 11 24H2 (E), 11 24H2, 11 23H2, 11 22H2 (E), 10 22H2, 10 21H2 (E), 10 21H2 (IoT), 10 1809 (E), 10 1607 (E) | x64 |
| Windows Server                | 2025, 23H2, 2022, 2019, 2016, 2012-R2, 2012 | x64 |  |
| Windows Server Core           | 2025, 2022, 2019, 2016, 2012-R2, 2012 | x64     |


## Limitations and connections

- array data types are not always supported in the current version (except for pgcopy target)
- spatial data types are not always supported between heterogenous rdbms.
- vector datatypes are not always compatibles between heterogenous rdbms.
- **TARGET TABLE MUST EXISTS**
- target table must have columns with compatibles datatypes with the source and aligned if mapmethod *position* is used.

## Gui Wizard to generate command line


<button type="button">[FastTransfer Wizard](FastTransfer_Wizard.html)</button>

## Syntax:

- [FastTransferCommand](#fasttransfercommand)
- [FastTransferOptions](#fasttransferoptions)
- [SourceConnectionType](#sourceconnectiontype)
- [SourceConnectionParameters](#sourceconnectionparameters)
- [SourceInfos](#sourceinfos)
- [TargetConnectionType](#targetconnectiontype)
- [TargetConnectionParameters](#targetconnectionparameters)
- [TargetInfos](#targetinfos)
- [ParallelParameters](#parallelparameters)
- [MappingParameters](#mappingparameters)
- [LogParameters](#logparameters)
- [LicenseParameters](#licenseparameters)

![Syntax](diagram/Syntax.svg)

**FastTransferCommand:**

![FastTransferCommand](diagram/FastTransferCommand.svg)


**FastTransferOptions:**

![FastTransferOptions](diagram/FastTransferOptions.svg)


**SourceConnectionType:**

![SourceConnectionType](diagram/SourceConnectionType.svg)


**SourceConnectionParameters:**

![SourceConnectionParameters](diagram/SourceConnectionParameters.svg)

**SourceInfos:**

![SourceInfos](diagram/SourceInfos.svg)


**SourceConnectionType:**

![TargetConnectionType](diagram/TargetConnectionType.svg)


**TargetConnectionParameters:**

![TargetConnectionParameters](diagram/TargetConnectionParameters.svg)


**TargetInfos:**

![TargetInfos](diagram/TargetInfos.svg)


**ParallelParameters:**

![ParallelParameters](diagram/ParallelParameters.svg)


**MappingParameters:**

![MappingParameters](diagram/MappingParameters.svg)


**LogParameters:**

![LogParameters](diagram/LogParameters.svg)

**LicenseParameters:**

![LogParameters](diagram/LicenseParameters.svg)



### Options explained

**WARNING : WE STRONG ADVISE TO USE LONG PARAMETERS**

- `-?`, `--help`  
  Show help information.

- `-c`, `--sourceconnectiontype <type>` 

    Source Connection Type. 
    Allowed Values: 

    * `clickhouse` for ClickHouse
    * `duckdb` for duckdb
    * `duckdbstream` for duckdb using streaming (more memory efficient))
    * `hana` for SAP HANA (.net driver)
    * `msoledbsql` SQL Server OleDB
    * `mssql` SQL Server Native Client (.Net)
    * `mysql` MySQL
    * `nzcopy` Netezza copy (WIP)
    * `nzoledb` Netzza OleDB
    * `nzsql` Netezza Native (.net driver)
    * `odbc` ODBC datasource (DSN must be configured)
    * `oledb` Generic OleDB datasource
    * `oraodp` Oracle ODP.Net
    * `pgcopy` PostgreSQL Copy
    * `pgsql` PostgreSQL Native (.Net)
    * `teradata` Teradata (.Net)


 - `-g`, `--sourceconnectstring <connectionstring>`  
    Source Connection String. (override all other source connection parameters).

  - `-n`, `--sourcedsn <dsn>`  
    ODBC DSN. (only if odbc source type is used). Drivers must be already installed on the machine and DSN must be configured.

  - `-p`, `--sourceprovider <provider>`  
    OleDB provider (e.g., `MSOLEDBSQL` for MSSQL or `NZOLEDB` for Netezza...).
    Only if oledb source type is used. OleDB provider must be already installed on the machine.

  - `-i`, `--sourceserver <server>`  
    * Source SQL instance (Server or Server\instance or Server:port)
    * for DuckDB the .duckdb file or :memory: 

  - `-u`, `--sourceuser <user>`  
    Source user.

  - `-x`, `--sourcepassword <password>`  
    Source user's password.

  - `-a`, `--sourcetrusted`  
    Switch to use trusted authentication on source.

  - `-d`, `--sourcedatabase <database>`  
    Source database.

  - `-s`, `--sourceschema <schema>`  
    Source schema. (must be set if pgsql Ctid method is used)

  - `-t`, `--sourcetable <table>`  
    Source table. (must be set if pgsql Ctid method is used)

  - `-q`, `--query <query>`  
    Plain text SQL query. Will be used instead of source table if provided

  - `-f`, `--fileinput <file>`  
    Input file storing SQL query. The file must exist.

  - `-C`, `--targetconnectiontype <type>`  
    Target Connection Type. 
    Allowed Values: 

    * `clickhousebulk` for ClickHouse BulkCopy
    * `duckdb` for DuckDB
    * `hanabulk` for SAP HANA 
    * `msbulk` for SQL Server BulkCopy
    * `mysqlbulk` for MySQL BulkCopy
    * `nzbulk` for Netezza BulkCopy
    * `orabulk` for Oracle BulkCopy
    * `oradirect` for Oracle Direct
    * `pgcopy` for postgresql using copy (Binary format for postgresql sources and Text for others)
    * `pgsql` for PostgreSQL Native (.Net)
    * `teradata` for Teradata (.Net)


  - `-I`, `--targetserver <server>`  
    * Target SQL instance :
    Server or Server\instance or Server:port.
    * .duckdb file for DuckDB


  - `-U`, `--targetuser <user>`  
    Target user.

  - `-X`, `--targetpassword <password>`  
    Target user's password.

  - `-A`, `--targettrusted`  
    Switch to use trusted authentication on target.

  - `-D`, `--targetdatabase <database>`  
    Target database.

  - `-S`, `--targetschema <schema>`  
    Target schema.

  - `-T`, `--targettable <table>`  
    Target table.


  - `-M`, `--method <method>`  
    Method for parallelism (if needed).
    Allowed Values: 

    - `DataDriven` Use the distinct value of the distributeKeyColumn (which can be a column or an expression) to distribute data
    - `Ctid` Recommanded and exclusive for postgreSQL and postgreSQL compatible. Use the Ctid pseudo column (for pgsql and pgcopy source only)
    - `Random` Use a modulo on the distributeKeyColumn to distribute data
    - `Rowid` For Oracle sources only : use rowid slices
    - `RangeId` Use a numeric range to distribute data (useful with an identity column or sequence without gaps. The column must be numerical)
    - `Ntile` Use the ntile function to distribute data evenly data can be numerical, date, datetime or string
    - `NZDataSlice` : Netezza source only. Use the data slices to distribute data retrieval
    - `None` No parallelism
    
    Default Value: `None`. If you want to use a parallel export/import use other than None. Try to use Parallelism only if you have a large amount of data to transfer (more than 1M cells).

  - `-K`, `--distributeKeyColumn <column>`  
    Column to be used to distribute data Not needed if Ctid method is used.

  - `-P`, `--degree <degree>`  
    Degree of Parallelism
    
    * `0` for Auto 
    * `0 > n < 1024` for fixed degree.
    * `n < 0` negative values will be used to adapt the degree of parallelism to the number of available CPUs.
    eg : -2 will use half the cpus on the machine where FastTransfer is launched 
    
    Nota : whatever the degree, if the method is `None`, the extraction will remain serial
    
    Default Value: `-2`.
  
  - `Q`, `--datadrivenquery`  
    Override query to be used to get the values list for the `DataDriven` method. You can avoid select distinct of the distributeKeyColumn on large table, if you have de reference table that contains all the values.

  - `-L`, `--loadmode <mode>`  
    Load mode of the data into the target. 
    Allowed Values: 
    - `Append` append data to the target table
    - `Truncate` truncate the target table before loading
    
    Default Value: `Append`.

  - `-B`, `--batchsize <size>`  
    Batch Size for BulkCopy. Default Value: `1048576`.

  - `-W`, `--useworktables`  
    Swith that will activate the usage of intermediate work tables. Useful in some rare cases

  - `-N`, `--mapmethod`  
    mapping method for the columns between source and target.
  Allowed Values: 
    - `Position` : FastTransfer will map the columns by their position in the source and target tables
    - `Name` : FastTransfer will map the columns by their name in the source and target tables (case insensitive) and will ignore missing columns (from source or target)
    
    Default Value: `Position`. 

  - `-R`, `--runid <RunSpanID>`  
    Run ID. coming from the caller. It will be used to allow tracing of the process. Default is a random Guid.  

  - `O` ,`--settingsfile`
    Custom Settings file for logging and other settings. Default is `FastTransfer__settings.json` in the same folder as the executable.

  - `--license`  
    License file. Default is `FastTransfer.lic` in the same folder as the executable. You can provide another filepath or an url to get the license informations


## Examples

```powershell
.\FastTransfer.exe `
--sourceconnectiontype "mssql" `
--sourceserver "localhost" `
--sourceuser "fastuser" `
--sourcepassword "fastpassword" `
--sourcedatabase "AdventureWorks2017" `
--sourceschema "Person" `
--sourcetable "Person" `
--targetconnectiontype "pgcopy" `
--targetserver "localhost" `
--targetuser "fastuser" `
--targetpassword "fastpassword" `
--targetdatabase "fastdb" `
--targetschema "public" `
--targettable "Person" `
--method "RangeId" ` 
--distributeKeyColumn "PersonID" `
--loadmode "Truncate" `
--degree -2 `  #Automatically adapt the degree of parallelism to 1/2 of cpu available
--runid "mssql-to-pgcopy-123456"
```

```powershell
.\FastTransfer.exe `
--sourceconnectiontype "pgsql" `
--sourceserver "localhost:15432" `
--sourceuser "fastuser" `
--sourcepassword "fastpassword" `
--sourcedatabase "fastdb" `
--sourceschema "Public" `
--sourcetable "Person" `
--targetconnectiontype "msbulk" `
--targetserver "localhost" `
--targetuser "fastuser" `
--targetpassword "fastpassword" `
--targetdatabase "AdventureWorks2017" `
--targetschema "Person" `
--targettable "Person" `
--method "Ctid" ` # Ctid is for pgsql and pgcopy source only 
--loadmode "Truncate" `
--degree -2 `  #Automatically adapt the degree of parallelism to 1/2 of cpu available
--runid "pgsql-to-msbulk-123456" `
--mapmethod "Name" 
```


for more examples see [examples](./samples/samples.md)

# Installation

Download the latest version from the link provided by Arpe.io and extract the files to a directory on your machine.
 For Linux user run a `chmod +x FastTransfer` command.

For the trial, that's it! You are ready to use FastTransfer.

**For other edition than trial you will need a valid license.** By default FastTransfer will try to find a *FastTransfer.lic* file in the same directory. You can also provide another path or an url in your organisation where you store/share the license file by using the `--license` parameter.


## Configuration and settings for logging

FastTransfer uses a settings file to configure the logging.
The default file is `FastTransfer_settings.json` in the same folder as the executable. You can specify a custom file using the `-O` option.

You can download the [FastTransfer_settings.json template](https://github.com/aetperf/FastTransfer-Documentation/raw/refs/heads/main/FastTransfer_Settings.json) to get started. The default file is already configured to use the SQL Server database for logging. You can also use the console and file sinks for logging.

You can start from the default file and modify it to suit your needs.

- You can, for exemple, change the connection string for the logs database, or the minimum level of logging.
- You can also remove some targets if you don't need them in the using section.

```json
{
  "ConnectionStrings": {
    "MS_FastTransferLogs": "Server=localhost;Database=FastTransferLogs;Integrated Security=SSPI;Encrypt=True;TrustServerCertificate=True"
  },
  "Serilog": {
    "Using": [
      "Serilog.Sinks.Console",
      "Serilog.Sinks.File",
      "Serilog.Sinks.MSSqlServer",
      "Serilog.Enrichers.Environment",
      "Serilog.Enrichers.Thread",
      "Serilog.Enrichers.Process",
      "Serilog.Enrichers.Context"
    ],
    "MinimumLevel": "Debug",
```
# Wrappers
FastTransfer is also available using wrappers.
One fully fonctionnal and supported wrapper is available for TSQL using a CLR procedure that avoid using xp_cmdshell or for PostgreSQL. You can call FastTransfer throught the database (you need to copy the FastTransfer on the host where the instance/cluster reside)

- [FastTransfer in MSSQL using a CLR/TSQL Wrapper](https://github.com/aetperf/FastWrappers-TSQL)
- [FastTransfer in PostgreSQL using a Python Wrapper](https://github.com/aetperf/FastWrappers-PGSQL)
- [FastTransfer in an AWS Lambda using Docker](https://github.com/aetperf/FastTransfer-AWS-Lambda)

# License

Commercial License. You can [buy FastTransfer online](https://www.arpe.io/product/fasttransfer/) or contact us at [sales@arpe.io](mailto:sales@arpe.io) for more information.

[CLUF *(FR)*](legal/CONTRAT%20DE%20LICENCE%20UTILISATEUR%20FINAL.pdf) and [EULA *(EN)*](https://www.arpe.io/end-user-licence-agreement)


