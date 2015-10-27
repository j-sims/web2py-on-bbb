### Docker failed to install. The only pre-built is 1.0.1 and it doesn't work.
Below are some steps I tried to easily get docker working and it failed.

Ultimately it is possible, but not worth the time at this point:
https://github.com/umiddelb/armhf/wiki/Installing,-running,-using-docker-on-armhf-%28ARMv7%29-devices

- curl https://get.docker.com/ | bash {fail}
    Error: you are not using a 64bit platform.
    Docker currently only supports 64bit platforms.
- Create shell script for install
    # Check that HTTPS transport is available to APT
    if [ ! -e /usr/lib/apt/methods/https ]; then
        apt-get update
        apt-get install -y apt-transport-https
    fi

    # Add the repository to your APT sources
    echo deb https://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list

    # Then import the repository key
    apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9

    # Install docker
    apt-get update
    apt-get install -y lxc-docker

    #
    # Alternatively, just use the curl-able install.sh script provided at https://get.docker.com
    #
- bash /path/to/script.sh

