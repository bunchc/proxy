nodes = {
    #'proxy'   => [1, 110],
    'proxy2'   => [1, 110],
}

Vagrant.configure("2") do |config|
    config.vm.box = "precise64"
    config.vm.box_url = "http://files.vagrantup.com/precise64.box"

    nodes.each do |prefix, (count, ip_start)|
        count.times do |i|
            hostname = "%s" % [prefix, (i+1)]

            config.vm.define "#{hostname}" do |box|
                box.vm.hostname = "#{hostname}.book"
                box.vm.network :public_network

                box.vm.provision :shell, :path => "#{prefix}.sh"

                # If using Fusion
                box.vm.provider :vmware_fusion do |v|
                    v.vmx["memsize"] = 512
                end
                # Otherwise using VirtualBox
                box.vm.provider :virtualbox do |vbox|
                    # Default to 1Gb RAM
                    vbox.customize ["modifyvm", :id, "--memory", 512]
                end
            end
        end
    end
end
