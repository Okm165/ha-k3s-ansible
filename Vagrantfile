Vagrant.configure("2") do |config|
    MasterNodesCount = 3

    # Kubernetes Master Nodes
    (1..MasterNodesCount).each do |i|
        config.vm.define "k8smaster#{i}" do |masternode|
            masternode.vm.box = "pavlnowak/fedora38-cloud"
            masternode.vm.box_version = "38.0.0"

            masternode.vm.provider :libvirt do |libvirt|
                libvirt.management_network_mode = "none"
                libvirt.driver = "kvm"
                libvirt.uri = "qemu:///system"
                # libvirt.storage_pool_name = "imgs"
                libvirt.memory = 4096
                libvirt.cpu_mode = "host-passthrough"
                libvirt.cpus = 4
                libvirt.cputopology :sockets => "1", :cores => "2", :threads => "2"
            end

            masternode.vm.hostname = "k8smaster#{i}"
            masternode.vm.network "public_network", :dev => "enp0s31f6"

            masternode.vm.provision "ansible" do |ansible|
                ansible.compatibility_mode = "2.0"
                ansible.playbook = "playbook.yaml"
            end
        end
    end
end
  