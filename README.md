# PDB-EOM
Oracle Enterprise Manager (OEM) is a comprehensive management tool provided by Oracle for monitoring and managing Oracle databases, applications, and systems.A Pluggable Database (PDB) is a portable, self-contained database that resides within a Container Database (CDB) in Oracle's Multitenant architecture, introduced with Oracle Database 12c.

Attempt to select the instance name from v$instance
SQL> select instance from v$instance;
select instance from v$instance
       *
ERROR at line 1:
ORA-00904: "INSTANCE": invalid identifier

-- Corrected query to select the instance name
SQL> select instance_name from v$instance;

INSTANCE_NAME
----------------
orcl1

-- Show the current container name
SQL> show con_name;

CON_NAME
------------------------------
CDB$ROOT

-- Show all pluggable databases (PDBs)
SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO

-- Select the PDB name and status from the CDB view
SQL> select pdb_name, status from cdb_pdbs;

PDB_NAME
--------------------------------------------------------------------------------
STATUS
----------
PDB$SEED
NORMAL

-- Show the database name and its open mode
SQL> SELECT NAME, OPEN_MODE FROM V$DATABASE;

NAME      OPEN_MODE
--------- --------------------
ORCL1     READ WRITE

-- Retrieve specific database parameters
SQL> SELECT NAME, VALUE FROM V$PARAMETER WHERE NAME IN ('db_create_file_dest', 'control_files', 'db_recovery_file_dest');

NAME
--------------------------------------------------------------------------------
VALUE
--------------------------------------------------------------------------------
control_files
D:\ORACLE1\ORADATA\ORCL1\CONTROLFILE\O1_MF_MHM32NJW_.CTL, D:\ORACLE1\FRA\ORCL1\C
ONTROLFILE\O1_MF_MHM32NRP_.CTL

db_create_file_dest
D:\Oracle1\oradata

db_recovery_file_dest
D:\Oracle1\fra

NAME
--------------------------------------------------------------------------------
VALUE
--------------------------------------------------------------------------------

-- Create a new pluggable database named pdb1 with admin user
SQL> CREATE PLUGGABLE DATABASE pdb1
  2     ADMIN USER pdbadmin IDENTIFIED BY gatera;

Pluggable database created.

-- Create another pluggable database named plsql_class2024db with admin user
SQL> create pluggable database plsql_class2024db admin user pdbadmin identified by gatera;

Pluggable database created.

-- Commit the changes made (if any)
SQL> commit;

Commit complete.

-- Show updated list of PDBs
SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 PLSQL_CLASS2024DB              MOUNTED
         4 PDB1                           MOUNTED

-- Open all pluggable databases
SQL> ALTER PLUGGABLE DATABASE ALL OPEN;

Pluggable database altered.

SQL>
-- Show the updated status of PDBs
SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 PLSQL_CLASS2024DB              READ WRITE NO
         4 PDB1                           READ WRITE NO

-- Select the name and open mode of all PDBs
SQL> SELECT name, open_mode FROM v$pdbs;

NAME
--------------------------------------------------------------------------------
OPEN_MODE
----------
PDB$SEED
READ ONLY

PLSQL_CLASS2024DB
READ WRITE

PDB1
READ WRITE

-- Set the current session to the plsql_class2024db PDB
SQL> ALTER SESSION SET CONTAINER = plsql_class2024db;

Session altered.

-- Create a new user in the current PDB
SQL> CREATE USER ir_plsqlauca IDENTIFIED BY gatera;

User created.

-- Grant all privileges to the newly created user
SQL> GRANT all privileges to ir_plsqlauca;

Grant succeeded.

-- Commit the changes made (if any)
SQL> commit;

Commit complete.

-- Show the current container name
SQL> show con_name;

CON_NAME
------------------------------
CDB$ROOT

-- Create a new pluggable database named ir_to_delete_pdb with admin user
SQL> CREATE PLUGGABLE DATABASE ir_to_delete_pdb
  2     ADMIN USER pdbadmin IDENTIFIED BY gatera;

Pluggable database created. -- The pluggable database is created

-- Drop the pluggable database ir_to_delete_pdb including its datafiles
SQL> DROP PLUGGABLE DATABASE ir_to_delete_pdb INCLUDING DATAFILES;

Pluggable database dropped.

