kubectl set image deployment/<nombre> <pod>=imagen --all

kubectl rollout history deployment/nginx

kubectl rollout undo deployment/nginx

kubectl expose deploument/<nombre> --name=<nombre> --port=<port> --type=<tiposervicio> --target-port=<port>


kubectl run nginx --image=nginx --restar=Always --port=80 --expose=true
