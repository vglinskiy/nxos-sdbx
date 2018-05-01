Vagrant.configure(2) do |config|
  config.vm.base_mac = "0800276CEE0E"
  config.vm.define "nxos" do |nxos|
    nxos.vm.box = "nxos-sdbx"
    nxos.ssh.insert_key = false
    nxos.vm.boot_timeout = 180
    nxos.vm.synced_folder '.', '/vagrant', disabled: true
    nxos.vm.network :forwarded_port, guest: 80, host: 8980, id: 'http'
    nxos.vm.network :forwarded_port, guest: 22, host: 5522, id: 'ssh'
    nxos.vm.network :forwarded_port, guest: 830, host: 8830, id: 'netconf'
    nxos.vm.provider :virtualbox do |vb|
      vb.name = "nxos-sdbx"
      vb.customize ['modifyvm',:id,'--uartmode1','server','/tmp/nxos-sdbx']
      vb.customize "pre-boot", [ 
                        "storageattach", :id,
                        "--storagectl", "SATA",
                        "--port", "1",
                        "--device", "0",
                        "--type", "dvddrive",
                        "--medium", "./nxos-sdbx.iso"
       ]
    end
  end
end

