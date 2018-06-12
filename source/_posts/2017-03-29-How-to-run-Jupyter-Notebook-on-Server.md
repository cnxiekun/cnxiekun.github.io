---
title: How to run Jupyter Notebook on Server
date: 2017-03-29 03:43:27
categories: Technique
tags: [Python, Server]
description:
---

### Access to Server (e.g., Pascal)

Open terminal and use your account and password to log in the server, e.g.,

```
$ ssh your_account_name@pascal.ieda.ust.hk
```

Then enter your password.

### Create a notebook configuration file

Use the following command to generate `jupyter_notebook_config.py`, whose default parent directory is `~/.jupyter`, if you don't have one:

```
$ jupyter notebook --generate-config
```

<!--more-->


### Generate a hased password

Open Python from terminal and use the following commands to obtain your *hashed password*:

```python
>>> from notebook.auth import passwd
>>> passwd()
Enter password:
Verrfy password:
'sha1:xxx...'
>>> ctrl+z
```

Remember your hashed password for later use.



### Use SSL for security

You can secure the connection  (`https://`) using a self-sighed certificate:

```
$ openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mykey.key -out mycert.pem
```

This command requires you to enter some personal information and one password for future use (login the Maxwell on your laptop, browser password). It would also generate two files `mykey.key` and `mycert.pem` in the current directory, for later use.

### Run a public notebook server

This step would let you access notebook on maxwell via a web browser. Open the configuration file via following command:

```
$ vim ~/.jupyter/jupyter_notebook_config.py
```

Find the following lines, make corresponding changes and uncomment them:

```python
## The full path to an SSL/TLS certificate file.
c.NotebookApp.certfile = u'./mycert.pem'
	
## The IP address the notebook server will listen on.
c.NotebookApp.ip = '*'

## The full path to a private key file for usage with SSL/TLS.
c.NotebookApp.keyfile = u'./mykey.key'
	
c.NotebookApp.password = u'sha1:xxx...<your hashed password>'
	
c.NotebookApp.open_browser = False

## The port the notebook server will listen on.
c.NotebookApp.port = 9999
```

Save and exit.

After above settings, you can start the notebook using the `jupyter notebook` command. Open your browser, e.g, `Safari`, go to
	
```
https://pascal.ieda.ust.hk:<your port>
```

It needs your password to enter (browser password created via SSL).


### Remark

1. The default location of `mycert.pem` and `mykey.key` is in the home directory `~/`if you use the above seeting. Acturally, you can move them to other directory, e.g., `~/.jupyter/`, then edit the addresses of `certfile` and `keyfile` in configuration file (see above).

2. You can use `nohup` command if you still want to use the notebook on Maxwell after you close the notebook terminal window, e.g,

  ```	
  $ nohup jupyter notebook > log &
  ```
  Adcanced:
  ```	
  $ nohup jupyter notebook > /dev/null 2>&1 &
  ```
  Note: you can also rename the config file, e.g., `myconfig.py`, then modify above nohup command as follows
  ```	
  $ nohup jupyter notebook --config=YOUR_PATH/myconfig.py > /dev/null 2>&1 &
  ```

3. If you want to kill it later, use `kill $(pgrep jupyter)`. Or use commend `netstat -tulnp` to check the Jupyter process, then `kill -9 PID`.

That's it, enjoy your notebook on your server.