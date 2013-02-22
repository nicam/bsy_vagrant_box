# -*- mode: ruby -*-
# vi: set ft=ruby :

def Kernel.is_windows?
    # Detect if we are running on Windows
    processor, platform, *rest = RUBY_PLATFORM.split("-")
    platform == 'mingw32'
end

Vagrant::Config.run do |config|
  config.vm.define :main do |main_config|
    main_config.vm.box = "liip-squeeze64"
    main_config.vm.box_url = "http://vagrantbox.liip.ch/liip-squeeze64.box"
    main_config.vm.network :hostonly, "10.11.12.14"
    main_config.vm.forward_port 3306, 13307
    main_config.vm.forward_port 80, 8080
    main_config.vm.share_folder "v-root", "/vagrant", ".", :nfs => !Kernel.is_windows?
    main_config.vm.provision :puppet, :module_path => "puppet/modules" do |puppet|
      puppet.manifests_path = "puppet/manifests"
      puppet.manifest_file = "main.pp"
    end
  end
end

