borg mount /opt/backups/borg/infrastructure/gitlab-techru /opt/restore_check/   # подмонтировать бэкап какпапку  
borg umount /opt/restore_check/ #размонтировать папку бэкапа  
borg prune --list --keep-daily 14 --keep-weekly 8 --keep-monthly 12 --dry-run borg@203.0.113.112:my_repo  # очистка бэкапа 
borg check -v /opt/backups/borg/infrastructure/gitlab-techru - проверка бэкпапа
