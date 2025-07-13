Kali is ran in a docker container

Check the images, use the most recent image
```
sudo docker image ls
```

Spinning up a new container
```
sudo docker run -it -v /mnt/kali:/host --net=host --cap-add=NET_RAW --cap-add=NET_ADMIN kali-1 /bin/bash
```

checking containers 
```
sudo docker container ps 
```

Attaching to a current running container
```
sudo docker start 364674ac0c03
sudo docker 364674ac0c03
```

navigate to ~ (thats where all my tools are) and start the venv also

Commiting a container to an image
```
sudo docker commit 364674ac0c03 image-name
```


