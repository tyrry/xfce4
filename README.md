## Ports for constructing the 'xfce4' and 'xfce4-extra' collections

Contributions are welcome. If you don't know what it all about, please take the time to read the documentation at
http://www.nutyx.org/en/build-package.html
(version française)
http://www.nutyx.org/fr/build-package.html

It will explain you what's a collection, a git, a port, the tools around 'cards' etc

### How to test this git:

#### 1. Clone it in your home directory

    $ cd
    $ git clone git://github.com/NuTyX/xfce4.git
    $ git clone git://github.com/NuTyX/houaphan.git

#### 2. Become root until the end, define and create the directory used by the scripts:

 The script is checking the files /etc/install-houaphan.conf and /etc/install-houaphan.conf.d/cards.conf if they exist, if yes it will use them, so:

    $ su -
    # echo "LFS=/mnt/lfs
    DEPOT=/houaphan" > /etc/install-houaphan.conf
    # mkdir -p /etc/install-houaphan.conf.d
    # cat > /etc/install-houaphan.conf.d/cards.conf << "EOF"
    dir /houaphan/xfce4
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

    # mkdir -v /mnt/lfs/root/{houaphan,xfce4}

#### 5. Mount your git project (assume below the user is 'tnut' so adapt to yours)

    # mount -o bind /home/tnut/xfce4 /mnt/lfs/root/xfce4
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
    
#### 9. If everything is OK, synchronize the 'xfce4' collection binaries 

    # cd /root/xfce4
    # bash scripts/xfce4 -s

#### 10. If everything is OK, check with cards level what's new

    # cards level

 It should shows all the packages available.

#### 11. If you want to build the 'xfce4' collection from the sources

    # bash scripts/xfce4 -a

#### 12. If you want to build the 'xfce4-extra' collection from the sources, add the proper line in top of the cards.conf file like this:

    dir /houaphan/xfce4-extra

 then you are ready to compile the 'xfce4-extra' collection

    # cd /root/xfce4
    # bash scripts/xfce4-extra -s
    # bash scripts/xfce4-extra -a 

Have fun :)
