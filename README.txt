JAYCIE RABY | CIS 450 | WINTER 2019
-----------------------------------------------------------------------------------------------------

PROJECT 2: DATE SYSTEM CALL

-----------------------------------------------------------------------------------------------------
Date System Call
	Your task is to add a new system call to xv6. The main point of the exercise is for you to see
	some of the different pieces of the system call machinery. Your new system call will get the
	current UTC time and return it to the user program. You may want to use the helper
	function, cmostime() (defined in lapic.c), to read the real time clock. date.h contains
	the definition of the struct rtcdate struct, which you will provide as an argument
	to cmostime() as a pointer.

You should create a user-level program that calls your new date system call; here's some source
you should put in date.c:

	#include "types.h"
	#include "user.h"
	#include "date.h"
	int
	main(int argc, char *argv[])
	{
		struct rtcdate r;
		if (date(&r)) {
		printf(2, "date failed\n");
		exit();
	}
	// print the time as a formatted string
	printf(1, "%d-%d-%d %d:%d:%d\n",
	r.month, r.day, r.year, r.hour, r.minute, r.second);
	exit();
}

In order to make your new date program available to run from the xv6 shell, add _date to
the UPROGS definition in Makefile.

Your strategy for making a date system call should be to clone all of the pieces of code that are
specific to some existing system call, for example the "uptime" system call. 

You should grep for uptime in all the source files, using grep -n uptime *.[chS]. 

The files you need to modify include: user.h, usys.S, syscall.c, syscall.h, sysproc.c.

The main implementation of date system call should be put in the sysproc.c file, named as
int sys_date(void). To fetch a pointer argument in a system call, you will need to use
the helper function, argptr (read sysfile.c for its usage examples).
When you're done, typing date to an xv6 shell prompt should print the current UTC time.
-----------------------------------------------------------------------------------------------------