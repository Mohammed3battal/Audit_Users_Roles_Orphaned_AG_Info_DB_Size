## Script: Audit Users, Roles, Orphaned Users, and AG Info Across All User Databases

**Description**:
This script scans all online user databases (that are either standalone or where the current node is the AG primary) to collect comprehensive security and availability group information. It reports:

- Database size
- All users and their roles
- Whether a user is orphaned
- Availability Group metadata (name, primary replica, listener)

**What It Detects**:
- `IsOrphaned = 1`: The user has no matching login in `master.sys.server_principals`
- `AGName = Standalone`: The database is not part of an AG
- Other useful info: user type, role name, total users

**Use Case**:
- Identify orphaned users after database restores or failovers
- Audit user and role assignments across all databases
- Document AG topology and ownership of databases
- Prepare for migrations or disaster recovery planning

**Output Columns**:
- `DatabaseName`, `DatabaseSizeMB`
- `UserName`, `UserType`, `RoleName`
- `IsOrphaned` (0 or 1)
- `TotalUsers`
- `AGName`, `PrimaryReplica`, `ListenerName`

**Requirements**:
- SQL Server 2012 or later
- `sysadmin` or equivalent privileges
- Works in Always On AG environments and standalone instances

**Notes**:
- You can export this to a CSV or permanent table for historical tracking
