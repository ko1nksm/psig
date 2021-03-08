# psig

Print signal mask.

## Requirements

- Linux / Unix (not tested) that has procfs.
- POSIX shell (dash, bash, ksh, zsh, etc.)
- `tr`, `kill`

Does not work with WSL1.

## Usage

```console
Usage: psig [options]... [<pid> | 0 | -]...
Usage: psig -d

  0: current proccess id
  -: parent proccess id
  no arguments: same as 'psig -'

Options:
  -g, --pgroup      Specify as a process group id
  -s, --session     Specify as a session id
  -c, --capability  Include capability
  -d, --decode      Decodes the status file read from stdin
  -h, --help        Display help
```

## Example

```console
$ psig
Name:bash State:S (sleeping) PPID:17480 PID:17481 PGID:17481 SigQ:0/99217
Command: -bash
SigBlk: 17:CHLD
SigIgn: 3:QUIT 20:TSTP 21:TTIN 22:TTOU 34:RTMIN
SigCgt: 1:HUP 2:INT 4:ILL 5:TRAP 6:ABRT 7:BUS 8:FPE 10:USR1 11:SEGV 12:USR2 13:PIPE 14:ALRM 15:TERM 17:CHLD 24:XCPU 25:XFSZ 26:VTALRM 28:WINCH 31:SYS
```

```console
$ psig 17481 0
Name:bash State:S (sleeping) PPID:17480 PID:17481 PGID:17481 SigQ:0/99217
Command: -bash
SigBlk: 17:CHLD
SigIgn: 3:QUIT 20:TSTP 21:TTIN 22:TTOU 34:RTMIN
SigCgt: 1:HUP 2:INT 4:ILL 5:TRAP 6:ABRT 7:BUS 8:FPE 10:USR1 11:SEGV 12:USR2 13:PIPE 14:ALRM 15:TERM 17:CHLD 24:XCPU 25:XFSZ 26:VTALRM 28:WINCH 31:SYS

Name:psig State:R (running) PPID:17481 PID:18494 PGID:18494 SigQ:0/99217
Command: /bin/sh /home/koichi/bin/psig 17481 0
SigIgn: 34:RTMIN
SigCgt: 2:INT 17:CHLD
```

```console
$ echo 'SigBlk: 0000000000002000' | psig -d
SigBlk: 14:ALRM

$ psig -d
Press CTRL-D when you have finished entering the data.
SigBlk: 0000000000002000
SigBlk: 14:ALRM
```
