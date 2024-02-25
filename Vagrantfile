$script = <<-SCRIPT
useradd student
usermod -aG wheel student
echo password | passwd student --stdin
SCRIPT

$network_script = <<-SCRIPT
nmcli connection add ifname enp0s8 \
    ipv4.method manual \
    ipv4.addresses $1/24 \
    ipv4.gateway 192.168.29.1 \
    ipv4.dns 8.8.8.8 \
    con-name enp0s8-manual \
    type ethernet
SCRIPT

Vagrant.configure("2") do |config|
    config.vm.define "control" do |h|
        h.vm.box = "redhat-gui/9.3"
        h.vm.hostname = "control.example.local"
        h.vm.network "private_network",
            virtualbox__intnet: true
        h.vm.provision "shell", inline: $script

        h.vm.provision "shell" do |s|
            s.inline = $network_script
            s.args = "192.168.29.190"
        end
        
        h.vm.provider :virtualbox

        h.vm.disk :disk, size: "20GB", name: "extra_disk"
    end
    config.vm.define "ansible1" do |h|
        h.vm.box = "redhat-gui/9.3"
        h.vm.hostname = "ansible1.example.local"
        h.vm.network "private_network",
            virtualbox__intnet: true
        h.vm.provision "shell", inline: $script
        h.vm.provision "shell" do |s|
            s.inline = $network_script
            s.args = "192.168.29.191"
        end
        
        h.vm.provider :virtualbox

        h.vm.disk :disk, size: "20GB", name: "extra_disk"
    end
    config.vm.define "ansible2" do |h|
        h.vm.box = "redhat-gui/9.3"
        h.vm.hostname = "ansible2.example.local"
        h.vm.network "private_network",
            virtualbox__intnet: true
        h.vm.provision "shell", inline: $script
        h.vm.provision "shell" do |s|
            s.inline = $network_script
            s.args = "192.168.29.192"
        end

        h.vm.provider :virtualbox

        h.vm.disk :disk, size: "20GB", name: "extra_disk"
    end
end
