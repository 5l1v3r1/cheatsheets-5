Advanced Package Tool
=====================

Various tips on debian's *apt* utilities like `apt-get`, `apt-cache`, `apt-file`, `dpkg`, etc.

=== <code>/etc/apt/sources.list</code> ===

;netselect: A program which determines the fastest server from a list of hosts given on the command line.
;netselect-apt: A program which generates a sources.list file using the best debian mirror.

The <code>netselect-apt</code> program can be found in the <code>netselect</code> source package. To install the <code>netselect</code> source package, add appropriate <code>deb-src</code> lines to <code>/etc/apt/sources.list</code> like:

 deb-src http://http.us.debian.org/debian testing main contrib non-free
 deb-src http://non-us.debian.org/debian-non-US testing/non-US main contrib non-free

then

 apt-get update
 apt-get source netselect

The above procedure will generate a directory with the netselect source, named for example <code>netselect-0.3.ds1</code>.

To generate a <code>sources.list</code> file for the testing distribution, run <code>./netselect-0.3.ds1/netselect-apt testing</code>.

=== Install/remove ===

 apt-get install pkg1 pkg2-
    Install pkg1 and remove pkg2.
 
 apt-get remove pkg1 pkg2+
    Remove pkg1 and install pkg2.
 
 -u
    Causes APT to show the complete list of packages which will be upgraded (when doing apt-get upgrade or apt-get dist-upgrade).
 
 apt-get -t dist install pkg
    Install pkg from distribution dist. 
 
 apt-get install package=version
    Install a specific version of a package.

=== Search ===

 apt-cache search regexp
 apt-cache show pkg
 apt-cache showpkg pkg
 COLUMNS=132 dpkg -l pattern
 
 dpkg -S file
    Search for a filename in installed packages.
 
 dpkg -L package
    List files installed from package.
 
 apt-file update
    Update the database of files all packages contain.
 
 apt-file search file
    Search for a filename in all packages.

=== Using source packages ===

 apt-get source pkgname
 
 apt-get -b source pkgname
    Automatically build the downloaded package.
 
 dpkg-buildpackage -rfakeroot -uc -b
    Build the package later, do this from within the directory that was created after downloading the source package.
 
 dpkg -i file.deb
 
 apt-get build-dep pkg
    Install the packages required for pkg to be built. (Sources must be installed separately by apt-get source.)

=== Miscellaneous ===

 apt-show-versions
    Lists available package versions with distribution.
 
 apt-show-versions -u
    Display a list of upgradeable packages.
 
 apt-cache depends pkgname
 
 apt-cache rdepends pkgname

=== Resources ===

# <code>apt-cache search -n ^apt-</code>
# [http://www.debian.org/doc/ddp Debian Documentation Project]
# [http://www.debian.org/doc/manuals/apt-howto/index.en.html APT HOWTO]


