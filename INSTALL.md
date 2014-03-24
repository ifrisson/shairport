Type `make` to build the packet decoder, `hairtunes`.

You need the following installed:

 * openssl
 * libao
 * Perl 5.10 or higher
 * Linux: avahi (or, for embedded systems, howl)
 * Windows/Mac OS X: Bonjour

Perl modules (install from CPAN if needed e.g. `perl -MCPAN -e 'install X'`):

once cpan is installed you can install the perl modules by issuing the following commands


	cpan install HTTP::Request
	cpan install HTTP::Message
	cpan install Crypt::OpenSSL::RSA
	cpan install IO::Socket::INET6
	cpan install Net::SDP

## Debian/Ubuntu:

    apt-get install build-essential libssl-dev libcrypt-openssl-rsa-perl libao-dev libio-socket-inet6-perl libwww-perl avahi-utils pkg-config
    make
    perl shairport.pl
    
to install as a daemon 
  
    make install
    
to change the service name
    
	nano shairport.pl
    
and look for the line that says my $apname = "ShairPort $$ on " . `hostname`; and change it to 

    my $apname = "WHATEVER YOU LIKE";
    
close the file with the Ctrl-X key combination. Press Y to accept the changes.
copy the startup deamon to /etc/init.d/

    cp shairport.init.sample /etc/init.d/shairport

make the file executable

    sudo chmod +x /etc/init.d/shairport

add it as a boot up service

    sudo update-rc.d shairport defaults

Test, then reboot

    sudo service shairport start
    

## Redhat/Fedora:

    yum install openssl-devel libao libao-devel perl-Crypt-OpenSSL-RSA perl-IO-Socket-INET6 perl-libwww-perl avahi-tools
    make
    perl shairport.pl
    

## Gentoo/Funtoo

    echo "media-libs/libao  alsa" >> /etc/portage/package.use
    echo "net-dns/avahi  mdnsresponder-compat" >> /etc/portage/package.use
    echo "dev-perl/HTTP-Message  ~x86" >> /etc/portage/package.keywords
    echo "dev-perl/HTTP-Date  ~x86" >> /etc/portage/package.keywords
    echo "dev-perl/Encode-Locale  ~x86" >> /etc/portage/package.keywords
    echo "dev-perl/LWP-MediaTypes  ~x86" >> /etc/portage/package.keywords
    emerge libao avahi dev-perl/HTTP-Message dev-perl/Crypt-OpenSSL-RSA dev-perl/IO-Socket-INET6
    rc-update add dbus default
    rc-update add avahi-daemon default
    /etc/init.d/dbus start
    /etc/init.d/avahi-daemon start
    make
    perl shairport.pl

## OpenBSD

    pkg_add -r gmake libao avahi p5-libwww p5-Crypt-OpenSSL-RSA p5-IO-Socket-INET6
    gmake
    perl shairport.pl

## Mac OS X:

  * install XCode
  * install [Homebrew](https://github.com/mxcl/homebrew) or [MacPorts](http://www.macports.org/)
  * type:

        $ export ARCHFLAGS="-arch x86_64" # (replace x86_64 by your arch)
        $ brew install pkg-config libao # for [Homebrew](https://github.com/mxcl/homebrew)
        $ port install pkgconfig libao # for [MacPorts](http://www.macports.org/)
        $ make
        $ perl -MCPAN -e 'install Crypt::OpenSSL::RSA' # (may require sudo)
        $ perl -MCPAN -e 'install IO::Socket::INET6' # (may require sudo)
        $ perl shairport.pl

  Users of OS X 10.5 and below will need to install a newer Perl (via `port`/`brew`).

### How to run as a daemon on Mac 10.6

    $ cp hairtunes shairport.pl /usr/local/bin
    $ vi /usr/local/bin/shairport.pl # change the path of hairtunes from ./hairtunes to /usr/local/bin/hairtunes
    $ mkdir -p ~/Library/LaunchAgents
    $ cp org.mafipulation.shairport.plist ~/Library/LaunchAgents/
    $ launchctl load org.mafipulation.shairport.plist
    $ launchctl unload org.mafipulation.shairport.plist # (to remove)

## Windows

 * Download and install Cygwin.
 * During setup, select
    * openssl-devel
    * openssl
    * libao
    * libao-devel
    * gcc4
    * make
    * pkg-config
    * perl
 * Install [Bonjour for Windows](http://support.apple.com/kb/DL999)
 * Launch the Cygwin Bash shell
 * type:

        $ make
        $ perl -MCPAN -e 'install Crypt::OpenSSL::RSA'
        $ perl -MCPAN -e 'install IO::Socket::INET6'
        $ perl shairport.pl
