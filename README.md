## Ports for constructing the 'gnome' and 'gnome-extra' collections

Contributions are welcome. If you don't know what it all about, please take the time to read the documentation at
http://www.nutyx.org/en/build-package.html
(version française)
http://www.nutyx.org/fr/build-package.html

It will explain you what's a collection, a git, a port, the tools around 'cards' etc

### How to test this git:

#### 1. Clone it in your home directory

    $ cd
    $ git clone git://github.com/NuTyX/gnome.git
    $ git clone git://github.com/NuTyX/houaphan.git

#### 2. Become root until the end, define and create the directory used by the scripts:

 The script is checking the files /etc/install-houaphan.conf and /etc/install-houaphan.conf.d/cards.conf if they exist, if yes it will use them, so:

    $ su -
    # echo "LFS=/mnt/lfs
    DEPOT=/houaphan" > /etc/install-houaphan.conf
    # mkdir -p /etc/install-houaphan.conf.d
    # cat > /etc/install-houaphan.conf.d/cards.conf << "EOF"
    dir /houaphan/gnome
    dir /houaphan/gui
    dir /houaphan/cli
    dir /houaphan/base|http://downloads.nutyx.org
    dir /houaphan/base-extra|http://downloads.nutyx.org
    base /houaphan/base
    base /houaphan/base-extra
    logdir /var/log/pkgbuild
    EOF

#### 3. Install a base NuTyX system (assume below the user is 'tnut' so adapt to yours)

    # bash /home/tnut/houaphan/scripts/install-houaphan

#### 4. In your chroot Make the directory where the git copy will comes

    # mkdir -v /mnt/lfs/root/{houaphan,gnome}

#### 5. Mount your git project (assume below the user is 'tnut' so adapt to yours)

    # mount -o bind /home/tnut/gnome /mnt/lfs/root/gnome
    # mount -o bind /home/tnut/houaphan /mnt/lfs/root/houaphan

#### 6. Enter now in your chroot

    # bash /home/tnut/houaphan/scripts/install-houaphan -ec

#### 7. Prepare the first execution of the build script

    # get cards.devel wget vim rsync git tar
 
#### 8. If everything is OK, synchronize the  houaphan 'base', 'cli' and 'gui' collections binaries

    # cd /root/houaphan
    # bash scripts/base -s
    # bash scripts/cli -s
    # bash scripts/gui -s
    
#### 9. If everything is OK, synchronize the 'gnome' collection binaries 

    # cd /root/gnome
    # bash scripts/gnome -s

#### 10. If everything is OK, check with cards level what's new

    # cards level

 It should shows all the packages available.

#### 11. If you want to build the 'gnome' collection from the sources

    # bash scripts/gnome -a

#### 12. If you want to build the 'gnome-extra' collection from the sources, add the proper line in top of the cards.conf file like this:

    dir /houaphan/gnome-extra

 then you are ready to compile the 'gnome-extra' collection

    # cd /root/gnome
    # bash scripts/gnome-extra -s
    # bash scripts/gnome-extra -a 

Have fun :)
