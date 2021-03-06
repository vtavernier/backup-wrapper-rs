# backup-wrapper-rs

backup-wrapper-rs is a binary that runs the selected backup backend with
arguments corresponding to directories that have been found under a common
root, with the xattr `user.backup = 1`.

Example systemd unit to run a backup with the rights to read any file:

	[Unit]
	Description=Backup tagged directories using backup-wrapper
	After=network.target
	Requires=network.target
	
	[Service]
	ExecStart=/usr/local/bin/backup-wrapper duplicity -r /backup-root -k GPG-KEY-ID -t some://backup-url full
	CapabilityBoundingSet=CAP_DAC_READ_SEARCH
	
	[Install]
	WantedBy=multi-user.target

## Usage

```
~ $ backup-wrapper duplicity -r /backup-root -k GPG-KEY-ID -t some://backup-url full
~ $ backup-wrapper duplicity -r /backup-root -k GPG-KEY-ID -t some://backup-url incremental
~ $ backup-wrapper restic -r /backup-root -p PASSWORD-FILE backup
```

## License

This program is available under the terms of the [MIT License](LICENSE).

## Author

Vincent Tavernier <vince.tavernier@gmail.com>
