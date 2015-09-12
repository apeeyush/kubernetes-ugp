# Installation Instructions

These kubernetes installation instructions have been verified on a fresh Ubuntu 14.04 AWS instance.

## Install dependencies
Install `mercurial` and `build-essentials` if not already installed.

    # Update package list
	sudo apt-get update

    # Install mercurial
    sudo apt-get install mercurial

    # Install build-essentials
    sudo apt-get install build-essential

## Install and setup etcd
    curl -L  https://github.com/coreos/etcd/releases/download/v2.1.1/etcd-v2.1.1-linux-amd64.tar.gz -o etcd-v2.1.1-linux-amd64.tar.gz
    tar xzvf etcd-v2.1.1-linux-amd64.tar.gz
    # Add etcd to path
    export PATH=$PATH:/home/<username>/etcd-v2.1.1-linux-amd64

## Install docker
    sudo wget -qO- https://get.docker.com/ | sh
    sudo usermod -aG docker <username>    # Logout and login back to take this in effect
    docker run hello-world                # To verify installation

## Install and setup go

- Install go from source

        # Installing from source - http://golang.org/doc/install/source
        git clone https://go.googlesource.com/go
        cd go
        git checkout go1.4.1
        cd go/src
        ./all.bash
        mkdir ~/goCode

- Add Go to PATH and setup GOPATH

        # Add the following lines to .profile
        # Set path to where go is installed
        export PATH=/home/<username>/go/bin:$PATH
        # Set GOPATH
        mkdir ~/goCode
        export GOPATH=$HOME/goCode
        # Add Go pkg path - http://golang.org/doc/code.html
        export PATH=$PATH:$GOPATH/bin

- Check go installation

        go version

- Install godep

        go get github.com/tools/godep

## Install kubernetes

    mkdir -p $GOPATH/src/k8s.io
    cd $GOPATH/src/k8s.io
    git clone https://github.com/apeeyush/kubernetes.git
    cd kubernetes/
    git remote add upstream 'https://github.com/kubernetes/kubernetes.git'

## Verify Installation

    # start the cluster locally
    hack/local-up-cluster.sh
