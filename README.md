This is a docker demo app by python.

How to use


docker run -it --name alpine alpine sh

docker run --name webserver -p 80:80 -d nginx:alpine
docker exec -it webserver sh



docker run -d --name pythonapp --link redis -p 5000:5000 chunha/pythonapp:0.1
docker run --name redis -d redis:alpine



https://hub.docker.com/r/chunha/
https://github.com/legolegoman/pythonapp


my-svc.my-namespace.svc.cluster.local



docker service create \
--name web -d \
--replicas 1 \
-p 5000:5000 \
 be7ec8e5e51a

docker service create \
--name redis -d \
--replicas 1 \
-p 6379:6379 \
 redis:alpine


docker image inspect chunha/pythonapp:0.1
