## Установка 

sudo apt update

sudo apt install apt-transport-https

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt update

sudo apt install docker-ce

sudo systemctl status docker

sudo usermod -aG docker $USER

docker ps
docker ps -a
docker images

## Вывод списка контейнеров имеет следующий вид:

docker container ls [options]

## Вывод инфы о контейнере:

ocker inspect [OPTIONS] NAME|ID [NAME|ID...]

## Очистка неиспользуемых контейнеров

docker system prune -f

## Запуск bash в контейнере

docker exec -it eb3c425838a8 bash -l

## Удаление контейнеров или образов

docker rm -f $(docker ps -aq)        # Delete all Containers
docker rmi -f $(docker images -q)    # Delete all Images

## Сохранение образа или контейнера в файл

docker save image:tag > arch_name.tar
docker load -i arch_name.tar





!!!!! docker service update cadvisor --force