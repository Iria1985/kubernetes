# kubernetes

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

