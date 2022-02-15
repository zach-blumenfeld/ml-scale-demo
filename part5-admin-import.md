# Part 5: Neo4j Admin Import


This section covers actually running the admin import command.  Admin import is a command line tool so no Python needed here, we can use the terminal.  

For our example it can be run like so from the shell on the local neo4j instance: 

```bash
bin/neo4j-admin import --database=ogblsc --id-type=INTEGER \
    --nodes=Paper=/data/demo-load/paper-c\\d-\\d+.csv \
    --nodes=Author=/data/demo-load/authors-\\d+.csv \
    --nodes=Institution=/data/demo-load/institution-\\d+.csv \
    --relationships=CITES=/data/demo-load/cited-\\d+.csv \
    --relationships=WRITES=/data/demo-load/writes-\\d+.csv \
    --relationships=AFFILIATED_WITH=/data/demo-load/affiliated_with-\\d+.csv
```

The above creates a new database called 'ogblsc' then loads and links all the nodes and relationships from the csv files. The regex in the csv names `\\d+`, this matches digit patterns so admin import picks up all the csvs we created in parts 3 and 4, i.e. `authors-00.csv`, `authors-01.csv`,...etc. 

Please ensure the root directory for these files aligns if you changed it in previous notebooks or moved to a different location. Also Note: If you decrease the chunk size from 20 Million in part 3, you may need to tweak the regex in the paper's csv line above to accommodate two digits after the ‘c’. 

Detailed Documentation for Admin Import can be found at https://neo4j.com/docs/operations-manual/current/tutorial/neo4j-admin-import/