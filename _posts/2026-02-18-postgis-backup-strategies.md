---
layout: post
title: "Backup and Restore Strategy for Large PostGIS Clusters"
date: 2026-02-18
author: PGCare
tags: [postgresql, administration, performance,postgis]
excerpt: "Logical dumps don’t scale for large PostGIS databases. This post breaks down physical backup strategy, WAL explosion risks, replication slot pitfalls, and why restore-time validation matters more than backup frequency in enterprise spatial systems "
---
# Backup and Restore Strategy for Large PostGIS Clusters

Backing up a 50GB database is routine.

Backing up a 2TB PostGIS cluster is infrastructure engineering.

PostGIS changes backup planning because:

- Rows are larger
- WAL volume is higher
- TOAST tables grow aggressively
- Restore time is rarely linear

This post focuses purely on operational reality.

---

# 1️ Why Logical Dumps Stop Making Sense

Check database size:

```sql
SELECT pg_size_pretty(pg_database_size(current_database()));
````

If your PostGIS database is:

* > 300GB → pg_dump becomes slow
* > 500GB → restore time becomes operationally risky
* > 1TB → logical restore is rarely acceptable for RTO

Why?

Because logical dump:

* Recreates schema
* Replays inserts row by row
* Rebuilds GIST indexes from scratch
* Generates additional WAL during restore

Spatial indexes are expensive to rebuild.

In real systems, a 1.5TB logical restore can take **10–20 hours**.

That is not DR. That is downtime.

---

# 2 Physical Backup Is the Baseline

For large PostGIS clusters, physical backup is mandatory.

### Base Backup

```bash
pg_basebackup -D /backup/full -Fp -Xs -P
```

Important flags:

* `-Fp` → plain format (filesystem copy)
* `-Xs` → stream WAL
* `-P` → progress

At multi-terabyte scale:

* Network throughput becomes limiting factor
* Disk IOPS on source matter
* Backup duration must be measured under load

Do not measure base backup on idle systems.

---

# 3 WAL Archiving Is Not Optional

Enable WAL archiving:

```conf
archive_mode = on
archive_command = 'cp %p /archive/%f'
```

For PostGIS systems, monitor archive volume:

```bash
du -sh /archive/
```

Spatial workloads generate more WAL because:

* Geometry updates log full rows
* TOAST data logged
* GIST index updates logged

If archive disk fills:
Primary stops.

Always monitor:

* Archive directory growth
* Replication slot retention
* WAL generation spikes during spatial batch jobs

---

# 4 Replication Slots: Hidden Disk Risk

If using streaming replication or logical slots:

```sql
SELECT slot_name,
       pg_size_pretty(
         pg_wal_lsn_diff(pg_current_wal_lsn(), restart_lsn)
       ) AS retained_wal
FROM pg_replication_slots;
```

If subscriber is slow:

* WAL accumulates
* Disk fills
* Primary crashes

In PostGIS clusters, this can happen faster due to large row size.

Alert on retained WAL size, not just replication delay in seconds.

---

# 5 Restore Time Is the Real KPI

Everyone measures backup success.

Few measure restore time.

Restore consists of:

1. Copy base backup to new node
2. Start recovery
3. Replay WAL
4. Load extensions
5. Warm cache
6. Application reconnect

Measure actual restore time:

```bash
time rsync -av /backup/full/ /var/lib/pgsql/data/
```

Then measure WAL replay duration from logs.

For 2TB clusters, realistic restore time is often:

* 2–6 hours minimum
* Longer under heavy WAL backlog

If your RTO expectation is 30 minutes,
and you have never tested full restore,
you are assuming.

---

# 6 PostGIS-Specific Restore Considerations

PostGIS is not just tables.

After restore, verify:

```sql
SELECT extname, extversion
FROM pg_extension
WHERE extname = 'postgis';
```

Confirm:

* Extension loads successfully
* GEOS / PROJ libraries match
* No missing shared library errors

OS-level mismatch can break spatial functions even if restore succeeds.

---

# 7 Backup Strategy Pattern That Works

For large PostGIS clusters:

* Weekly full base backup
* Continuous WAL archiving
* Replication standby for fast failover
* Quarterly full restore testing
* WAL retention sized for worst-case replay window

Never rely on a single method.

---

# 8 What Actually Fails in Real Incidents

In real production incidents, failures are rarely:

* Corrupted geometry
* Broken spatial queries

They are:

* Disk full due to WAL retention
* Backup incomplete due to IO bottleneck
* Restore too slow for SLA
* Archive directory filling silently

Backup strategy is capacity engineering, not checkbox compliance.

---

# Final Operational Principle

If you have never:

* Restored your full multi-TB PostGIS cluster
* Measured end-to-end restore time
* Validated extension loading post-restore
* Simulated WAL-heavy recovery

Then you do not know your disaster recovery capability.

You only have backups.

In large PostGIS systems,
restore predictability matters more than backup frequency.
