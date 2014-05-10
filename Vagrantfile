VM_MEMORY = ENV.fetch("VM_MEMORY", 6*1024).to_i
VM_CORES = ENV.fetch("VM_CORES", 4).to_i
BOX_VERSION = 186
IOAPIC = VM_CORES >= 2 ? "on" : "off"

Vagrant.configure('2') do |config|

  config.vm.hostname='bosh-lite'
  config.vm.box = "boshlite-ubuntu1204-build#{BOX_VERSION}"
  config.vm.network :private_network, ip: '192.168.50.4'

  config.vm.provider :virtualbox do |v, override|
    override.vm.box_url = "http://bosh-lite-build-artifacts.s3.amazonaws.com/bosh-lite/#{BOX_VERSION}/boshlite-virtualbox-ubuntu1204.box"
    v.customize ["modifyvm", :id, "--memory", VM_MEMORY]
    v.customize ["modifyvm", :id, "--cpus", VM_CORES]
    v.customize ["modifyvm", :id, "--ioapic", IOAPIC]
  end

  config.vm.provider :vmware_fusion do |v, override|
    override.vm.box_url = "http://bosh-lite-build-artifacts.s3.amazonaws.com/bosh-lite/#{BOX_VERSION}/boshlite-vmware-ubuntu1204.box"
    v.vmx["numvcpus"] = VM_CORES
    v.vmx["memsize"] = VM_MEMORY
  end

end
