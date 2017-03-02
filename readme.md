## Vagrant - OCS Inventory - Hyper-V
Create a centos7 vm and configure Hyper-V

#### Notes

* Networking - you must be using a network where the VM can DHCP boot

* Networking - "onenetwork" should be swapped out for the name of your virtual switch

* TemporaryFix - once fixed the line "sed -i -e s/7010/7011/ /usr/share/ocsinventory-reports/ocsreports/var.php" should be removed

* Database setup - Admin: root     Password: <blank>    Database: ocsweb    Server: localhost

* Default usr/pwd: admin:admin