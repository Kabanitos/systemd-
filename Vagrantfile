MACHINES = {
  # Имя DV "pam"
  :"systemd" => {
              # VM box
              :box_name => "centos/7",
              # Количество ядер CPU
              :cpus => 2,
              # Указываем количество ОЗУ (В Мегабайтах)
              :memory => 1024,
              # Указываем IP-адрес для ВМ
              :ip => "192.168.57.10",
            }
}

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.network "private_network", ip: boxconfig[:ip]
    config.vm.define boxname do |box|
      box.vm.box = boxconfig[:box_name]
      box.vm.box_version = boxconfig[:box_version]
      box.vm.host_name = boxname.to_s

      box.vm.provider "virtualbox" do |v|
        v.memory = boxconfig[:memory]
        v.cpus = boxconfig[:cpus]
      end
    
      box.vm.provision "ansible" do |ansible|
				ansible.playbook = "ansible/playbook.yml"
				ansible.inventory_path = "ansible/inventory.yml"
				ansible.host_key_checking = "false"
				ansible.limit = "all"
      end
    end
  end
end

