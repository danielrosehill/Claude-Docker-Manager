# Docker Volume Backup Assistant

Help the user backup Docker volumes and container data.

## Analysis Phase

1. **List Volumes**: Run `docker volume ls --format "{{.Name}}\t{{.Driver}}"`
2. **Show Volume Details**: For each important volume, show `docker volume inspect {volume}`
3. **Identify Mounted Volumes**: Check running containers for bind mounts and named volumes

## Backup Options

### Option 1: Volume Tarball Backup
Create a tarball of volume data:
```bash
docker run --rm -v {volume_name}:/data -v {backup_path}:/backup alpine tar czf /backup/{volume_name}-$(date +%Y%m%d).tar.gz -C /data .
```

### Option 2: Container-Specific Backup
For databases and applications with built-in backup:
- PostgreSQL: `pg_dump`
- MySQL/MariaDB: `mysqldump`
- MongoDB: `mongodump`
- Redis: RDB/AOF files

### Option 3: Rsync to NAS/Remote
If NAS is configured, rsync volume data to remote storage.

## Backup Location

Ask the user where to store backups:
- Local directory
- NAS (if available at 10.0.0.50)
- Cloud storage (Wasabi if configured)

## Documentation

After backup, update `context/volumes/backup-log.md` with:
- What was backed up
- Backup location
- Timestamp
- Backup size
