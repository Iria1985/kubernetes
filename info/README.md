jmcousino@pymit.es
jsanchez@pymit.es

# kubernetes
¿Que és un pod? Es la unidad mínima de kubernetes.

Lo más recomendable es tener un pod por contenedor por si tenemos que escalar el pod no consumamos recursos sin necesidad.

## Arrancar un pod
kubectl run nginxpod --image=nginx --restart=Never
pod/nginxpod created

## Listar los pods que tenemos 
Si automáticamente hacemos un listado de pods una vez arrancado veremos que nos pone STATUS=ContainerCreating

C:\Users\Iria>kubectl get pods
NAME       READY   STATUS              RESTARTS   AGE
nginxpod   0/1     ContainerCreating   0          9s


Le damos un rato y volvemos a listar y nos da STATUS=Running que sería lo correcto

C:\Users\Iria>kubectl get pods
NAME       READY   STATUS              RESTARTS   AGE
nginxpod   0/1     Running   0          49s

## Listar los pods y ver en que nodo están corriendo
kubectl get pods -o wide

NAME       READY   STATUS    RESTARTS   AGE   IP          NODE             NOMINATED NODE   READINESS GATES
nginxpod   1/1     Running   0          33m   10.1.0.11   docker-desktop   <none>           <none>

# Se queda espiando que pasa con los pods
kubectl get pods --watch

#eliminar un pod
kubectl delete pod nginxpod
pod "nginxpod" deleted

# Ver información del pod =>  
kubectl describe pod nginxpod

Name:               nginxpod
Namespace:          default
Priority:           0
PriorityClassName:  <none>
Node:               docker-desktop/192.168.65.3
Start Time:         Wed, 11 Dec 2019 16:41:53 +0100
Labels:             run=nginxpod
Annotations:        <none>
Status:             Running
IP:                 10.1.0.12
Containers:
  nginxpod:
    Container ID:   docker://a2b4809c43304eb41b1e2fb05a7ce2bfe1e36204a57a7773f4bc6c103bb562d1
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:50cf965a6e08ec5784009d0fccb380fc479826b6e0e65684d9879170a9df8566
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 11 Dec 2019 16:41:59 +0100
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-5slfx (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  default-token-5slfx:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-5slfx
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age   From                     Message
  ----    ------     ----  ----                     -------
  Normal  Scheduled  10s   default-scheduler        Successfully assigned default/nginxpod to docker-desktop
  Normal  Pulling    7s    kubelet, docker-desktop  Pulling image "nginx"
  Normal  Pulled     5s    kubelet, docker-desktop  Successfully pulled image "nginx"
  Normal  Created    5s    kubelet, docker-desktop  Created container nginxpod
  Normal  Started    4s    kubelet, docker-desktop  Started container nginxpod


## KUBERNETES SE BASA EN ETIQUETAS
kubectl get pod -l <valor>
kubectl get pod -l <clave>=<valor>

kubectl get pod -l run=nginxpod


Podemos encontrar las etiquetas establecidas en un pod con un describe pod bajo "labels"


kubectl exec -it nombrecompletodelpod /bin/bash

con este comando te conectas al pod. Si el pod solo contiene un contenedor automaticamente al conectarte al pod te conectarías a ese contenedor.
Si el pod contiene más de un contenedor tendriamos que dar el nombre del pod y también del contenedor a conectarnos.



## Apertura de puertos
KUBECTL PORT-FORWARD
Esto solo es para probar, se queda siempre con el prompt

kubectl port-forward nginxpod 8000:80

#ETIQUETAS

se pueden utilizar con pods, deployments, manifest etc.
Se utilizan sobretodo para buscar

### Establecer label
kubectl label pod <nombrepod> app=miaplicacion

### mostrar las labels que tengan los pods
kubectl get pod --show-labels

#mostrar todo lo q tenemos
kubectl get all

NAME           READY   STATUS    RESTARTS   AGE
pod/nginxpod   1/1     Running   0          20m

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   43h


## escalar horizontalmente

kubectl replicaset scale <nombrepod> --replicas=5


