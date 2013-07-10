require 'berkshelf/vagrant'

Vagrant::Config.run do |config|
  config.vm.host_name = "openresty-buildpack"

  config.vm.box = "precise64"
  config.vm.box_url = "http://dl.dropbox.com/u/1537815/precise64.box"

  config.vm.network :hostonly, "33.33.33.10"
  
  config.ssh.max_tries = 40
  config.ssh.timeout   = 120

end
