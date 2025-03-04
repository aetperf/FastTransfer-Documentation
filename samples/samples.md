# FastTransfer Samples

## Source Postgreql - Target MSSQL

### Transfert de PostgreSQL à MSSQL avec une requête SQL
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --query "select * from tpch_10.orders" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "None" `
    --loadmode "Truncate"
```

### Transfert de PostgreSQL à MSSQL avec un schéma et une table spécifiée
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "None" `
    --loadmode "Truncate"
```

### Transfert de PostgreSQL à MSSQL avec une requête SQL pour une autre table
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --query "select * from tpch_10.nation" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "nation" `
    --method "None" `
    --loadmode "Truncate"
```

### Transfert de PostgreSQL à MSSQL avec une méthode DataDriven
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:15432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --query "select * from tpch_10.orders" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "DataDriven" `
    --distributeKeyColumn "FLOOR(o_orderkey/10000000)" `
    --degree 6
```

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:15432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "Ctid" `
    --loadmode "Truncate" `
    --degree 12
```

### Transfert de PostgreSQL à MSSQL avec une méthode Random
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:15432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --query "select * from tpch_10.orders" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "Random" `
    --distributeKeyColumn "o_orderkey" `
    --degree 6
```

## Source Postgreql - Target MSSQL Parallel Ctid

### Transfert from PostgreSQL to MSSQL with Ctid method for table "orders"

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "Ctid" `
    --degree 10 `
    --loadmode "Truncate"
```

### Transfert from PostgreSQL to MSSQL with Ctid method for table "lineitem"
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --sourceschema "tpch_10" `
    --sourcetable "lineitem" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "lineitem" `
    --method "Ctid" `
    --degree 10 `
    --loadmode "Truncate"
```

### Dynamic degree using negative degree
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:15432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "Ctid" `
    --degree -4 `
    --loadmode "Truncate"
```


### Using an input file
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourcedatabase "tpch" `
    --sourcefile "..\..\..\..\FastTransfert\samples\select_orders.sql" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders_2" `
    --method "Ctid" `
    --degree 6 `
    --loadmode "Truncate"
```



## Source Postgreql - Target Postgresql

### Transfer from PostgreSQL to PostgreSQL using a query
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "pgcopy" `
    --targetserver "localhost" `
    --targetdatabase "tpch_import" `
    --query "select * from ""tpch_10"".orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "orders" `
    --method "None"
```

### Transfer from PostgreSQL to PostgreSQL using Ctid method
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "pgcopy" `
    --targetserver "localhost" `
    --targetdatabase "tpch_import" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "orders" `
    --method "Ctid" `
    --degree 6 `
    --loadmode "Truncate"
```

### Source Postgreql - Target Postgresql using insert unnest
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "pgsql" `
    --targetserver "localhost" `
    --targetdatabase "tpch_import" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "orders" `
    --method "Ctid" `
    --degree 10 `
    --loadmode "Truncate" `
    --batchsize 10000
```

### Source Postgreql - Target Postgreql using pgcopy binary

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgcopy" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "pgcopy" `
    --targetserver "localhost" `
    --targetdatabase "tpch_import" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "orders" `
    --method "None" `
    --loadmode "Truncate"
```

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgcopy" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "pgcopy" `
    --targetserver "localhost:15432" `
    --targetdatabase "tpch_import" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "orders" `
    --method "Ctid" `
    --degree 10 `
    --loadmode "Truncate"
```

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgcopy" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "pgcopy" `
    --targetserver "localhost" `
    --targetdatabase "tpch_import" `
    --sourceschema "tpch_10" `
    --sourcetable "lineitem" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "lineitem" `
    --method "Ctid" `
    --degree 10 `
    --loadmode "Truncate"
```


## Source mssql - Target Postgresql

### Transfer from MSSQL to PostgreSQL without method

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "pgcopy" `
    --targetserver "localhost:15432" `
    --targetdatabase "tpch_import" `
    --query "select * from dbo.orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "orders" `
    --method "None" `
    --loadmode "Truncate"
```

### Transfer from MSSQL to PostgreSQL with Random method
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "pgcopy" `
    --targetserver "localhost:15432" `
    --targetdatabase "tpch_import" `
    --query "select * from dbo.orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "orders" `
    --method "Random" `
    --distributeKeyColumn "o_orderkey" `
    --degree -3 `
    --loadmode "Truncate"
```

## Source mssql - Target mysql

### Transfer from MSSQL to MySQL without method
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "mysqlbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch" `
    --query "select * from dbo.orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch" `
    --targettable "orders" `
    --method "None" `
    --loadmode "Truncate"
```

### Transfer from MSSQL to MySQL with Random method

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "mysqlbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch" `
    --query "select * from dbo.orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch" `
    --targettable "orders" `
    --method "Random" `
    --distributeKeyColumn "o_orderkey" `
    --degree 6 `
    --loadmode "Truncate"
```

### Transfer from MSSQL to MySQL with DataDriven method

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "mysqlbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch" `
    --query "select * from dbo.orders_part" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch" `
    --targettable "orders" `
    --method "DataDriven" `
    --distributeKeyColumn "`$PARTITION.PF_DATE(o_orderdate)" `
    --degree 7 `
    --loadmode "Truncate"
```

### Transfer from MSSQL to MySQL with DataDriven method and additional column
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "mysqlbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch" `
    --query "select *,null as o_orderdate_year from dbo.orders" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch" `
    --targettable "orders_part" `
    --method "DataDriven" `
    --distributeKeyColumn "`$PARTITION.PF_DATE(o_orderdate)" `
    --degree -4 `
    --loadmode "Truncate"
```


## Source MySQL - Target MSSQL

### Transfert de MySQL à MSSQL sans méthode spécifique

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mysql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --query "select * from tpch.orders" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "None"
``` 


### Transfert de MySQL à MSSQL avec méthode Random
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mysql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --query "select * from tpch.orders" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "Random" `
    --distributeKeyColumn "o_orderkey" `
    --degree 10
```


### Transfert de MySQL à MSSQL avec méthode DataDriven
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mysql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --query "select * from tpch.orders" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "DataDriven" `
    --distributeKeyColumn "year(o_orderdate)" `
    --degree 10
```

### Transfert de MySQL à MSSQL pour la table orders_part avec méthode DataDriven
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mysql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --query "select * from tpch.orders_part" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders_part" `
    --method "DataDriven" `
    --distributeKeyColumn "o_orderdate_year" `
    --degree 10
```


### Source Hyper (pgsql driver) - Target MSSQL
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:8095" `
    --sourcedatabase "D:\OpenData\TPCH\data\hyper\tpch_sf10.hyper" `
    --sourceuser "tableau_internal_user" `
    --sourcepassword "" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --query "select * from ""ORDERS""" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "None"
```

## Source MSSQL - Target MSSQL

### Transfert de MSSQL à MSSQL sans méthode spécifique
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch" `
    --sourcetrusted `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_copy" `
    --query "select * from orders" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "None"
```

### Transfert de MSSQL à MSSQL avec méthode Random
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --sourceschema "dbo" `
    --sourcetable "orders" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders_3" `
    --method "Random" `
    --distributeKeyColumn "o_orderkey" `
    --degree 12
```

### Transfert de MSSQL à MSSQL avec méthode RangeId
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --sourceschema "dbo" `
    --sourcetable "orders" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders_3" `
    --method "RangeId" `
    --distributeKeyColumn "o_orderkey" `
    --degree 12
```

### Transfert de MSSQL à MSSQL avec méthode Ntile
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch_test" `
    --sourcetrusted `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --sourceschema "dbo" `
    --sourcetable "orders" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders_3" `
    --method "Ntile" `
    --distributeKeyColumn "o_orderkey" `
    --degree 12
```

### Transfert de MSSQL à MSSQL sans méthode spécifique pour la table lineitem
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch" `
    --sourcetrusted `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_copy" `
    --query "select * from lineitem" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "lineitem" `
    --method "None"
```

### Transfert de MSSQL à MSSQL avec méthode Random pour la table lineitem
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch" `
    --sourcetrusted `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_copy" `
    --query "select * from lineitem" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "lineitem" `
    --method "Random" `
    --distributeKeyColumn "l_orderkey" `
    --degree 6
```

### Transfert de MSSQL à MSSQL sans méthode spécifique pour la table TEST_71_1M_12m
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "FASTExportData" `
    --sourcetrusted `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "FASTExportData_copy" `
    --query "select * from TEST_71_1M_12m" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "TEST_71_1M_12m" `
    --method "None"
```

### using mssql partitionning Source to mssql target (faster than insert/select if target have clustered columnstore index)
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mssql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch10_collation_bin2" `
    --sourcetrusted `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch10_collation_bin2_copy" `
    --query "select * from orders_part" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "DataDriven" `
    --distributeKeyColumn "`$PARTITION.PF_DATE(o_orderdate)" `
    --degree 10 `
    --loadmode "Truncate"
```

## Netezza to MSSQL using DataDriven on DATASLICEID
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "nzsql" `
    --sourceserver "NZSOURCESYS" `
    --sourcedatabase "TPCH" `
    --sourceuser "TPCH" `
    --sourcepassword "TPCH" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "DataDriven" `
    --distributeKeyColumn "DATASLICEID" `
    --degree 6
```

## Source Postgreql - Target Oracle orabulk
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "orabulk" `
    --targetserver "localhost:1521/ORCLPDB" `
    --targetdatabase "ORCLPDB" `
    --query "select * from tpch_10.orders" `
    --targetuser "TPCH_IN" `
    --targetpassword "TPCH_IN" `
    --targetschema "TPCH_IN" `
    --targettable "ORDERS" `
    --method "None" `
    --loadmode "Truncate" `
    --batchsize 100000
```
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "orabulk" `
    --targetserver "localhost:1521/ORCLPDB" `
    --targetdatabase "ORCLPDB" `
    --query "select * from tpch_10.orders" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetuser "TPCH_IN" `
    --targetpassword "TPCH_IN" `
    --targetschema "TPCH_IN" `
    --targettable "ORDERS" `
    --method "Ctid" `
    --degree 12 `
    --loadmode "Truncate" `
    --batchsize 100000 
```

## Source Postgreql - Target Oracle oradirect
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "oradirect" `
    --targetserver "localhost:1521/ORCLPDB" `
    --targetdatabase "ORCLPDB" `
    --query "select * from tpch_10.orders limit 10005" `
    --targetuser "TPCH_IN" `
    --targetpassword "TPCH_IN" `
    --targetschema "TPCH_IN" `
    --targettable "ORDERS" `
    --method "None" `
    --loadmode "Truncate" `
    --batchsize 1000
```

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "oradirect" `
    --targetserver "localhost:1521/ORCLPDB" `
    --targetdatabase "ORCLPDB" `
    --query "select * from tpch_10.orders" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetuser "TPCH_IN" `
    --targetpassword "TPCH_IN" `
    --targetschema "TPCH_IN" `
    --targettable "ORDERS" `
    --method "Ctid" `
    --degree 10 `
    --loadmode "Truncate" `
    --batchsize 10000
```

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:5432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "oradirect" `
    --targetserver "localhost:1521/ORCLPDB" `
    --targetdatabase "ORCLPDB" `
    --query "select * from tpch_10.orders" `
    --targetuser "TPCH_IN" `
    --targetpassword "TPCH_IN" `
    --targetschema "TPCH_IN" `
    --targettable "ORDERS" `
    --method "DataDriven" `
    --distributeKeyColumn "(EXTRACT('Year' FROM o_orderdate))" `
    --degree 7 `
    --loadmode "Truncate" `
    --batchsize 10000
```

## Source MySQL - Target Oracle oradirect
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "mysql" `
    --sourceserver "localhost" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "oradirect" `
    --targetserver "localhost:1521/ORCLPDB" `
    --targetdatabase "FREEPDB1" `
    --query "select * from tpch.orders_part" `
    --targetuser "TPCH_IN" `
    --targetpassword "TPCH_IN" `
    --targetschema "TPCH_IN" `
    --targettable "ORDERS_PART" `
    --method "DataDriven" `
    --distributeKeyColumn "o_orderdate_year" `
    --degree 10 `
    --batchsize 10000
```

## Source Oracle - Target MSSQL
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "oraodp" `
    --sourceserver "localhost:1521/ORCLPDB" `
    --sourcedatabase "ORCLPDB" `
    --query "select * from TPCH_IN.ORDERS FETCH NEXT 10 ROWS ONLY" `
    --sourceuser "TPCH_IN" `
    --sourcepassword "TPCH_IN" `
    --sourceschema "TPCH_IN" `
    --sourcetable "ORDERS" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "None" `
    --loadmode "Truncate"
```

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "oraodp" `
    --sourceserver "LOCALHOST:1521/ORCLPDB" `
    --sourcedatabase "ORCLPDB" `
    --sourceuser "TPCH_IN" `
    --sourcepassword "TPCH_IN" `
    --sourceschema "TPCH_IN" `
    --sourcetable "ORDERS_FLAT" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "Rowid" `
    --loadmode "Truncate" `
    --degree 12
```

## Source ODBC - Target MSSQL
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "odbc" `
    --sourcedsn "DSNORA23CFREEPDB1" `
    --sourcedatabase "FREEPDB1" `
    --query "select * from TPCH_IN.ORDERS FETCH NEXT 10 ROWS ONLY" `
    --sourceuser "TPCH_IN" `
    --sourcepassword "TPCH_IN" `
    --sourceschema "TPCH_IN" `
    --sourcetable "ORDERS" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders" `
    --method "None" `
    --loadmode "Truncate"
```

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "odbc" `
    --sourcename "DSNMySQLTPCH" `
    --sourcedatabase "tpch" `
    --query "select * from tpch.orders_part LIMIT 10" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --targetconnectiontype "msbulk" `
    --targetserver "localhost" `
    --targetdatabase "tpch_test" `
    --targettrusted `
    --targetschema "dbo" `
    --targettable "orders_part" `
    --method "None" `
    --loadmode "Truncate"
```

## Source Postgreql - Target HANA
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:15432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetconnectiontype "hanabulk" `
    --targetserver "hxehost:39015" `
    --targetdatabase "" `
    --targetuser "SYSTEM" `
    --targetpassword "AetP202440" `
    --targetschema "TPCH" `
    --targettable "ORDERS" `
    --method "None" `
    --loadmode "Truncate" `
    --batchsize 5000 `
    --query "select * from tpch_10.orders limit 100000"
```
``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:15432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourceschema "tpch_10" `
    --sourcetable "orders" `
    --targetconnectiontype "hanabulk" `
    --targetserver "hxehost:39015" `
    --targetdatabase "" `
    --targetuser "SYSTEM" `
    --targetpassword "AetP202440" `
    --targetschema "TPCH" `
    --targettable "ORDERS" `
    --method "Ctid" `
    --degree 4 `
    --loadmode "Truncate" `
    --batchsize 5000
```

## Source HANA - Target Postgreql
``` powershell
.\FastTransfer.exe `
    --targetconnectiontype "pgsql" `
    --targetserver "localhost:15432" `
    --targetdatabase "tpch_import" `
    --targetuser "FastUser" `
    --targetpassword "FastPassword" `
    --targetschema "tpch_10" `
    --targettable "orders" `
    --sourceconnectiontype "hana" `
    --sourceserver "hxehost:39015" `
    --sourcedatabase "" `
    --sourceuser "SYSTEM" `
    --sourcepassword "AetP202440" `
    --sourceschema "TPCH" `
    --sourcetable "ORDERS" `
    --method "Random" `
    --distributeKeyColumn "o_orderkey" `
    --degree 12 `
    --loadmode "Truncate" `
    --batchsize 5000
```

## Source Postgreql - Target clickhouse (local)

``` powershell
.\FastTransfer.exe `
    --sourceconnectiontype "pgsql" `
    --sourceserver "localhost:15432" `
    --sourcedatabase "tpch" `
    --sourceuser "FastUser" `
    --sourcepassword "FastPassword" `
    --sourceschema "tpch_10" `
    --query "select * from tpch_10.orders limit 100000" `
    --targetconnectiontype "clickhousebulk" `
    --targetserver "localhost:8123" `
    --targetdatabase "default" `
    --targetuser "default" `
    --targetpassword "jKpHQEfXC91VCWrXoMb3" `
    --targetschema "default" `
    --targettable "orders" `
    --method "None" `
    --loadmode "Truncate" `
    --batchsize 10000
```
``` powershell
.\FastTransfer.exe `
   --sourceconnectiontype "pgsql" `
   --sourceserver "localhost:15432" `
   --sourcedatabase "tpch" `
   --sourceuser "FastUser" `
   --sourcepassword "FastPassword" `
   --sourceschema "tpch_10" `
   --sourcetable "orders" `
   --targetconnectiontype "clickhousebulk" `
   --targetserver "localhost:8123" `
   --targetdatabase "default" `
   --targetuser "default" `
   --targetpassword "jKpHQEfXC91VCWrXoMb3" `
   --targetschema "default" `
   --targettable "orders" `
   --method "Ctid" `
   --degree 15 `
   --loadmode "Truncate" `
   --batchsize 1000000
```


## Source ClickHouse to Postgresql
``` powershell
.\FastTransfer.exe `
   --targetconnectiontype "pgcopy" `
   --targetserver "localhost:15432" `
   --targetdatabase "tpch" `
   --targetuser "FastUser" `
   --targetpassword "FastPassword" `
   --targetschema "tpch_10" `
   --targettable "orders_empty" `
   --sourceconnectiontype "clickhouse" `
   --sourceserver "localhost:8123" `
   --sourcedatabase "default" `
   --sourceuser "default" `
   --sourcepassword "jKpHQEfXC91VCWrXoMb3" `
   --sourceschema "default" `
   --query "select * from default.orders limit 100000" `
   --method "None" `
   --degree 15 `
   --loadmode "Truncate" `
   --batchsize 10000
```
``` powershell
.\FastTransfer.exe `
   --targetconnectiontype "pgcopy" `
   --targetserver "localhost:15432" `
   --targetdatabase "tpch" `
   --targetuser "FastUser" `
   --targetpassword "FastPassword" `
   --targetschema "tpch_10" `
   --targettable "orders_empty" `
   --sourceconnectiontype "clickhouse" `
   --sourceserver "localhost:8123" `
   --sourcedatabase "default" `
   --sourceuser "default" `
   --sourcepassword "jKpHQEfXC91VCWrXoMb3" `
   --sourceschema "default" `
   --sourcetable "orders" `
   --method "RangeId" `
   --distributeKeyColumn "O_ORDERKEY" `
   --degree 15 `
   --loadmode "Truncate" `
   --batchsize 100000
```

``` powershell
   .\FastTransfer.exe `
   --targetconnectiontype "pgcopy" `
   --targetserver "localhost:15432" `
   --targetdatabase "tpch" `
   --targetuser "FastUser" `
   --targetpassword "FastPassword" `
   --targetschema "tpch_10" `
   --targettable "orders_empty" `
   --sourceconnectiontype "clickhouse" `
   --sourceserver "localhost:8123" `
   --sourcedatabase "default" `
   --sourceuser "default" `
   --sourcepassword "jKpHQEfXC91VCWrXoMb3" `
   --sourceschema "default" `
   --sourcetable "orders" `
   --method "Ntile" `
   --distributeKeyColumn "O_ORDERKEY" `
   --degree 15 `
   --loadmode "Truncate" `
   --batchsize 100000
```
``` powershell
.\FastTransfer.exe `
   --targetconnectiontype "pgcopy" `
   --targetserver "localhost:15432" `
   --targetdatabase "tpch" `
   --targetuser "FastUser" `
   --targetpassword "FastPassword" `
   --targetschema "tpch_10" `
   --targettable "orders_empty" `
   --sourceconnectiontype "clickhouse" `
   --sourceserver "localhost:8123" `
   --sourcedatabase "default" `
   --sourceuser "default" `
   --sourcepassword "jKpHQEfXC91VCWrXoMb3" `
   --sourceschema "default" `
   --sourcetable "orders" `
   --method "Random" `
   --distributeKeyColumn "O_ORDERKEY" `
   --degree 15 `
   --loadmode "Truncate" `
   --batchsize 100000
```

``` powershell
.\FastTransfer.exe `
   --targetconnectiontype "pgcopy" `
   --targetserver "localhost:15432" `
   --targetdatabase "tpch" `
   --targetuser "FastUser" `
   --targetpassword "FastPassword" `
   --targetschema "tpch_10" `
   --targettable "orders_empty" `
   --sourceconnectiontype "clickhouse" `
   --sourceserver "localhost:8123" `
   --sourcedatabase "default" `
   --sourceuser "default" `
   --sourcepassword "jKpHQEfXC91VCWrXoMb3" `
   --sourceschema "default" `
   --sourcetable "orders" `
   --method "DataDriven" `
   --distributeKeyColumn "year(o_orderdate)" `
   --degree 15 `
   --loadmode "Truncate" `
   --batchsize 100000 
```

## source Postgreql target teradata
``` powershell
   .\FastTransfer.exe `
   --sourceconnectiontype "pgsql" `
   --sourceserver "localhost:15432" `
   --sourcedatabase "tpch" `
   --sourceuser "FastUser" `
   --sourcepassword "FastPassword" `
   --sourceschema "tpch_10" `
   --sourcetable "orders" `
   --targetconnectiontype "teradata" `
   --targetserver "192.168.239.129:1025" `
   --targetdatabase "TPCH" `
   --targetuser "UTPCH" `
   --targetpassword "UTPCH" `
   --targetschema "TPCH" `
   --targettable "orders" `
   --method "Ctid" `
   --degree 15 `
   --loadmode "Truncate" `
   --batchsize 10000
```

``` powershell
.\FastTransfer.exe `
   --sourceconnectiontype "teradata" `
   --sourceserver "192.168.239.129:1025"  `
   --sourcedatabase "TPCH" `
   --sourceuser "UTPCH" `
   --sourcepassword "UTPCH" `
   --sourceschema "TPCH" `
   --sourcetable "orders_15M" `
   --targetconnectiontype "msbulk" `
   --targetserver "localhost" `
   --targetdatabase "tpch10_collation_bin2" `
   --targetuser "FastUser" `
   --targetpassword "FastPassword" `
   --targetschema "dbo" `
   --targettable "orders_15M_copy" `
   --method "RangeId" `
   --distributeKeyColumn "o_orderkey" `
   --degree 12 `
   --loadmode "Truncate" 
```


## source mssql target duckdb
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "mssql" `
--sourceserver "localhost" `
--sourcedatabase "tpch10_collation_bin2" `
--sourceschema "dbo" `
--sourcetable "orders_1M" `
--sourcetrusted `
--targetconnectiontype "duckdb" `
--targetdatabase "tpch10_insert" `
--targetschema "tpch10" `
--targettable "orders" `
--method "None" `
--loadmode "Truncate" `
--targetserver "D:\OpenData\TPCH\data\10\duckdb\tpch10_insert.duckdb" 
```

## Source DuckDB

### using DuckDB (Memory) with a query on a json parquets and nested fields, target MSSQL

``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdb" `
--sourceserver ":memory:" `
--query "select * EXCLUDE(Risques, Interlocuteurs),unnest(interlocuteurs,recursive := true ) from (select day, unnest(contexte_chantier, recursive := true), unnest(detail_chantier, recursive := true) from read_parquet('D:\CLIENTS\ENEDIS\BI4ALL\CHANTIER\**\*.parquet', hive_partitioning=true)) t_row_unest" `
--targetconnectiontype "msbulk" `
--targetserver "localhost" `
--targettrusted `
--targetdatabase "ENDSBI4ALL" `
--targetschema "bi4all" `
--targettable "DuckChantiers_hpart" `
--method "DataDriven" `
--distributeKeyColumn "day" `
--loadmode "Truncate" `
--degree 8 `
--runid "DuckDB_Parquet_part_To_MSSQL2022_part_Parallel_DataDriven_P8"
```


### using DuckDB (Stream) with a query on 16 multiple CSV files parallel Datadriven on filename, target MSSQL

``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT * exclude filename FROM read_csv('D:\temp\FastBCP_lineitem_Extract\lineitem*.CSV', filename=true)" `
--targetconnectiontype "msbulk" `
--targetserver "localhost" `
--targettrusted `
--targetdatabase "tpch_test" `
--targetschema "dbo" `
--targettable "lineitem" `
--method "DataDriven" `
--distributeKeyColumn "filename" `
--datadrivenquery "select file from glob('D:\temp\FastBCP_lineitem_Extract\*.CSV')" `
--loadmode "Truncate" `
--degree 16 `
--runid "CSV_To_MSSQL_Parallel16_DataDriven_filename"
```

### using DuckDB (Stream) with a query on a single big CSV files parallel Random l_orderkey, target MSSQL
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT * FROM read_csv('D:\temp\lineitem*.CSV')" `
--targetconnectiontype "msbulk" `
--targetserver "localhost" `
--targettrusted `
--targetdatabase "tpch_test" `
--targetschema "dbo" `
--targettable "lineitem" `
--method "Random" `
--distributeKeyColumn "l_orderkey" `
--loadmode "Truncate" `
--degree 16 `
--runid "CSV_part_To_MSSQL2022_Parallel16_Random_l_orderkey"
```

### using DuckDB (Stream) with a query on a single big CSV files parallel DD l_orderkey slice, target MSSQL
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT * FROM read_csv('D:\temp\lineitem*.CSV') rcsv" `
--targetconnectiontype "msbulk" `
--targetserver "localhost" `
--targettrusted `
--targetdatabase "tpch_test" `
--targetschema "dbo" `
--targettable "lineitem" `
--method "DataDriven" `
--distributeKeyColumn "(l_orderkey/5000000)::int" `
--datadrivenquery "select distinct (l_orderkey/5000000)::int l_orderkey_group from read_csv('D:\temp\lineitem*.CSV') rcsv" `
--loadmode "Truncate" `
--degree 13 `
--runid "CSV_To_MSSQL2022_Parallel12_DD_l_orderkeyDiv5M"
```

### DuckDB Stream single small csv file
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT * from read_csv('D:\DATA\arborescence.csv') rcsv" `
--targetconnectiontype "msbulk" `
--targetserver "localhost" `
--targettrusted `
--targetdatabase "Edilians" `
--targetschema "dbo" `
--targettable "arborescence" `
--method "None" `
--loadmode "Truncate" `
--runid "CSV_To_MSSQL2022_SingleThread"
```


### DuckDB Stream medium small csv file
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT * from read_csv('D:\OpenData\wikidata\vector_database_wikipedia_articles_embedded.csv') rcsv" `
--targetconnectiontype "pgcopy" `
--targetserver "localhost:35432" `
--targetuser "postgresql" `
--targetpassword "DdDlOhTWliObsMYqtotl" `
--targetdatabase "wikipedia" `
--targetschema "public" `
--targettable "articles" `
--method "None" `
--loadmode "Truncate" `
--runid "CSV_To_pg17_SingleThread"
```

### DuckDB Stream medium small csv file
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT * from read_csv('D:\OpenData\wikidata\vector_database_wikipedia_articles_embedded.csv') rcsv" `
--targetconnectiontype "pgcopy" `
--targetserver "localhost:35432" `
--targetuser "postgres" `
--targetpassword "DdDlOhTWliObsMYqtotl" `
--targetdatabase "wikipedia" `
--targetschema "public" `
--targettable "articles" `
--method "DataDriven" `
--distributeKeyColumn "(id/10000)::int" `
--loadmode "Truncate" `
--degree 12 `
--runid "CSV_To_pg17_Thread12"
```

### DuckDB Stream medium small csv file with format given for the csv file
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT * FROM read_csv('D:\OpenData\wikidata\vector_database_wikipedia_articles_embedded.csv', auto_detect=false, delim=',', quote='""', escape='""', new_line='\n', skip=0, comment='', header=true, columns={'id': 'BIGINT', 'url': 'VARCHAR', 'title': 'VARCHAR', 'text': 'VARCHAR', 'title_vector': 'VARCHAR', 'content_vector': 'VARCHAR', 'vector_id': 'BIGINT'}) rcsv" `
--targetconnectiontype "pgcopy" `
--targetserver "localhost:35432" `
--targetuser "postgres" `
--targetpassword "DdDlOhTWliObsMYqtotl" `
--targetdatabase "wikipedia" `
--targetschema "public" `
--targettable "articles" `
--method "DataDriven" `
--distributeKeyColumn "(id/10000)::int" `
--loadmode "Truncate" `
--degree 12 `
--runid "CSV_To_pg17_Thread12"
```

``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT * FROM read_csv('D:\OpenData\wikidata\vector_database_wikipedia_articles_embedded.csv', auto_detect=false, delim=',', quote='""', escape='""', new_line='\n', skip=0, comment='', header=true, columns={'id': 'BIGINT', 'url': 'VARCHAR', 'title': 'VARCHAR', 'text': 'VARCHAR', 'title_vector': 'VARCHAR', 'content_vector': 'VARCHAR', 'vector_id': 'BIGINT'}) rcsv limit 100" `
--targetconnectiontype "msbulk" `
--targetserver "localhost\SS2025" `
--targettrusted `
--targetdatabase "wikipedia" `
--targetschema "dbo" `
--targettable "wikipedia_articles_embeddings_as_vector" `
--loadmode "Truncate" `
--runid "CSV_To_mssql_SingleThread"
```

### duckdb file to postgresql
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver "D:\OpenData\wikidata\dbpedia_14.duckdb" `
--query "SELECT label, title, content, split, content_word_count, chunk, content_n_chunks, chunk_index, chunk_word_count, chunk_embedding::text FROM dbpedia_14 limit 100" `
--targetconnectiontype "pgcopy" `
--targetserver "localhost:35432" `
--targetuser "postgres" `
--targetpassword "DdDlOhTWliObsMYqtotl" `
--targetdatabase "wikipedia" `
--targetschema "public" `
--targettable "dbpedia_14" `
--method "None" `
--distributeKeyColumn "(chunk_index/10000)::int" `
--loadmode "Truncate" `
--runid "DuckDB_To_pgcopy_SingleThread"
```


``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver "D:\OpenData\wikidata\dbpedia_14.duckdb" `
--sourceschema "main" `
--sourcetable "dbpedia_14" `
--query "SELECT label, title, content, split, content_word_count, chunk, content_n_chunks, chunk_index, chunk_word_count, chunk_embedding::text FROM dbpedia_14" `
--targetconnectiontype "pgcopy" `
--targetserver "localhost:35432" `
--targetuser "postgres" `
--targetpassword "DdDlOhTWliObsMYqtotl" `
--targetdatabase "wikipedia" `
--targetschema "public" `
--targettable "dbpedia_14" `
--method "Ntile" `
--distributeKeyColumn "chunk_index" `
--degree 14 `
--loadmode "Truncate" `
--runid "DuckDB_To_pgcopy_14Thread"
```

### duckdb to mssql with vector as varchar
``` powershell
.\FastTransfer.exe `
--sourceconnectiontype "duckdbstream" `
--sourceserver ":memory:" `
--query "SELECT id,url,title,text,title_vector::varchar tv,content_vector::varchar cv,vector_id from read_csv('D:\OpenData\wikidata\vector_database_wikipedia_articles_embedded.csv') limit 100" `
--targetconnectiontype "msbulk" `
--targetserver "localhost\SS2025" `
--targettrusted `
--targetdatabase "wikipedia" `
--targetschema "dbo" `
--targettable "wikipedia_articles_embeddings_as_vector" `
--loadmode "Truncate" `
--runid "CSV_To_mssql_SingleThread"
```

