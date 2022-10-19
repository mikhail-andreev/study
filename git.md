GIT

git init - инициализирует репзиторий в текущей папке

git branch - показывает список веток

git branch branch-name - создает новую ветку 

git branch branch-name - переключается на последний комит в ветке branch-name

git checkout -b add/vasiliyshilov - создаст нам отдельную ветку + переключится в неё

git add . добавит в новый коммит все изменившиеся файлы в папке

git commit зафиксирует изменения

git push --set-upstream origin add/vasiliyshilov отправит изменения на гит сервер

git pull - забирает изменения с удаленного репозитория

git rm --cached <file> - не следить за файлом