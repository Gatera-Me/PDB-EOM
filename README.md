# PDB-EOM
Oracle Enterprise Manager (OEM) is a comprehensive management tool provided by Oracle for monitoring and managing Oracle databases, applications, and systems.A Pluggable Database (PDB) is a portable, self-contained database that resides within a Container Database (CDB) in Oracle's Multitenant architecture, introduced with Oracle Database 12c.

## Task 1: Create a New Pluggable Database (PDB)

### SQL Command to Create PDB
To create a new Pluggable Database named `plsql_class2024db`, the following command was executed:

```sql
CREATE PLUGGABLE DATABASE plsql_class2024db 
ADMIN USER ir_plsqlauca IDENTIFIED BY [your_password]
FILE_NAME_CONVERT = ('C:\app\oradata\XE\pdbseed', 'C:\app\oradata\XE\plsql_class2024db');

Pluggable database created.

CREATE PLUGGABLE DATABASE ir_to_delete_pdb 
ADMIN USER ir_plsqlauca IDENTIFIED BY [your_password]
FILE_NAME_CONVERT = ('C:\app\oradata\XE\pdbseed', 'C:\app\oradata\XE\ir_to_delete_pdb');

Pluggable database created.
ALTER PLUGGABLE DATABASE ir_to_delete_pdb OPEN;
Pluggable database altered.

ALTER PLUGGABLE DATABASE ir_to_delete_pdb CLOSE;
Pluggable database altered.


DROP PLUGGABLE DATABASE ir_to_delete_pdb INCLUDING DATAFILES;
Pluggable database dropped.


