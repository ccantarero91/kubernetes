# kubernetes
Curso de Cubernetes con devacademy


# Set up
```
yum install -y git

yum install -y curl


#Install docker

yum install -y yum-utils \

      device-mapper-persistent-data \

      lvm2

yum-config-manager \

    --add-repo \

    https://download.docker.com/linux/centos/docker-ce.repo

yum install -y docker-ce-17.06.1.ce

systemctl start docker

systemctl enable docker

#Export para que tire
export PATH=$PATH:/usr/local/bin


#Install Kubectl 

cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
yum install -y kubectl

#Install Minikube 

curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.30.0/minikube-linux-amd64 && chmod +x minikube && sudo cp minikube /usr/local/bin/ && rm -f minikube

minikube start --vm-driver=none

#Probar instalacion

kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.10 --port=8080

kubectl expose deployment hello-minikube --type=NodePort

curl $(minikube service hello-minikube --url)
```


# Comentarios del curso
Kuberentes mas sencillo que mesos (docker swam ni loco)

Un conjunto de nodos de k8 seria un cluster.

Si el sistema se cae un nodo o varios, se van añadiendo mas maquinas o escalando las mismas de forma vertical.

El master es el encargado de administrar el resto de nodos (que no deja de ser a su vez otro nodo del cluster, pero con otro tipo de software o mas instalado). Si el master se cae, es un problema, por ello lo suyo seria tener master de bk.



API server : donde lanzamos las peticiones
Etcd : donde se almacena la info de las aplicaciones, info de los nodos, de los master 
Scheduler : encargado de administrar el cluster, levanta las apps, el encargado de levantar el trabajo dentro de los nodos
Kube: es la que informa al master
Controller: cerebro principal => le indica al master cuando se ha caido un nodo.

Sigo en ppt (master vs node)

Comandos
kubectl get replicaset
Nos saca todas las replicasset que tenemos ahí lanzadas
kubectl rollout history deployment/myapp-rs-frontend
Para sacar la historia de cambios que ha habido de rollput en el deplyment que le pasemos
kubectl rollout undo deployment/myapp-rs-frontend --to-revision=1
Para volver a una revision en concreto de las que se muestran en el history
Kubectl describe {deployment|pod|replicaset} id
Muestra la información del objeto indicado


# PPT

[PPT](Curso%20Docker+K8s-2.pptx)
