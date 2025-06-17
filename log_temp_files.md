# log_temp_files

[Link](https://www.linkedin.com/posts/crunchy-data-solutions-inc-_postgres-performance-logging-tip-log-temp-activity-7340402356687183872-Uktd)

Postgres performance logging tip: log temp files. 

Why?

Ideally you set the log_temp_files to be the same size as your working memory, work_mem.  work_mem is the memory limit per operation before Postgres needs to spill to disk. If an operation fits within work_mem, the system won’t create temp files, so no logging needed. If the operation spills to disk, it creates a temp file at least as big as work_mem.  

-- log temp files >4mb in kb, set to current work_mem setting
log_temp_files = '4096'

The actual logs for temp files will look like this:

2024-05-16 14:23:05.123 UTC [12345] user@database LOG:  temporary file: path "base/pgsql_tmp/pgsql_tmp1234.0", size 245760
2024-05-16 14:23:05.123 UTC [12345] user@database DETAIL:  Sort operation used temporary file because work_mem was exceeded