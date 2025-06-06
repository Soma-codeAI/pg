## File based replication
```
# Switch WAL files in Postgres
select pg_switch_wal();

# Switch Standby PG to primary 
select pg_promote()

select pg_start_backup();
select pg_stop_backup();
```

## Streaming replication 
```
- Wal_level: Replica 
- Wal_log_hints=on (pg_rewind)
- Max_Wal_senders = int
- Wal_keep_segments = 
- hot_standby = on

select pg_create_physical_replication_slot ('Standby');
select * from pg_replication_slots;
select pg_drop_replication_slot('Standby');
select pg_create_logical_replication_slot('Standby')
```

### Monitoring 
```
select * from pg_stat_replication_view;
select pg_is_in_recovery();
select * from pg_last_wal_receive_lsn();
select * from pg_last_wal_replay_lsn();
select * from pg_last_xact_replay_timestamp();
```

```
Alter ststen set synchronous_standby_names to '*';
```

selec```
1) Using pg_ctl 
 ./pg_ctl promote -D <data directory>
2) Using trigger file in the path specified by promote_trigger_file
3) Using SQL `select pg_promote()`
```

# [  
PostgreSQL Database Administration on Windows/Linux- Part 2](https://fiserv.udemy.com/course/postgresql-v12-database-administration-on-winlinux-part-2/)
