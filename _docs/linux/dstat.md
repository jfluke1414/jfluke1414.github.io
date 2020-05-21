---   
order: 39   
title: (LINUX) dstat   
category: Linux   
---   
   
yum install dstat   
   
Note   
Users of Sleuthkit might find Sleuthkit's dstat being renamed to datastat to avoid a name conflict. See Debian bug #283709 for more information.   
Options   
-c, --cpu   
		enable cpu stats (system, user, idle, wait, hardware interrupt, software interrupt)   
	-C 0,3,total   
		include cpu0, cpu3 and total   
	-d, --disk   
		enable disk stats (read, write)   
	-D total,hda   
		include hda and total   
	-g, --page   
		enable page stats (page in, page out)   
	-i, --int   
		enable interrupt stats   
	-I 5,10   
		include interrupt 5 and 10   
	-l, --load   
		enable load average stats (1 min, 5 mins, 15mins)   
	-m, --mem   
		enable memory stats (used, buffers, cache, free)   
	-n, --net   
		enable network stats (receive, send)   
	-N eth1,total   
		include eth1 and total   
	-p, --proc   
		enable process stats (runnable, uninterruptible, new)   
	-r, --io   
		enable I/O request stats (read, write requests)   
	-s, --swap   
		enable swap stats (used, free)   
	-S swap1,total   
		include swap1 and total   
	-t, --time   
		enable time/date output   
	-T, --epoch   
		enable time counter (seconds since epoch)   
	-y, --sys   
		enable system stats (interrupts, context switches)   
	--aio   
	enable aio stats (asynchronous I/O)   
	--fs   
	enable filesystem stats (open files, inodes)   
	--ipc   
	enable ipc stats (message queue, semaphores, shared memory)   
	--lock   
	enable file lock stats (posix, flock, read, write)   
	--raw   
	enable raw stats (raw sockets)   
	--socket   
		enable socket stats (total, tcp, udp, raw, ip-fragments)   
	--tcp   
	enable tcp stats (listen, established, syn, time_wait, close)   
	--udp   
	enable udp stats (listen, active)   
	--unix   
	enable unix stats (datagram, stream, listen, active)   
	--vm   
	enable vm stats (hard pagefaults, soft pagefaults, allocated, free)   
	--stat1 --stat2   
		enable (external) plugins by plugin name, see PLUGINS for options   
	Possible internal stats are   
		aio, cpu, cpu24, disk, disk24, disk24old, epoch, fs, int, int24, io, ipc, load, lock, mem, net, page, page24, proc, raw, socket, swap, swapold, sys, tcp, time, udp, unix, vm   
	--list   
	list the internal and external plugin names   
	-a, --all   
		equals -cdngy (default)   
	-f, --full   
		expand -C, -D, -I, -N and -S discovery lists   
	-v, --vmstat   
		equals -pmgdsc -D total   
	--bw, --blackonwhite   
		change colors for white background terminal   
	--float   
		force float values on screen (mutual exclusive with --integer)   
	--integer   
		force integer values on screen (mutual exclusive with --float)   
	--nocolor   
		disable colors (implies --noupdate)   
	--noheaders   
		disable repetitive headers   
	--noupdate   
		disable intermediate updates when delay > 1   
	--output file   
		write CSV output to file   
