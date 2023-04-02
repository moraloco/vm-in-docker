FROM ubuntu:18.04
RUN apt-get update -y && \
    apt-get install -y qemu-kvm libvirt-daemon-system libvirt-dev linux-image-generic curl net-tools jq openssh-server openssh-client && \
    apt-get autoclean && \
    apt-get autoremove
RUN curl -O https://releases.hashicorp.com/vagrant/$(curl -s https://checkpoint-api.hashicorp.com/v1/check/vagrant  | \
    jq -r -M '.current_version')/vagrant_$(curl -s https://checkpoint-api.hashicorp.com/v1/check/vagrant  | \
    jq -r -M '.current_version')-1_amd64.deb && \
    dpkg -i vagrant_$(curl -s https://checkpoint-api.hashicorp.com/v1/check/vagrant  | \
    jq -r -M '.current_version')-1_amd64.deb && \
    vagrant plugin install vagrant-libvirt && \
    vagrant box add --provider libvirt peru/windows-10-enterprise-x64-eval && \
    vagrant init peru/windows-10-enterprise-x64-eval && \
    rm -rf vagrant_$(curl -s https://checkpoint-api.hashicorp.com/v1/check/vagrant | jq -r -M '.current_version')-1_amd64.deb
COPY startup.sh /
RUN chmod +x /startup.sh
ENTRYPOINT ["/startup.sh"]
