Bash overlay on klog timetracker (https://github.com/jotaen/klog)

#### Warning

USE AT YOUR OWN RISK. MAKE BACKUPS OF YOUR JOURNAL.

It works well for me but it is not heavily tested against inexpected use or hostile special characters.

It was developped incrementally driven by my needs.

So it uses only a subset of klog and it is probably even incompatible with some of klog features (eg. breaks). It abuses klog tags.
Actually, it might even be rewritten as a standalone command-line time tracker soon or later.

#### Goal

I use it to finely track time spent for multiples clients and tasks with only one journal.

Configuration is set in your `$HOME/.tt`, e.g. with this content:
```
WORKFILE=/home/jeremie/workspace/klog/work.klg
EDITOR=geany
```

`tt` can also be piped to itself for advanced filtering and billing (see examples below).

#### Usage

Use `tt --help` for the latest info.

Please use only the following commands. Do not use `klog` on the journal or at least, make sure to have a backup.

The syntax of `task` below is `client=project "optional details"`

The variant of `regex` is that of `grep -E`.

  * `tt`                 show help
  * `tt task`            stop current task and start a new one
  * `tt stop`            stop current task (`tt end` is ok as well)
  * `tt resume [regex]`  restart last task, or the last task that matches the provided regex

  * `tt backup`          create a timestamped backup of your journal
  * `tt cat`             dumps current log file
  * `tt edit`            edit current log file
  * `tt replace`         only when piped: replaces current journal with the standard input (dangerous)

  * `tt today`           dumps current stats today
  * `tt bill [task]`     show time spent on task or client (exact match)

  * `tt keep [task]`     keep regex and dump a klog-compatible file
  * `tt discard [task]`  discard regex and dump a klog-compatible file
 
Examples:

```
  tt bill 'client1'           # cumulative time spent en client1
  tt bill 'client1=sysadmin'  # time spent on client1 individual tasks

  tt backup
  tt keep 'client1=(dev.*|sysadmin)'| tt bill client1 > billing_report_client1_projects_dev_and_sysadmin.txt
  tt discard 'client1=(dev.*|sysadmin)'| tt replace  # remove previous billed entries from journal
```
