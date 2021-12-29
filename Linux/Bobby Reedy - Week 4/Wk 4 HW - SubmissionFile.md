## Week 4 Homework Submission File: Linux Systems Administration

### Step 1: Ensure/Double Check Permissions on Sensitive Files

1. Permissions on `/etc/shadow` should allow only `root` read and write access.

    - Command to inspect permissions: ls -l shadow

    - Command to set permissions (if needed): sudo chmod 600 shadow

2. Permissions on `/etc/gshadow` should allow only `root` read and write access.

    - Command to inspect permissions: ls -l gshadow

    - Command to set permissions (if needed): sudo chmod 600 gshadow

3. Permissions on `/etc/group` should allow `root` read and write access, and allow everyone else read access only.

    - Command to inspect permissions: ls -l group

    - Command to set permissions (if needed): sudo chmod 644 group

4. Permissions on `/etc/passwd` should allow `root` read and write access, and allow everyone else read access only.

    - Command to inspect permissions: ls -l passwd

    - Command to set permissions (if needed): sudo chmod 644 passwd

### Step 2: Create User Accounts

1. Add user accounts for `sam`, `joe`, `amy`, `sara`, and `admin`.

    - Command to add each user account (include all five users):
		- sudo adduser sam
		- sudo adduser joe
		- sudo adduser amy
		- sudo adduser sara
		- sudo adduser admin

2. Ensure that only the `admin` has general sudo access. 

    - Command to add `admin` to the `sudo` group: sudo usermod -aG sudo admin
		- Check for whether other users have sudo access: 
			-groups sam
			-groups joe
			-groups amy
			-groups sara

### Step 3: Create User Group and Collaborative Folder

1. Add an `engineers` group to the system.

    - Command to add group: sudo addgroup engineers

2. Add users `sam`, `joe`, `amy`, and `sara` to the managed group.

    - Command to add users to `engineers` group (include all four users):
		- sudo usermod -aG engineers sam
		- sudo usermod -aG engineers joe
		- sudo usermod -aG engineers amy
		- sudo usermod -aG engineers sara

3. Create a shared folder for this group at `/home/engineers`.

    - Command to create the shared folder: sudo mkdir engineers

4. Change ownership on the new engineers' shared folder to the `engineers` group.

    - Command to change ownership of engineer's shared folder to engineer group: 
		- sudo chown :engineers engineers

### Step 4: Lynis Auditing

1. Command to install Lynis: sudo apt install lynis

2. Command to see documentation and instructions: man lynis

3. Command to run an audit: sudo lynis audit system

4. Provide a report from the Lynis output on what can be done to harden the system.

    - Screenshot of report output:

-[ Lynis 2.6.2 Results ]-

  Warnings (5):
  ----------------------------
  ! Version of Lynis is very old and should be updated [LYNIS] 
      https://cisofy.com/controls/LYNIS/

  ! Multiple accounts found with same UID [AUTH-9208] 
      https://cisofy.com/controls/AUTH-9208/

  ! No password set for single mode [AUTH-9308] 
      https://cisofy.com/controls/AUTH-9308/

  ! Found one or more vulnerable packages. [PKGS-7392] 
      https://cisofy.com/controls/PKGS-7392/

  ! Found some information disclosure in SMTP banner (OS or software name) [MAIL-8818] 
      https://cisofy.com/controls/MAIL-8818/


### Bonus
1. Command to install chkrootkit: sudo apt install chkrootkit

2. Command to see documentation and instructions: man chkrootkit

3. Command to run expert mode: sudo chkrootkit -x

4. Provide a report from the chrootkit output on what can be done to harden the system.
    - Screenshot of end of sample output: I ran the following command to filter for malicious content.
		-sudo chkrootkit -q

/usr/lib/debug/.build-id /usr/lib/python2.7/dist-packages/ansible/galaxy/data/container/files/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/container/.travis.yml /usr/lib/python2.7/dist-packages/ansible/galaxy/data/container/templates/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/default/collection/roles/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/default/collection/docs/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/default/role/files/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/default/role/.travis.yml /usr/lib/python2.7/dist-packages/ansible/galaxy/data/default/role/templates/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/apb/files/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/apb/.travis.yml /usr/lib/python2.7/dist-packages/ansible/galaxy/data/apb/templates/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/network/files/.git_keep /usr/lib/python2.7/dist-packages/ansible/galaxy/data/network/.travis.yml /usr/lib/python2.7/dist-packages/ansible/galaxy/data/network/templates/.git_keep /lib/modules/5.0.0-23-generic/vdso/.build-id
/usr/lib/debug/.build-id /lib/modules/5.0.0-23-generic/vdso/.build-id
not tested
INFECTED: Possible Malicious Linux.Xor.DDoS installed
/tmp/burpsuite_community_linux_v2020_11_3.sh
/tmp/vagrant-shell
/tmp/response.varfile
/tmp/str.sh
enp0s3: PACKET SNIFFER(/sbin/dhclient[1038])
 The tty of the following user process(es) were not found
 in /var/run/utmp !
! RUID          PID TTY    CMD
! gdm          2091 tty1   /usr/bin/Xwayland :1024 -rootless -terminate -accessx -core -listen 4 -listen 5 -displayfd 6
! gdm          2043 tty1   /usr/lib/gdm3/gdm-wayland-session gnome-session --autostart /usr/share/gdm/greeter/autostart
! gdm          2048 tty1   /usr/lib/gnome-session/gnome-session-binary --autostart /usr/share/gdm/greeter/autostart
! gdm          2056 tty1   /usr/bin/gnome-shell
! gdm          2183 tty1   /usr/lib/gnome-settings-daemon/gsd-a11y-settings
! gdm          2185 tty1   /usr/lib/gnome-settings-daemon/gsd-clipboard
! gdm          2187 tty1   /usr/lib/gnome-settings-daemon/gsd-color
! gdm          2189 tty1   /usr/lib/gnome-settings-daemon/gsd-datetime
! gdm          2197 tty1   /usr/lib/gnome-settings-daemon/gsd-housekeeping
! gdm          2199 tty1   /usr/lib/gnome-settings-daemon/gsd-keyboard
! gdm          2204 tty1   /usr/lib/gnome-settings-daemon/gsd-media-keys
! gdm          2211 tty1   /usr/lib/gnome-settings-daemon/gsd-mouse
! gdm          2212 tty1   /usr/lib/gnome-settings-daemon/gsd-power
! gdm          2215 tty1   /usr/lib/gnome-settings-daemon/gsd-print-notifications
! gdm          2224 tty1   /usr/lib/gnome-settings-daemon/gsd-rfkill
! gdm          2226 tty1   /usr/lib/gnome-settings-daemon/gsd-screensaver-proxy
! gdm          2230 tty1   /usr/lib/gnome-settings-daemon/gsd-sharing
! gdm          2233 tty1   /usr/lib/gnome-settings-daemon/gsd-smartcard
! gdm          2237 tty1   /usr/lib/gnome-settings-daemon/gsd-sound
! gdm          2242 tty1   /usr/lib/gnome-settings-daemon/gsd-wacom
! gdm          2179 tty1   /usr/lib/gnome-settings-daemon/gsd-xsettings
! gdm          2138 tty1   ibus-daemon --xim --panel disable
! gdm          2142 tty1   /usr/lib/ibus/ibus-dconf
! gdm          2302 tty1   /usr/lib/ibus/ibus-engine-simple
! gdm          2147 tty1   /usr/lib/ibus/ibus-x11 --kill-daemon
! sysadmin     2392 tty2   /usr/lib/xorg/Xorg vt2 -displayfd 3 -auth /run/user/1000/gdm/Xauthority -background none -noreset -keeptty -verbose 3
! sysadmin     2390 tty2   /usr/lib/gdm3/gdm-x-session --run-script env GNOME_SHELL_SESSION_MODE=ubuntu gnome-session --session=ubuntu
! sysadmin     2414 tty2   /usr/lib/gnome-session/gnome-session-binary --session=ubuntu
! sysadmin     2586 tty2   /usr/bin/gnome-shell
! sysadmin     2746 tty2   /usr/lib/gnome-settings-daemon/gsd-a11y-settings
! sysadmin     2748 tty2   /usr/lib/gnome-settings-daemon/gsd-clipboard
! sysadmin     2743 tty2   /usr/lib/gnome-settings-daemon/gsd-color
! sysadmin     2758 tty2   /usr/lib/gnome-settings-daemon/gsd-datetime
! sysadmin     2825 tty2   /usr/lib/gnome-disk-utility/gsd-disk-utility-notify
! sysadmin     2760 tty2   /usr/lib/gnome-settings-daemon/gsd-housekeeping
! sysadmin     2761 tty2   /usr/lib/gnome-settings-daemon/gsd-keyboard
! sysadmin     2764 tty2   /usr/lib/gnome-settings-daemon/gsd-media-keys
! sysadmin     2706 tty2   /usr/lib/gnome-settings-daemon/gsd-mouse
! sysadmin     2707 tty2   /usr/lib/gnome-settings-daemon/gsd-power
! sysadmin     2710 tty2   /usr/lib/gnome-settings-daemon/gsd-print-notifications
! sysadmin     2795 tty2   /usr/lib/gnome-settings-daemon/gsd-printer
! sysadmin     2716 tty2   /usr/lib/gnome-settings-daemon/gsd-rfkill
! sysadmin     2719 tty2   /usr/lib/gnome-settings-daemon/gsd-screensaver-proxy
! sysadmin     2722 tty2   /usr/lib/gnome-settings-daemon/gsd-sharing
! sysadmin     2725 tty2   /usr/lib/gnome-settings-daemon/gsd-smartcard
! sysadmin     2727 tty2   /usr/lib/gnome-settings-daemon/gsd-sound
! sysadmin     2733 tty2   /usr/lib/gnome-settings-daemon/gsd-wacom
! sysadmin     2736 tty2   /usr/lib/gnome-settings-daemon/gsd-xsettings
! sysadmin     2621 tty2   ibus-daemon --xim --panel disable
! sysadmin     2625 tty2   /usr/lib/ibus/ibus-dconf
! sysadmin     2880 tty2   /usr/lib/ibus/ibus-engine-simple
! sysadmin     2629 tty2   /usr/lib/ibus/ibus-x11 --kill-daemon
! sysadmin     2812 tty2   nautilus-desktop
! admin        3553 pts/0  bash
! admin        3608 pts/0  su sysadmin
! root        20436 pts/0  /bin/sh /usr/sbin/chkrootkit -q
! root        21183 pts/0  ./chkutmp
! root        21185 pts/0  ps axk tty,ruser,args -o tty,pid,ruser,args
! root        21184 pts/0  sh -c ps axk "tty,ruser,args" -o "tty,pid,ruser,args"
! root        20435 pts/0  sudo chkrootkit -q
! sysadmin     3116 pts/0  bash
! sysadmin     3609 pts/0  bash
! sysadmin     5825 pts/0  man lynis
! sysadmin    19415 pts/0  man chkrootkit
! sysadmin    20386 pts/0  man chkrootkit
! sysadmin     5835 pts/0  pager
! sysadmin    19425 pts/0  pager
! sysadmin    20396 pts/0  pager
! sysadmin     3540 pts/0  su admin
not tested

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
