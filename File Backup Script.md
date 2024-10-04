## 1. File Backup Script


```bash
#!/bin/bash

backup_dir="/path/to/backup"
source_dir="/path/to/source"

# Create a timestamped backup of the source directory
tar -czf "$backup_dir/backup_$(date +%Y%m%d_%H%M%S).tar.gz" "$source_dir"
```

### Explanation:
1. **`backup_dir` and `source_dir`**: Set the paths where the backup will be stored and the directory to be backed up.
2. **`tar -czf`**: The `tar` command creates a compressed `.tar.gz` archive. The options used:
   - `-c`: Create a new archive.
   - `-z`: Compress the archive using `gzip`.
   - `-f`: Specify the name of the archive file.
3. **`$(date +%Y%m%d_%H%M%S)`**: This inserts the current timestamp (Year, Month, Day, Hour, Minute, Second) into the filename.
4. **`"$source_dir"`**: The source directory is enclosed in quotes to handle spaces or special characters.

This will create a backup in the specified `backup_dir` with the timestamp appended to the filename.
