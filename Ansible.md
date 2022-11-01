## ANSIBLE:
 
ansible-inventory --list -y - воводит список подключенных серверов

ansible all -m ping -u root - тестирование подключения к серверам, вместо root - имя пользователя

ansible all -a "df -h" -u root - проверка использования дисков на всех подключенных серверах

ansible-playbook --check --diff zzz_test.yml