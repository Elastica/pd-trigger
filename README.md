pd-trigger
====================

A lightweight, portable, and robust PagerDuty trigger utility.
---------------------

The pd-trigger  utility can be used to trigger PD incidents, straight from the
shell, or any program.  pd-trigger is written in portable Bourne-ish sh(1).

  https://developer.pagerduty.com/documentation/integration/events/trigger

### Dependencies

pd-trigger depends on the *curl(1)* utility, but is otherwise quite portable.

The authors are using it on the following platforms:

-   FreeBSD
-   Debian/Ubuntu Linux
-   OSX/Darwin

pd-trigger should work well on the following platforms as well,

-    OpenBSD
-    CentOS/RHEL 
-    NetBSD
-    Illumos/Solaris
-    DragonFlyBSD

Can be run from cron(1), called from other UNIX programs, and receive stdout in pipes from other programs, as plain text.


### Installation

pd-trigger is a very self-contained utility, and can be installed a number of different ways.  A simple installer is included:

    $ ./install

If you run the installer as root, it will attempt to install into
/usr/local/bin by default.  If any other user, it will attempt to
install ~/bin for that user.  There are ENV overrides to allow 
changing install location, among other install details- read the
script for more info.

    
### Examples

prints help page,

    $ pd-trigger -h

writes stock config file to stdout,
(create a PagerDuty Service Key and add it)

    $ pd-trigger -p > ~/etc/pd-trigger.conf

lazily creates a host-unique PD event,

    $ pd-trigger

alternatively, specify a Service Key as command arg,

    $ pd-trigger -s "012345678901234567890123456789012"

pipe input into an event description,

    $ netstat -nr | pd-trigger

view the JSON payload (but do not trigger an event),

    $ pd-trigger -j

Print incident_key string to stdout, (replies dump to syslog as well, by default),

    $ pd-trigger -t

When successfully exiting, pd-trigger will dump PagerDuty response messages lazily into syslog(1) via logger(1), and has command arguments to return incident state strings to calling processes if desired.


