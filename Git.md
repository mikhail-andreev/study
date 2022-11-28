## GIT

git init - инициализирует репзиторий в текущей папке

git branch - показывает список веток

git branch branch-name - создает новую ветку 

git branch branch-name - переключается на последний комит в ветке branch-name

git checkout -b add/p.sergeev - создаст нам отдельную ветку + переключится в неё

git add . добавит в новый коммит все  файлы в папке

git add -A добавит в новый коммит все изменившиеся файлы в папке

git commit зафиксирует изменения

git push --set-upstream origin add/p.sergeev отправит изменения на гит сервер

git push --set-upstream origin $(git_current_branch) - то же самое

!!!!! git branch --set-upstream-to=origin/adsbid_parking adsbid_parking

git checkout master; - переключение в master

git pull - забирает изменения с удаленного репозитория

git rm --cached <file> - не следить за файлом

gaa; gc -m "обновлено"; gpsup

git add --all; git commit -v -m "суть изменений"; git push --set-upstream origin $(git_current_branch) -  Команда 3 в 1

git reset --hard HEAD - отмена последней операции

git rebase develop - слияение с переносом комитов из указаной в текущую 

git remote add - Добавить новый удаленный репо

git remote -v -  списое удаленных репозиториев

git rebase -i HEAD~3 - редактировать 3 последние коммита, например squash

