# sesh

`
sesh = silent exploitation shell
| security engineering shell
| super epic shell
| stealth espionage shell
| standalone execution shell
| sexy encrypted shell
`
# a linux shell for pentetration <sub><sup><sub><sub><sup><sub><sup><sub>testing</sub></sup></sub></sup></sub></sub></sup></sub>

## features

- fully modular - enable/disable any feature at compile or runtime
- ~~total disregard for~~ active leveraging of established conventions
- does not touch disk without you knowing about it
- read and write files without changing metadata
- assume the identity of an already running process (or whatever you want it to be)
- in-memory command history
- embed arbitrary files in the binary for later use
- configuration can be saved as a short string, which can be loaded with ease
- built in enumeration scripts
- spoof running time (may need root)
- something like a cooler version of [moonwalk](https://github.com/mufeedvh/moonwalk)
- ignore SIGHUP (and/or other signals)
- cool udp and tcp revshell capability, which when combined with the previous feature, means you can ssh (or whatever) to a target, run sesh, close ssh connection, and then reconnect via a more stealthy route (alla [pwncat](https://github.com/cytopia/pwncat))
- send random data to random (or not so random) ip addresses to cover communications
- many useful tools built in, don't need to run binaries from disk, such as:
    - cat, base64, zip, tar, netcat, nano, ls, find, grep, wget, su, env, chmod, chown, chgrp, getcap, setcap, etc
    - (*note that most of these will be replaced with cool rewrites, i.e. ls->exa, find->bfs, etc. will be kinda like busybox but more based.*)
    - might also just chuck python in there

- run executables from memory, from network, or even local binaries with or without +x set
    - not sure if I can do this, but optimally, given a binary in any of the above forms, you would be able to execute them with [userland exec](https://grugq.github.io/docs/ul_exec.txt) without overwriting the original sesh process, i.e imagine you are in a sesh session, and you run `silentexec /bin/ls`, this would read the `ls` binary, execute it with userland exec, show you the output, then return you to your sesh session, all without starting or stopping any processes at all!
    - ok I thought a bit more about the above idea, and I think I can basically (before sesh performs a userland exec) patch the target binary (in memory) in such a way that rather than exiting post-execution, it instead would itself perform a userland exec to get back to sesh. This would mean losing whatever state sesh was previously in though, which might be a problem, but I could probably save the state and restore it using a method similar to that used by CryoPID.
    - alternatively perhaps I should basically somehow spin up a userland virtual machine sort of thing. I'll have to investigate that avenue.
    - less cool version: through the use of memfd, like [this](https://magisterquis.github.io/2018/03/31/in-memory-only-elf-execution.html)

- ability to start a process as a child of some arbitrary process (cursed+hard), or maybe something like [this](https://github.com/aseemjakhar/jugaad) to start the process *inside* another process without causing any issues with the original process

- awesome backdooring using *a project I haven't started writing yet*, which involves infecting preexisting executables with a self-replicating security flaw (thanks [Johnny!](https://en.wikipedia.org/wiki/John_von_Neumann))

> [!WARNING]  
> Written in Go!!!
