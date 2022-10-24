## Когда отвалились репозитории на CentOS 8:

sudo sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-*
sudo sed -i -e "s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g" /etc/yum.repos.d/CentOS-*


## Добавление репозитория PowerTools:

You can enable it with the following commands:
yum install dnf-plugins-core
And then:
yum config-manager --set-enabled powertools
Or:
yum config-manager --set-enabled PowerTools
You can also just open /etc/yum.repos.d/CentOS-PowerTools.repo with a text editor and set enabled= to 1 instead of 0'.

Run yum repolist and you'll see it.
EDIT:
The repo is now powertools instead of PowerTools when enabling it with yum. There was a bug so the developers may set it back to what it was before which is why both are listed. The repo file still has the same name.




