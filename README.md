# Install Rancher on Rocky

Recruitment before install rancher
- [Docker installed](https://github.com/Yuzyzy88/install-docker-rocky)
  

### 1. Run docker command to start the Rancher container:
   
   ```
   $ sudo docker run -d --name=rancher --privileged --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher:latest
   ```
   
   It is maps host port 80 & 443 to the container port 80 & 443 respectively and starts the container in privileged mode

### 2. Check container status

  ```
  docker ps
  ```

### 3. Open broswer

  ```
  <ip address>:80
  ```

### 4. Enter password

  ```
  docker ps | grep -i rancher
  docker logs  <container-id>  2>&1 | grep "Bootstrap Password:"
  ```

### 5. If you want to install helm

  ```
  kubectl get secret --namespace cattle-system bootstrap-secret -o go-template='{{.data.bootstrapPassword|base64decode}}{{"\n"}}'
  ```


### 6. Install kubectl

  ```
  -LS https://dl.k8s.io/release/stable.txt`/bin/linux/amd64/kubectl
  ```

  change to excutable and move to your PATH

  ```
  chmod +x ./kubectl
  sudo mv ./kubectl /usr/local/bin/kubectl
  ```

  If */usr/local/bin* is not in your PATH. You can add to your bashrc

  ```
  vim ~/.bashrc
  ```

  add to the end and save file

  ```
  export PATH=$PATH:/usr/local/bin
  ```

  reload bashrc

  ```
  source ~/.bashrc
  kubectl version --client
  ```

### 7. Setting kube config
  - Download Kubeconfig from your cluster
  - Create directory  ``` mkdir -p ~/.kube```
  - Copy your config to ``` vim ~/.kube/config ```
