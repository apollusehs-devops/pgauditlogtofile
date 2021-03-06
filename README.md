# pgAudit Log to File

[pgAudit Log to File](https://github.com/fmbiete/pgauditlogtofile) is an addon to [pgAudit](https://www.pgaudit.org/) than will redirect audit log lines to an independent file, instead of using PostgreSQL server logger.

This will allow us to have an audit file that we can easily rotate without polluting server logs with those messages.

Audit logs in heavily used systems can grow very fast. This extension allows to automatically rotate the files based in a number of minutes.

## Build
```
make install USE_PGXS=1
```

## Installation
- Build the extension
- Inside PostgreSQL

```
postgres=# CREATE EXTENSION pgauditlogtofile;
```

## Configuration

### pgaudit.log_directory
Name of the directory where the audit file will be created.

**Default**: 'log'

Empty or NULL will disable the extension and the audit logging will be done to PostgreSQL server logger.

### pgaudit.log_filename
Name of the file where the audit will be written. Writing to an existing file will append the new entries.

This variable can contain time patterns up to minute to allow automatic rotation.

**Default**: 'audit-%Y%m%d_%H%M.log'

Empty or NULL will disable the extension and the audit logging will be done to PostgreSQL server logger.

### pgaudit.log_rotation_age
Number of minutes after which the audit file will be rotated.

**Default**: 1440 minutes (1 day)

0 will disable the rotation


### Test
```
cd test
vagrant plugin install vagrant-vbguest
vagrant up
```
