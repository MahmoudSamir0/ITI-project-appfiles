# ITI-project-appfiles

1.prepare your [infrastructure](https://github.com/MahmoudSamir0/ITI-project-infrastructure) 


## now your infrastructure is ready 

## connect to your private instance using ssh

 **copy this command before that modify the require in <>**


 ```shell script
 gcloud compute ssh --zone "<zone of your instance>" "<instance id>" --tunnel-through-iap --project "<project id>"
```

## you are now in your private machine

install kubetcl 
- [kubectl](https://kubernetes.io/docs/tasks/tools)


- install google-cloud-sdk-gke-gcloud-auth-plugin 

 **copy this command**

```shell script
sudo apt-get install google-cloud-sdk-gke-gcloud-auth-plugin
```


### connect to your cluster

 **copy this command before that modify the require in <>**


```shell script
gcloud container clusters get-credentials <cluster name> --zone <zone> --project <project id>
```

you will get this massage 

```
Fetching cluster endpoint and auth data.
kubeconfig entry generated for <cluster name>.
```


install git you can clone this repo in your private machine

[git](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-debian-10)


clone this repo 

```shell script
git clone https://github.com/MahmoudSamir0/ITI-project-appfiles.git
```

go to repo dir

```shell script
cd ITI-project-appfiles
``` 

you can see files


```shell script
ls 
```



## Configure Docker & gcloud to work with GCR of your project
1. run following command  to login in your cli 
- login to your  account in (google cloud platform)

 **copy this command**

  ```shell script
  gcloud auth login
  ```
2. be sure that you have install docker 
- [docker](https://docs.docker.com/engine/install/)

3.  to use docker without sudo 

 **copy this command**
  
  ```shell script
 sudo usermod -a -G docker ${USER}
```
4.   **copy this command**


  ```shell script
 VERSION=2.1.5
OS=linux  # or "darwin" for OSX, "windows" for Windows.
ARCH=amd64  # or "386" for 32-bit OSs, "arm64" for ARM 64.

curl -fsSL "https://github.com/GoogleCloudPlatform/docker-credential-gcr/releases/download/v${VERSION}/docker-credential-gcr_${OS}_${ARCH}-${VERSION}.tar.gz" \
| tar xz docker-credential-gcr \
&& chmod +x docker-credential-gcr && sudo mv docker-credential-gcr /usr/bin/
```
 **copy this command**

  ```shell script

gcloud auth configure-docker
```
 **copy this command**

```shell script
docker-credential-gcr configure-docker
```
```shell script
sudo chmod 666 /var/run/docker.sock
```
go to your yaml files of your jenkins

```shell script
cd jenkins
```
##  now you can build and push 

## prepare your jenkins 

 **copy this command**

1.create namespace

```shell script
kubectl create namespace devops-tools
```

2.create service account 

```shell script
kubectl apply -f serviceAccount.yaml
```

3.create your volumes

```shell script
kubectl apply -f volume.yml
```
4. create your deployment 

```shell script
kubectl apply -f deployment.yaml
```
5. create your service 

```shell script
kubectl apply -f service.yaml
```
## now jenkins is ready 

## prepare  agent for jenkins

1.

``shell script
cd ../my-agent
```
now your now in your agent file

2. run your agent deployment

```shell script
kubectl apply -f agent.yaml
```

3. run service for your agent

```shell script
kubectl apply -f agent_svc.yaml
```

## now your agent is ready

now open your agent

```shell script
kubectl exec -it -n <name of agent> -- /bin/bash
```

```shell script
service ssh start
```

change password for jenkins user

```shell script
passwd jenkins
```

```shell script
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```

``shell script
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
```


```shell script
apt-get update && apt-get install google-cloud-cli
```

```shell script
apt-get install google-cloud-sdk-gke-gcloud-auth-plugin

```

```shell script
su - jenkins
```

```shell script
chmod 666 /var/run/docker.sock
```
```shell script
gcloud auth configure-docker
```

make the agent to connect to your cluster

```shell script
gcloud container clusters get-credentials <cluster name> --zone <zone> --project <project id>

```

verify by running 

```shell script
kubectl get node
```
## get external ip of service of your jenkins 

```shell script
kubectl get service -n devops-tools
```
take it and open it in your browser


 kubectl get po -n devops-tools

```shell script
 kubectl get po -n devops-tools
```

```shell script
kubectl exec -it -n <jenkins-name> -- /bin/bash
```

now your now inside the pod

now take the path of password appearing in front of you in your browser

```shell script
cat /var/jenkins_home/secrets/initialAdminPassword
```


take the password to your jenkins

complete the information of 


# now you are in jenkins and its ready


## configer your agent to be ready



























