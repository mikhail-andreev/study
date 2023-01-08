## ANSIBLE:
 
ansible-inventory --list -y - воводит список подключенных серверов

ansible all -m ping -u root - тестирование подключения к серверам, вместо root - имя пользователя

ansible all -a "df -h" -u root - проверка использования дисков на всех подключенных серверах

ansible-playbook --check --diff zzz_test.yml - накатываение плэйбука в режиме проверки 

## Ускорение выполнения плейбука:

pipelining = true

[ssh_connection]
ssh_args = -o ControlMaster=auto -o ControlPersist=30m -o ServerAliveInterval=5 -o ServerAliveCountMax=0 -o ControlPath=/home/madfidel/.ssh/cm_socket/%r@%h:%p