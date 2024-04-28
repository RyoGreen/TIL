# How to remove running container
## stop running container
`docker stop $(docker ps -q)`

## rm container
`docker rm $(docker ps -q -a)`

## remove image
`docker system prune -a --volumes`
