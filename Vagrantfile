# -*- mode: ruby -*-
# vi: set ft=ruby :

# Copyright (c) 2014, Shigemi ISHIDA
# All rights reserved.
# 
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
# 1. Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in the
#    documentation and/or other materials provided with the distribution.
# 3. Neither the name of the Institute nor the names of its contributors
#    may be used to endorse or promote products derived from this software
#    without specific prior written permission.
# 
# THIS SOFTWARE IS PROVIDED BY THE INSTITUTE AND CONTRIBUTORS ``AS IS'' AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED.  IN NO EVENT SHALL THE INSTITUTE OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
# OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
# SUCH DAMAGE.

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  #----------------------------------------------------------------------
  # base box
  config.vm.box = "debian-jessie-a1-x11"
  config.vm.box_url = "http://www.f.ait.kyushu-u.ac.jp/~ishida/vagrant-box/debian-jessie-a1-x11_x86-64_jp.box"

  #----------------------------------------------------------------------
  # network
  #----------------------------------------------------------------------
  #------------------------------
  # shared folder
  #------------------------------
  config.vm.synced_folder "tinyos-main", "/home/vagrant/tinyos-main"

  #----------------------------------------------------------------------
  # vm specific config
  #----------------------------------------------------------------------
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.customize ["modifyvm", :id, "--memory",  "4096"]
    vb.customize ["modifyvm", :id, "--cpus",    "2"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
  end

  #----------------------------------------------------------------------
  # provisioning
  #----------------------------------------------------------------------
  # chef auto install
  config.omnibus.chef_version = :latest
  config.vm.provision "chef_solo" do |chef|
    chef.cookbooks_path = "cookbooks"
    # chef.log_level = :debug
    chef.json = {
      "tinyos" => {
        "main-dir" => "~/tinyos-main"
      }
    }

    chef.add_recipe "apt"
    chef.add_recipe "git"
    chef.add_recipe "chef-tinyos"
  end
end
