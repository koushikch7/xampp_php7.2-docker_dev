This image is intended for PHP+MySQL development. For convenience, it also runs SSH server to connect to. __Both MySQL and phpmyadmin use default XAMPP password__.


## Running the image:

This image uses /web/ directory for your page files, so you need to mount it.

```
docker run --name chkXampp -p 1000:22 -p 80:80 443:443 -d -v ~/my_web_pages:/web chk07/xampp
```
The command above will expose the SSH server on port 41061 and HTTP server on port 41062.    
Feel free to use your own name for the container...

To connect to your web page, visit this URL: [http://localhost:41062/www](http://localhost/web)    
And to open up the XAMPP interface: [http://localhost:41062/](http://localhost/)

## additional How tos

### ssh connection

default SSH password is 'root'.

```
ssh root@localhost -p 1000
```

### get a shell terminal inside your container

```
docker exec -ti myXampp bash
```

### use binaries provided by XAMPP

Inside docker container:
```
export PATH=/opt/lampp/bin:$PATH
```
You can then use `mysql` and friends installed in `/opt/lampp/bin` in your current bash session. If you want this to persist, you need to add it to your user or system-wide `.bashrc` (inside container).

### Use your own configuration

In your home directory, create a `my_apache_conf` directory in which you place any number of apache configuration directive files. As soon as they end up with the .conf extension, they will be used by the image.

```
docker run --name chkXampp -p 1000:22 -p 80:80 -d -v ~/my_web_pages:/web  -v ~/my_apache_conf:/opt/lampp/apache2/conf.d chk07/xampp
```

### Restart the server

Once you have modified configuration for example
```
docker exec chkXampp /opt/lampp/lampp restart
```
Please report any issues in issues section on github: https://github.com/tomsik68/docker-xampp/issues where we can track them conveniently. Thanks :)
