# Super awesome mailserver

Run your own mailserver with docker compose. The project's goal is to easily setup a mailserver, which is valid in all supported points.

**Warning:** If you do not know the difference of an MTA and MDA, please do not intend to use this project. Running your own mailserver won't increase your [Qi](https://en.wikipedia.org/wiki/Qi) and nobody will award you with a black belt in system administration. One of the project's goal is to create more *valid* servers running. If you setup the server badly, you actually counterpoint the project's goal.

# Intro

Running a mailserver can be very hard. And for most people, it actually is.

For me too. In my email career, I started using gmail. After the NSA leaks in 2013, I switched to my own mailserver.

I was proud of it and it kept working for around a year. But I fucked up very hard, after running an update before going on holiday, which included [Perl major update, which forced to rebuilt all modules](https://www.archlinux.org/news/perl-updated-to-520/). My greylisting daemon started to fail after reboot. It blocked all mail and I did not get a chance to fix it during holidays. Needless to say here, I did anything what a senior sysadmin advises not to do to start this fuckup.

Lessons learned. I started migrating to other paid providers with my own domain. But after two years, I have to conclude that none of them are the bee's knees.

I want to switch back to a selfhosted setup. But let's take the learned lessons into account, take the time to develop a great setup and fully understand it.

# Goals (and Features)
##  Why should this project should have specific goals?

Maintaining and running a stable mailserver is hard for normal people. There are too [many](https://en.wikipedia.org/wiki/Open_mail_relay) [tarpits](https://mailbox.org/en/ipv6-deactivated-for-our-incoming-mail-servers/) [to]( "Add your fail! I'm sure the're plenty of.") [step]( "Add your fail! I'm sure the're plenty of.") in. Administration timecosts are quite high to have a mailserver on a single domain basis maintained manually. This leads to improperly configured mailservers, which violate specifications.


# (Planned) Features

- [ ] deployment tests
- [ ] HTTP
    - [ ] autoconfiguration support
- [ ] IMAPs
    - [ ] default inbox folder
	  - [ ] letsencrypt signing certificates
- [ ] SMTPs
    - [ ] Greylisting
	  - [ ] SSL/letsencrypt signing certificates
	  - [ ] Sieve Mailfilter sync support
	  - [ ] DKIM

To be enhanced. This is just the minimal setup

# Principles for the achitecture

- One process per container
    - No `supervisord`, no service-scripts, everyting plain in your shell-file
- As small images as possible
    - Do not base on debian/ubuntu or CentOS/Fedora/..
    - use alpine unless not possible
- The atomic unit should be the docker-compose cluster and not the single container itself
    - It's not desired to have the container management done manually by `docker run ...`
    - Chain the services together via `docker-compose.yml`
