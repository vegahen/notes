# Kubernetes

colima start --kubernetes

kubectl version

## https://github.com/nigelpoulton/getting-started-k8s.git

docker build -t vegahen/getting-started-k8s:1.0 .

docker push vegahen/getting-started-k8s:1.0

kubectl get nodes

kubectl apply -f pod.yml

kubectl get pods --watch

kubectl get pods -o wide

kubectl describe pod hello-pod

kubectl apply -f multi-pod.yml

kubectl delete -f multi-pod.yml

kubectl expose pod hello-pod --name=hello-svc --target-port=8080 --type=NodePort

kubectl get svc

kubectl delete svc hello-svc

kubectl get pods --show-labels

kubectl apply -f svc-nodeport.yml

kubectl describe svc ps-nodeport

kubectl get ep

cat svc-lb.yml

kubectl delete pod hello-pod

kubectl apply -f deploy.yml

kubectl get deploy

kubectl get rs

kubectl rollout history deploy web-deploy

kubectl rollout undo deploy web-deploy --to-revision 1'

kubectl exec -it my-pod sh
