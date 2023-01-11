## ANSIBLE:
 
ansible-inventory --list -y - воводит список подключенных серверов

ansible all -m ping -u root - тестирование подключения к серверам, вместо root - имя пользователя

ansible all -a "df -h" -u root - проверка использования дисков на всех подключенных серверах

ansible-playbook --check --diff zzz_test.yml - накатываение плэйбука в режиме проверки 

## Ускорение выполнения плейбука:

pipelining = true

[ssh_connection]
ssh_args = -o ControlMaster=auto -o ControlPersist=30m -o ServerAliveInterval=5 -o ServerAliveCountMax=0 -o ControlPath=/home/madfidel/.ssh/cm_socket/%r@%h:%p

## проверка доступности инфраструктуры:

ansible all --limit ':backup02-ovh:ovirt-node11-ovh:ovirt-node01-ovh:ovirt-node02-ovh:ovirt-node03-ovh:ovirt-node04-ovh:ovirt-node05-ovh:ovirt-node06-ovh:ovirt-node07-ovh:ovirt-node08-ovh:ovirt-node09-ovh:ovirt-node10-ovh:adsbid-stage-admin-ovh:adsbid-stage-cabinet-ovh:adsbid-stage-ch01-ovh:adsbid-stage-dsw01-ovh:adsbid-stage-dsw02-ovh:adsbid-stage-dsw03-ovh:adsbid-stage-lb01-ovh:adsbid-stage-lb02-ovh:adsbid-stage-lb02-ovh:adsbid-stage-rs01-ovh:adsbid-stage-tnt01-ovh:adsbid-ukraine-dsw01-ovh:crm-dev01-ovh:dmp-stage-rs01-ovh:dmp-stage-zoo01-ovh:dmp-stage-zoo02-ovh:dmp-stage-zoo03-ovh:dmp-stageas01-ovh:dmp-stageas02-ovh:dmp-stagecabdb01-ovh:dmp-stagech01-ovh:dmp-stagech02-ovh:dmp-stagedsw01-ovh:dmp-stagedsw02-ovh:dmp-stagedsw03-ovh:dmp-stagelb01-ovh:gitlab-dindrunner02-ovh:gitlab-techru:global-gitrun01-ovh:global-gitrun02-ovh:glpi-ovh:grafana-ovh:graylog-dsw01-ovh:graylog-dsw02-ovh:graylog-dsw03-ovh:graylog-els01-ovh:graylog-els02-ovh:graylog-els03-ovh:inf-test01-ovh:lb01-ovh:ns01-ovh:ns02-ovh:ns12-ovh:opentelemetry01-ovh:ovirt-mgr-ovh:ovirt-mgr-ovh.techhprof.ru:prom-agent-ovh:prom-vm01-ovh:qa-lt01-ovh:rtb-gitrun01-ovh:rtb-gitrun02-ovh:zabbix-db-ovh:zabbix-srv-ovh:rtb-dev-dsw01-ovh:rtb-dev-dsw02-ovh:rtb-dev-lb01-ovh:rtb-stage-as01-ovh:rtb-stage-as02-ovh:rtb-stage-as03-ovh:rtb-stage-as04-ovh:rtb-stage-ch01-ovh:rtb-stage-ch02-ovh:rtb-stage-ch03-ovh:rtb-stage-kdb01-ovh:rtb-stage-mdb01-ovh:rtb-stage-ml01-ovh:rtb-stage-pg01-ovh:rtb-stage-rs01-ovh:rtb-stage-rs02-ovh:rtb-stage-rs03-ovh:rtb-stage-rs11-ovh:rtb-stage-rs12-ovh:rtb-stage-rs13-ovh:rtb-stage-rs14-ovh:rtb-stage-zoo01-ovh:rtb-stage-zoo02-ovh:rtb-stage-zoo03-ovh:rtb-stagecab-ovh:rtb-stagedsw01-ovh:rtb-stagedsw02-ovh:rtb-stagedsw03-ovh:rtb-stagelb01-ovh:spo-web-ovh:tracker-dev-cabinet-ovh:tracker-dev01-ovh:tracker-preland02-ovh:vitrina-dev02-ovh:vitrina-mon01-ovh:vitrina-stage-dsw01-ovh:vitrina-stage-dsw02-ovh:vitrina-stage-dsw03-ovh:vitrina-stage-lb01-ovh:vitrina-stage-lb02-ovh:vitrina-stage-mdb01-ovh:vitrina-testdb01-ovh:vitrina-testdb01-ovh:vitrina-testdb02-ovh:vitrina-testdb02-ovh:vitrina-testdb03-ovh:vitrina-testdb03-ovh:vpn-land-ovh' -u s.hudoyarov -m ping | grep -P 'SUCCESS|UNREACHABLE'