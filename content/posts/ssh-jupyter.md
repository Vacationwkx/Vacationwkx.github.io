---
title: "Use Jupiter Notebook by ssh"
date: 2020-12-05T22:18:34+08:00
draft: false
categories: ComputerTech
tags:
  - reinforcement learning
  - linux
---

This blog shows up a way to ssh a ubuntu computer (as Jupyter Notebook server) from mac.

# Prerequirements

## Ubuntu / Remote Setting

### SSH Setting

run the following command to enable the ssh on ubuntu(18.04)

```shell
$ sudo apt-get install openssh-server
```

### Jupyter Notebook Setting(optional)

using jupyter notebook  may require the token or password, you may refer to [the jupyter notebook official site](https://jupyter-notebook.readthedocs.io/en/stable/security.html) for details.

- Token

  take note of the result`jupyter notebook` command, the token is inside the link after `token=`, e.g

  ```
  $ http://localhost:8888/?token=c8de56fa4deed24899803e93c227592aef6538f93025fe01
  ```

- Password

  to set the password, first run

  ```
  $ jupyter notebook --generate-config
  ```

  to generate `jupyter_notebook_config.py`, see where it locate at [official site](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html).

  then run

  ```
  $ jupyter notebook password
  Enter password:  ****
  Verify password: ****
  ```

  to set the password, afterwards all localhost:XXXX can log in with this password

# Run Jupyter at Mac

only 2 commands:

- Ubuntu: `jupyter notebook --no-browser --port=XXXX`
- Mac: `ssh -N -f -L localhost:YYYY:localhost:XXXX remoteuser@remotehost` or `ssh -L localhost:YYYY:localhost:XXXX remoteuser@remotehost` for not running in background, in case the port usage conflict

you may set up a script refer to [Lj Miranda's post](https://ljvmiranda921.github.io/notebook/2018/01/31/running-a-jupyter-notebook/),

and remove the forward port rule refer to [this question on StackExchange](https://superuser.com/questions/539644/how-to-remove-port-forwarding-rule-on-mac), or simply reboot your mac

# If remote is HPC (NUS)

Terminal 1 (after ssh login)

```
$ module load singularity
$ qsub -I -l select=1:mem=50GB:ncpus=10:ngpus=1 -l walltime=02:00:00 -q volta_login
# walltime = 02:00:00 can be changed
$ singularity exec /app1/common/singularity-img/3.0.0/tensorflow_2.3.1-cuda_11.1-cudnn_8-ubuntu18.04-py36-nvcr20.11.simg jupyter notebook
```

Terminal 2 

- login using port forward: ssh -L YYY:volta01:8888 nusip@atlas9
  - or atlas 8
- open localhost:9999



