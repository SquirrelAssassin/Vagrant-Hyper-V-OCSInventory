$script = <<SCRIPT
sed -i /etc/sysconfig/selinux -r -e 's/^SELINUX=.*/SELINUX=permissive/g'
sed -i /etc/selinux/config -r -e 's/^SELINUX=.*/SELINUX=permissive/g'
yum install -y make gcc net-tools autoconf vim git httpd mariadb-server mod_perl php-pecl-zip php-gd php-mbstring.x86_64 php-soap epel-release  \
perl-ExtUtils-MakeMaker mod_php perl-XML-Simple perl-Net-IP perl-SOAP-Lite cpan php-mysql httpd-devel* perl-CPAN perl-Archive-Zip perl-Net-IP perl-XML-Simple \
perl-SOAP-Lite perl-ExtUtils-Embed perl-XML-Entities perl-ExtUtils-CBuilder
(echo y;echo o conf prerequisites_policy follow;echo o conf commit)|cpan
thing=('YAML' 'ExtUtils::Install' 'Archive::Zip' 'ModPerl::MM' 'Apache::DBI' 'Apache2::SOAP' 'Net::IP' 'XML::Simple' 'Compress::Zlib' 'XML::Entities' )
for i in "${thing[@]}"; do cpan -i $i; done
systemctl start mariadb.service
systemctl enable mariadb.service
systemctl enable httpd.service
yum -y update
git clone https://github.com/OCSInventory-NG/OCSInventory-Server.git
git clone https://github.com/OCSInventory-NG/OCSInventory-ocsreports.git ./OCSInventory-Server/ocsreports
cd OCSInventory-Server/
chmod u+x setup.sh
yes " " | sh setup.sh
sed -i -e s/7010/7011/ /usr/share/ocsinventory-reports/ocsreports/var.php
reboot
SCRIPT
Vagrant.configure("2") do |config|
config.ssh.insert_key = false
config.vm.box_check_update = false 
config.vm.synced_folder ".", "/vagrant", disabled: true
config.vm.network :private_network, "bridge": "onenetwork"
  config.vm.define :ocs do |ocs|
        ocs.vm.box = "cdaf/CentOSLVM"
		ocs.vm.provider :hyperv do |ocs| 
		ocs.vmname = "ocs"
		ocs.memory = "2048"
		ocs.cpus = 2 
		ocs.differencing_disk = "true"
	  end
      ocs.vm.provision "shell", inline: $script
	end
end 
