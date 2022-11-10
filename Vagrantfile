Vagrant.configure('2') do |config|
    servers=[
        {
            :hostname => 'control',
            :box => 'spirit/ubuntu-20.04',
            :ip => '10.0.2.21',
            :hostname => '9111',
        },
        {
            :hostname => 'node1',
            :box => 'spirit/ubuntu-20.04',
            :ip => '10.0.2.22',
            :hostname => '9211',
        },
        {
            :hostname => 'node2',
            :box => 'spirit/ubuntu-20.04',
            :ip => '10.0.2.23',
            :hostname => '9311',
        },
        {
            :hostname => 'node3',
            :box => 'spirit/ubuntu-20.04',
            :ip => '10.0.2.24',
            :hostname => '9411',
        }
    ]

    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network :private_network, ip: machine[:ip]
            node.vm.network 'forwaded_port', guest: 22, host: machine[:ssh_port], id: "ssh"
            node.vm.provider :virtualbox do |vb|
                vb.customize ['modifyvm', :id, '--memory', 512]
                vb.customize ['modifyvm', :id, '--cpus', 1]
            end
        end
    end
end