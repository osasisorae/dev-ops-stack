Vagrant.configure('2') do |config|
    servers=[
        {
            :hostname => 'control',
            :box => 'bento/ubuntu-20.04',
            :ip => '192.168.56.110',
            :ssh_port => '2201',
        },
        {
            :hostname => 'node1',
            :box => 'bento/ubuntu-20.04',
            :ip => '192.168.56.111',
            :ssh_port => '2202',
        },
        {
            :hostname => 'node2',
            :box => 'bento/ubuntu-20.04',
            :ip => '192.168.56.112',
            :ssh_port => '2203',
        },
        {
            :hostname => 'node3',
            :box => 'bento/ubuntu-20.04',
            :ip => '192.168.56.113',
            :ssh_port => '2204',
        }
    ]
    # add memory and cpu to each server
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network :private_network, ip: machine[:ip]
            node.vm.network 'forwarded_port', guest: 22, host: machine[:ssh_port], id: "ssh"
            node.vm.provider :virtualbox do |vb|
                vb.customize ['modifyvm', :id, '--memory', 512]
                vb.customize ['modifyvm', :id, '--cpus', 1]
            end
        end
    end
end