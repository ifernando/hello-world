VAGRANTFILE_API_VERSION = "2"
box      = 'ubuntu/trusty64'
url      = 'https://atlas.hashicorp.com/ubuntu/boxes/trusty64'
hostname = 'jenkins'
ip       = '192.168.5.99'
ram      = '1024'

Vagrant::Config.run do |config|
  config.vm.box = box
  config.vm.box_url = url
  config.vm.host_name = hostname
  config.vm.network :hostonly, ip 

  config.vm.customize [
    'modifyvm', :id,
    '--name', hostname,
    '--memory', ram
  ]
end

Vagrant.configure("2") do |config|
  config.vm.network "forwarded_port", guest: 8080, host: 9090
  config.vm.network "forwarded_port", guest: 8080, host: 9091
  config.vm.provision "ansible" do |ansible|
          ansible.verbose = "vvv"
          ansible.playbook = "jenkins.yml"
          ansible.inventory_path="ansible.host"
          ansible.limit = "all"
        end

end

