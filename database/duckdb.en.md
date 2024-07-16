### DuckDB 
 - A in-process analytical database.
 - DuckDB v1.0.0 was released in June 2024.

### Python usage

 - Local installation
 ```
 $ pip install duckdb
 ```
 ```
 Defaulting to user installation because normal site-packages is not writeable
 Collecting duckdb
 Downloading duckdb-1.0.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (18.5 MB)
 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 18.5/18.5 MB 5.3 MB/s eta 0:00:00
 Installing collected packages: duckdb
 Successfully installed duckdb-1.0.0
 ```
### Access

  - 1) Hugging Face dataset
    - Hugging Face access token
    ```
    hf_tk = 'hf_*******************'
    ```
    - DuckDB connection
    ```
    conn = duckdb.connect()
    conn.execute("CREATE SECRET hf_token (TYPE HUGGINGFACE, TOKEN {0});".format(hf_tk_data))
    ```
    - DuckDB HTTPFS libraries

    ```
    conn.execute("INSTALL httpfs;")
    <duckdb.duckdb.DuckDBPyConnection object at 0x7fef109a73b0>
    conn.execute("LOAD httpfs;") 
    <duckdb.duckdb.DuckDBPyConnection object at 0x7fef109a73b0>    
    ```

    - DuckDB queries
    ```
    httpfs_ds = 'hf://datasets/strauss-oak/fin/fin-expenses.csv'
    statement = "SELECT * FROM '{0}'".format(httpfs_ds)
    conn.sql(statement)
    ```
    ```    
    ```

### References
 - DuckDB - [https://duckdb.org/]
