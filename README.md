# SpamReporter

Submits spam email to reporting accounts — sends messages stored in a Maildir to SpamCop, KnujOn, or any specified reporting address (such as the 
[FTC's](http://www.consumer.ftc.gov/articles/0038-spam#report) [spam@uce.gov](mailto:spam@uce.gov)).

### Dependencies

 * [Ruby](https://www.ruby-lang.org/), [Mutt](http://www.mutt.org/)
 * Some features use `ssh`, `scp` and `awk`
 * POSIX-like environment with `cat`, `cp`, `rm`, `mktemp`, and pipes
 * Spam stored in a [Maildir](http://cr.yp.to/proto/maildir.html) or [Maildir++](http://www.courier-mta.org/imap/README.maildirquota.html) directory

### Installation

Copy the `spamreporter` executable to some appropriate location like `~/bin/`, preferably in your $PATH, and make sure it's marked as executable.

### Usage

Intended for use in a cronjob on a mail server, at an interval and `--limit` appropriate to the policies of that server and of the report recipients.

Messages should not be moved into the spam Maildir automatically, unless it is an inbox for spam trap addresses.  (See [SpamCop: Can I automatically forward spam from my spamtraps?](https://www.spamcop.net/fom-serve/cache/402.html))


```
Usage: spamreporter [arguments]

Required arguments:
    -s, --source <maildir>           Report messages in this maildir as spam (may be repeated)
    -d, --destination <maildir>      Move reported messages to this maildir (see also -r)
    -f, --from <email>               The email address to use in the From: header
    -a, --address <email>            Report spam to this address (may be repeated; see also -i, -k, -e, and -t)

Optional arguments:
    -i, --id, --spamcop <spamcop id> Report spam to SpamCop using this user ID
    -q, --quick                      Report to SpamCop for quick reporting
    -k, --knoujon [knujon id]        Report spam to KnujOn, optionally with a user ID
    -e, --echo                       Also send report to From: address
    -r, --remove                     Delete reported messages (conflicts with and replaces -d)
    -l, --limit <count>              Report no more than count messages (default 1)
    -h, --host, --remote <host>      Use ssh to send mail through another host (may also require -b and/or -m)
    -b, --body                       Spam message reported as body of report message (rather than as attachment)
    -m, --mua <command>              Use this command to send mail (default /usr/bin/mutt)
    -v, --verbose                    Enable verbose output
    -t, --test                       Send report only to From: address, and do not (re)move messages (implies -v and -e, replaces -a, -i, and -k)
    -n, --dryrun                     Walk through process without sending reports or (re)moving messages
    -g, --debug                      Enable debug output (implies -v)

Informational arguments:
        --help                       Show this message (instead of any reporting)
        --version                    Show version (instead of any reporting)
        --license                    Show license (GNU AGPLv3)
```

### License

SpamReporter - submits spam email to reporting accounts<br/>
Copyright © 2003-2015 Shad Sterling <<me@shadsterling.com>>

This program is free software: you can redistribute it and/or modify it under the terms of the
GNU Affero General Public License as published by the Free Software Foundation,
either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY;
without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
See the GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License along with this program.
If not, see <http://www.gnu.org/licenses/agpl.html>


