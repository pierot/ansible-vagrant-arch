# Vagrant development environment

## Remember the following commands

`vagrant plugin install vagrant-vbguest`

## Install ansible locally

`sudo easy_install pip`
`sudo pip install ansible`

# Ubuntu setup (ubutu-test/)

Prepare image after first ssh login

`sudo apt-get update`
`sudo apt-get install python-software-properties`

`sudo apt-add-repository ppa:rquillo/ansible`
`sudo apt-get update`
`sudo apt-get install ansible`

# Arch Linux setup

(see https://github.com/proximitybbdo/ansible)

I used the packer image creator for Arch via https://github.com/elasticdog/packer-arch
