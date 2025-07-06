# Quick Quarm EQ
<h3>About</h3>

Adapted from https://github.com/ryhoneyman/quick-quarm to use the TAKP repos

<h3>Instructions</h3>
<ul>
  <li>Install Ubuntu 22.04 or later in a VM or on metal, I don't care, don't use WSL2, or try to run this on a pregnancy test.</i>
  <li>Install with any user that has sudo privilege.
  <li>Clone this repo to the directory of your choosing: <b>git clone https://github.com/DDTully/quick-quarm.git</b>
  <li>Change to the quick-quarm repo directory and run <b>sudo ./scripts/setup</b>
  <li>You will need the TAKP client (not quarm) to play</li>
</ul>

<h4>Configuration</h4>
<pre>
user@host:~/quick-quarm$ sudo ./scripts/setup

Detected /home/user/quick-quarm as Quick Quarm home (user: user)

The defaults are a great starting point, so it's safe to accept them as is to get up and running.
However, if you have a cloned repo of EQMacEmu/Server that you are using for development, feel free to use that instead.

If you are using your own repo, make sure you've setup your git SSH key, and git username/email BEFORE continuing.

Install user [user]:
EQMacEmu repository [https://github.com/EQMacEmu/Server.git]:
Database host [localhost]:
Database name [quarm]:
Database username [quarm]:
Database password [quarm]:
Host address [192.168.1.100]:

Writing configuration to /home/user/quick-quarm/etc/.env
</pre>

<h4>Setup</h4>
<pre>
Beginning setup:
   [INSTALL] Updating system...
   [INSTALL] Upgrading system...
   [INSTALL] Installing dependencies...
   [INSTALL] Setting up MySQL user...
    [SOURCE] Cloning Server repo...
    [SOURCE] Cloning quests repo...
    [SOURCE] Cloning maps repo...
  [DATABASE] Extracting latest database files...
  [DATABASE] Setup database and tables...
     [MYSQL] Importing: quarm < /home/rhoneyman/quick-quarm/db/login_tables_*.sql
     [MYSQL] Importing: quarm < /home/rhoneyman/quick-quarm/db/player_tables_*.sql
     [MYSQL] Importing: quarm < /home/rhoneyman/quick-quarm/db/alkabor_*.sql
     [MYSQL] Importing: quarm < /home/rhoneyman/quick-quarm/db/data_tables_*.sql
     [MYSQL] Importing: quarm < /home/rhoneyman/quick-quarm/source/EQMacEmu/loginserver/login_util/tblloginserversettings.sql
     [MYSQL] Importing: quarm < /home/rhoneyman/quick-quarm/files/update_settings.sql
     [BUILD] Generating make files...
     [BUILD] Starting build with X threads... (this may take some time for the initial build)
   [INSTALL] Cleaning up bin directory
   [INSTALL] Copy build binaries to bin directory
   [INSTALL] Create logs and shared directories
   [INSTALL] Link quests and maps directories
   [INSTALL] Copy in auxillary configuration files
    [CONFIG] Updating eqemu_config.json
    [CONFIG] Updating login.ini
   [SYSTEMD] Installing Quick Quarm service
   [SYSTEMD] Service eqemu-loginserver.service installing...
   [SYSTEMD] Service eqemu-queryserv.service installing...
   [SYSTEMD] Service eqemu-shared-memory.service installing...
   [SYSTEMD] Service eqemu-ucs.service installing...
   [SYSTEMD] Service eqemu-world.service installing...
   [SYSTEMD] Service eqemu-zone.service installing...
   [SYSTEMD] Service quick-quarm.target installing...
   [SYSTEMD] Enabling Quick Quarm service


===== DONE!!! =====

Congratulations! Everything completed successfully, and you're one step closer to your own Quarm server.

Next Steps:

 * New users: Download the TAKP v2.2 Client and the associated PQ package zip file from PQ Discord #server-files
 * Existing users: Copy your existing TAKP folder to another separate folder from your normal PQ install.
 * Edit the file eqhost.txt file and change loginserver.takproject.net:6000 to 192.168.1.100:6000
 * Start your client (run as Administrator, and set compatibility options if needed)
 * Login as whatever username/password you want to use (this will fail and is expected).  Click Ok, and hit [ENTER] again.
 * You should see your Quick Quarm EQ server in the list: select it, create a character, and enter the world.
 * On your Quick Quarm host, run ./scripts/eq-makegm -l LOGINACCOUNT
 * If you are already logged in, enter '/sit', '/camp login', then log back in to activate GM powers.
</pre>

<h3>What It Does</h3>
<ul>
  <li>Updates the system and install all Project Quarm dependencies
  <li>Downloads source from git repos
  <li>Installs the Project Quarm database and sets up user/permissions
  <li>Builds and installs the Project Quarm source code into binaries
  <li>Updates all configuration files for this specific installation
  <li>Installs quick-quarm.target service into systemd and enables it on boot.
</ul>

<h3>Updating</h3>
In order to update Project Quarm to the latest source and database, from the quick-quarm repo directory just run:
<ul>
  <li><b>./scripts/update</b>
  <li><b>sudo systemctl restart quick-quarm.target</b> (server will come down and restart)
</ul>
<p>Note that if you are using your own repo, update will not attempt a source update since we assume you are controlling the source locally.

<h3>Setup Flags</h3>
<pre>
./setup
        -d      Enable debug
        -v      Enable verbose logging
        -f      Enable forced commands (disregard any safety checks) <b>[not currently used]</b>
        -c      Enable clean mode (removes database/source and starts clean)
        -h      This help
</pre>
