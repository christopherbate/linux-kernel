# Building the Debian Package

You need Docker installed in order to launch the build container. From the build container, you will build the linux kernel. The script to launch the build container will bind mount the repository directory in to the container. The 
Debian package will be placed in the container one folder up from the `linux-kernel` directory (the one you start in). So you will need 
to use `docker cp` to copy the file out of the container. Several pebian packages will be created, the one desired is `linux-image-4.4.167-rockchip-dev_4.4.167--rockchip-ayufan_arm64.deb`.

1. Rename the configuration file: `cp ./use_this.config ./.config`
2. Start the build container (the docker commands are in this script): `sudo ./dev-shell`.
May work without sudo (he appears to have designed it to work without, but won't work for me, 
regardless of docker group, etc.)
3. Build the debian package: `./dev-make kernel-package`.
4. Start a new shell outside the container in the repo directory. Then do 
`docker ps` to find the container name of the build container. 
5. Copy package: `docker cp [container name]:/path/to/deb_package /path/on/your/hdd`
6. Exit container shell with `logout` or `exit`. The container will automatically
be destroyed, including the deb package if you did not copy it out. 

SCP file to board and install with `dpkg -i /path/to/deb`. You can also SCP directly from the container. He uses the container to upload the built package to the cloud from GitLab.



