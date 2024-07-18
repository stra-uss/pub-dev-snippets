### Databases

##### 1. DuckDB


<script src="https://gist.github.com/stra-uss/f0ba27058beccdb6b33b83a83ca1b5b0.js"></script>

{% gist f0ba27058beccdb6b33b83a83ca1b5b0 %}




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
    __Hugging Face access token__

    

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
    100% ▕████████████████████████████████████████████████████████████▏ 
┌──────────┬────────────┬──────────────────────┬──────────┬──────────────────────┬───┬──────────────────────┬─────────────────────┬──────────────┬───────────────┬────────┬──────────────────────┐
│ column00 │   alu_id   │       alu_nome       │ alu_sexo │     alu_endereco     │ … │      alu_email       │ alu_data_nascimento │ pro_latitude │ pro_longitude │ tur_id │ progresso_alfabeti…  │
│  int64   │   int64    │       varchar        │ varchar  │       varchar        │   │       varchar        │        date         │    double    │    double     │ int64  │        int64         │
├──────────┼────────────┼──────────────────────┼──────────┼──────────────────────┼───┼──────────────────────┼─────────────────────┼──────────────┼───────────────┼────────┼──────────────────────┤
│        0 │ 3011133716 │ Enrico da Rocha      │ F        │ Travessa de Nunes,…  │ … │ evelyncaldeira@exa…  │ 2017-09-15          │     -0.71667 │     -48.52333 │      4 │                    1 │
│        1 │ 2777938602 │ Maria Sophia Costela │ M        │ Passarela de Souza…  │ … │ danielacardoso@exa…  │ 2016-07-23          │    -25.42944 │     -50.00639 │     53 │                    8 │
│        2 │ 1473623193 │ Letícia Cardoso      │ M        │ Viaduto João Felip…  │ … │ claricemendes@exam…  │ 2015-07-11          │    -14.66463 │     -52.35558 │    159 │                    9 │
│        3 │ 1092234402 │ Sophia Nunes         │ F        │ Pátio de Silva, 93…  │ … │ goncalveseloah@exa…  │ 2017-12-05          │    -28.44917 │         -52.2 │     69 │                    8 │
│        4 │ 1732375819 │ Melissa Santos       │ M        │ Rodovia Aragão, 85…  │ … │ rochaantonio@examp…  │ 2017-08-22          │     -8.28333 │     -35.03333 │     14 │                    7 │
│        5 │  214673810 │ Lavínia Moraes       │ F        │ Esplanada Nicole R…  │ … │ pedro-miguel79@exa…  │ 2015-04-04          │    -21.42917 │     -45.94722 │     41 │                    2 │
│        6 │   88279296 │ Srta. Ana Lívia No…  │ M        │ Área Fernandes, 16…  │ … │ heitorteixeira@exa…  │ 2015-03-20          │    -23.44361 │     -51.87389 │      2 │                    2 │
│        7 │ 2787938349 │ Davi Luiz Peixoto    │ F        │ Núcleo de Porto, 7…  │ … │ barbara02@example.…  │ 2015-05-16          │     -4.16694 │      -40.7475 │    155 │                    8 │
│        8 │ 1275133968 │ Joana Vieira         │ F        │ Jardim de Moraes C…  │ … │ nascimentojoao-gab…  │ 2017-06-06          │    -17.74431 │     -48.62789 │     43 │                    5 │
│        9 │ 2216555963 │ Lucas Martins        │ F        │ Lagoa Fernanda da …  │ … │ da-cruzdanilo@exam…  │ 2018-02-26          │     -4.42472 │     -41.45861 │     64 │                    8 │
│        · │      ·     │       ·              │ ·        │          ·           │ · │          ·           │     ·               │         ·    │          ·    │      · │                    · │
│        · │      ·     │       ·              │ ·        │          ·           │ · │          ·           │     ·               │         ·    │          ·    │      · │                    · │
│        · │      ·     │       ·              │ ·        │          ·           │ · │          ·           │     ·               │         ·    │          ·    │      · │                    · │
│      990 │ 1665808742 │ Amanda Nogueira      │ M        │ Esplanada de Ferna…  │ … │ jesusjoao-pedro@ex…  │ 2017-06-28          │    -22.57306 │      -47.1725 │     85 │                    9 │
│      991 │ 2204222886 │ Ana Lívia Monteiro   │ M        │ Largo Danilo Lima,…  │ … │ joao-lucasmoraes@e…  │ 2015-05-22          │     -3.14306 │     -58.44417 │      2 │                    3 │
│      992 │   31406416 │ Ana Clara Mendes     │ F        │ Sítio Davi Azevedo…  │ … │ lcaldeira@example.…  │ 2018-09-22          │    -19.72806 │     -50.19556 │     14 │                    5 │
│      993 │  214792702 │ Vitória Jesus        │ F        │ Área Pereira, 88 V…  │ … │ fernandarocha@exam…  │ 2015-12-26          │    -10.95817 │     -38.79084 │    160 │                    4 │
│      994 │ 1787745023 │ Dr. Bernardo Pereira │ M        │ Aeroporto de Sales…  │ … │ ana-claramoura@exa…  │ 2016-05-03          │    -20.87306 │     -48.29694 │     34 │                    4 │
│      995 │ 1613201536 │ Carlos Eduardo da …  │ M        │ Rodovia Ana Júlia …  │ … │ ana-laura60@exampl…  │ 2017-12-28          │       -28.24 │     -48.67028 │     52 │                    1 │
│      996 │  309198715 │ Luiz Otávio da Rosa  │ F        │ Distrito Melissa O…  │ … │ almeidaotavio@exam…  │ 2016-06-29          │     -8.76194 │     -63.90389 │    165 │                    1 │
│      997 │ 3192587622 │ Benjamin Viana       │ M        │ Alameda Mariane Ca…  │ … │ luanaribeiro@examp…  │ 2015-07-08          │       -28.24 │     -48.67028 │      1 │                    7 │
│      998 │ 2693276028 │ Evelyn Silva         │ M        │ Parque de Santos, …  │ … │ xvieira@example.net  │ 2017-02-26          │    -21.42917 │     -45.94722 │     66 │                    2 │
│      999 │ 1637466040 │ Maria Aragão         │ F        │ Rua Martins, 16 Mi…  │ … │ rafaelpereira@exam…  │ 2017-10-29          │    -22.57306 │      -47.1725 │     88 │                    7 │
├──────────┴────────────┴──────────────────────┴──────────┴──────────────────────┴───┴──────────────────────┴─────────────────────┴──────────────┴───────────────┴────────┴──────────────────────┤
│ 1000 rows (20 shown)                                                                                                                                                     15 columns (11 shown) │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘

    ```

### References
 - DuckDB - [https://duckdb.org/]
