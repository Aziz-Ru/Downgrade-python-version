## Here I downgrade python version and switch the multiple version of python
I'm using python3.11.6 now i want switch 3.10.11
# Make a directory python file which you want downgrade 
`mkdir ~/python-source-files`

# Download python3.10.11 
`wget -P ~/python-source-files https://www.python.org/ftp/python/3.10.11/Python-3.10.11.tgz`


# Extract 3.10.11.tgz 
```
cd python-source-files/
tar xvzf Python-3.10.11.tgz

```
# change directory in Python3.10.11 
`cd Python-3.10.11/` and configure optimization `./configure --enable-optimizations`
and run this command for alternative install `sudo make altinstall`

 After alternative install now check how many python version available to see that 
 run this `ls /usr/local/lib | grep python`
 
 where is python3.10 to see that `type -a python3.10`
 
 Now update pyhton3.10 for alternative 
 ```
 sudo update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.10 1
 
 sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 2

 ```
# Switch version of python 
```
sudo update-alternatives --config python3

```
 




