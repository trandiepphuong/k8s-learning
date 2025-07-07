# install helm

```
wget https://get.helm.sh/helm-v3.16.2-linux-amd64.tar.gz
tar xvf helm-v3.16.2-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/bin/
helm version
```

# install Ingress controller

```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm pull ingress-nginx/ingress-nginx
tar -xzf ingress-nginx-4.12.3.tgz
kubectl create ns ingress-nginx
helm -n ingress-nginx install ingress-nginx -f ingress-nginx/values.yaml ingress-nginx
```

# docker build and push
```
docker buildx build \  
 -t trandiepphuongdev/ecommerce-frontend:v2 \
 --push .
```
# install metric-server
```
helm repo add  metric-server https://kubernetes-sigs.github.io/metrics-server/
helm pull metric-server/metrics-server
tar -xvf metrics-server-*
helm install metric-server metrics-server -n kube-system
```

horizontal-pod-autoscaler-upscale-delay: Khoảng thời gian tối thiểu giữa các lần scale up (mặc định là 3 phút).
horizontal-pod-autoscaler-downscale-delay: Khoảng thời gian tối thiểu giữa các lần scale down (mặc định là 5 phút).
horizontal-pod-autoscaler-sync-period: Chu kỳ mà HPA kiểm tra lại tài nguyên và cập nhật trạng thái (mặc định là 15 giây).

# install nfs-server
```
sudo apt install nfs-server -y
sudo mkdir /data
sudo chown -R nobody:nogroup /data
sudo chmod -R 777 /data
sudo vi /etc/exports
# add line ====>     /data *(rw,sync,no_subtree_check)
sudo exportfs -rav
sudo systemctl restart nfs-server
```