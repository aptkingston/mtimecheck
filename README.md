# mtimecheck

A simple bash script to keep local file system aware of changes on network shares.

>`mtimecheck` recursively checks a directory for it's most recently modified child. If that child's modification time is newer than the root folder, a local file operation is performed to make the local file system "aware" of new content.

### Usage

`mtimecheck [ flags ] directory1 directory2 ... directoryX`

>Run `mtimecheck --help` for a full list of of flags

### Usage for Plex
A common scenario is a Plex server which has network shares mounted for library folders. Plex's "automatically update my library" option does not work well for file system changes on network shares, and will likely not recognise new media.

Setting up `mtimecheck` as a frequent cron task can keep Plex always up to date by notifying the local file system of changes on these network shares by checking modification times, allowing Plex to see these changes and rescan the library.

### Example cron task

To check for changes every 5 minutes and log the output to `/var/log/mtimecheck.log`, add the following crontab:

`*/5 * * * * /path/to/mtimecheck -o /var/log/mtimecheck.log`