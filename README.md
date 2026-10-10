# PostgreSQL Backup, PITR and Replication Lab

1. Logical backup with `pg_dump -Fc`, verified with `pg_restore` into `bootcamp_check`
2. WAL archiving (`wal_level=replica`, `archive_mode=on`) and `pg_basebackup`
3. Point-in-time recovery to 2026-10-10 18:03:13+03, just before `DELETE FROM students`
4. Streaming standby on port 5433 using the `replicator` role
5. Monitoring with `pg_stat_replication` (state = streaming, lag_bytes = 0)

## Lessons learned
- The recovery target time must fall inside the archived WAL range, or recovery fails.
- On Ubuntu, WAL is archived to a `postgres`-owned folder, not the home directory.
- A standby is read-only: writes fail with "cannot execute DELETE in a read-only transaction".
