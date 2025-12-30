# Oracle-PDB-Migration-UNIORA-to-OCI
This project involves the ongoing migration of 72 Oracle Pluggable Databases (PDBs) from an existing environment to Oracle Cloud Infrastructure (OCI).  The migration is being executed in a high-scale, multi-tenant architecture, where stability, sequencing, and validation are more critical than raw execution speed.

This migration was executed following the official corporate runbook and 
operational procedures documented in Confluence.

The logical design and baseline architecture were predefined as part of 
the organization’s standard Oracle-to-OCI migration framework.

My responsibility focused on the execution, validation, and operational 
delivery of each migration, ensuring accuracy, consistency, and production 
readiness across multiple PDBs.

### 1. Source Environment Preparation and Freeze (UNIORA)

The migration process begins with a controlled preparation phase to ensure data consistency and operational safety.

Activities performed:

Connection to the source PDB as SYS using SQL Developer

Secure access to the UNIORA21 database host via terminal

Execution of a FULL Oracle Data Pump export, including:

Exclusion of statistics and grants

Generation of dump and log files

Upload of the dump file to OCI Object Storage

Removal of the local dump to free disk space

During this phase:

The export script provides operational guidance for subsequent steps

Export logs are monitored until successful completion

Objective:
Ensure a consistent, portable database snapshot before any structural changes.

### 2. Controlled Shutdown of the Source PDB

After export completion:

All active user sessions are terminated

The PDB is closed from the CDB level, ensuring:

Immediate session termination

State cleanup

Safe PDB closure

Objective:
Prevent concurrent writes and guarantee integrity of the exported data.

### 3. Target PDB Provisioning on OCI

In the OCI environment:

Administrative access to the OCI console

Selection of the UNIORA21 CDB

Cloning of the standard baseline PDB (UNILIMSPADRAO)

Creation of the target PDB using the same logical name as the source

The cloning process is monitored until full completion.

Objective:
Provision a structurally compatible PDB prior to data import.

### 4. Security and Access Preparation on Target PDB

On the newly created PDB:

SYS-level administrative access

Creation of the DB_OWNER account

Controlled assignment of:

Administrative roles

Data Pump privileges

Scheduler and integration permissions

Required access for AWS and OCI integrations

Additionally:

Creation of functional roles (DBA and READONLY)

Alignment with corporate UniLIMS security standards

Objective:
Ensure the PDB is fully prepared to receive data and operate under enterprise security policies.

### 5. Database Import on OCI

From the OCI CDB host:

Execution of an automated procedure that:

Generates the required tnsnames.ora entries

Downloads the dump from OCI Object Storage

Performs a FULL Data Pump import

Post-import:

Detailed analysis of import logs

Expected warnings (grants and invalid objects) are reviewed

Critical issues are remediated before proceeding

Objective:
Restore the database logically while preserving structure and data integrity.

### 6. Post-Import Adjustments and Optimization

Following data restoration:

Cleanup and resizing of the temporary tablespace

Connection to the PDB using the OWNER account

Execution of standardized post-migration scripts, including:

Application parameter configuration

Context and environment adjustments

Update of URLs, services, proxies, and integrations

Recreation of users, permissions, DB Links, and scheduled jobs

Compilation of invalid objects

Objective:
Align the restored database with the operational standards of the OCI environment.

### 7. Technical and Functional Validation

Validation activities include:

Email service testing

Web service and report execution

Verification of invalid objects

End-to-end connectivity testing

On the UniWinAplic application server:

Update of tnsnames.ora

Redirection to the OCI database endpoint

Registration of the new PDB service if required

Objective:
Confirm the environment is fully functional from a technical perspective.

### 8. Application and Service Integration

Execution of the MobService build via Jenkins

Restart of required application services

Functional validation through:

Web access

Mobile access

Core UniX application workflows

Objective:
Validate full application integration with the migrated database.

### 9. Go-Live and Migration Closure

After successful validation:

Update of the Keeper system, officially moving the environment from UNIORA to OCI

Final endpoint redirection

Confirmation of production access via the official portal

## Objective:
Complete the migration and place the environment into official production operation.

<img width="1895" height="857" alt="image" src="https://github.com/user-attachments/assets/8c6be2f7-54b1-4015-82e1-7dc758173355" />


