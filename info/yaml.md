apiVersion: la versión de la api de k8s que se va a utilizar
kind: tipo de objeto que se va a crear
Metadata: Muy útiles para las búsquedas
spec: Especificaciones técnicas


Crea el objeto pero nada mas
kubectl create -f fichero.yml 

Crea objeto y/o lo modifica
kubectl -f fichero.yml

Cuando creamos un pod
El valor de la propiedad kind es pod
Podemos indicar recursos requeridos y los recursos límite. 

dependiendo de donde se alojen los recursos se mediran los CPUS de la siguiente manera:
aws -> vCPU
GPC Core
Azure -- Vcore

si no expecificamos limites cogeran todos los recursos que necesiten


# PROPIEDADES BASICAS DE LOS PODS
containers:
volumes:
restartPolicy:
dnsPolicy:

#En cuanto a los TEMPLATES CONTAINERS:
image: 
imagePullPolicy: política de recuperación de imagen  
	IfNotPresent: si no está cacheada la baja
	Always:siempre la pide aunque esté cacheada
	Never: nunca pida la imagen
name:
ports:
env:
resources:





#EJEMPLOS:

##Ejemplo 1:

apiVErsion: v1
kind: Pod
metadata:
	name: redis
spec:
	containers:
	- name: redis
	  image: redis
	  volumeMounts:
	  - name: redis-storage
	    mountPath: /data/redis
	volumes:
	- name: redis-storage
	  emptyDir: {}



##Hay dos Lifecycle Hooks

PostStart: Se ejecuta justo al arranque del pod
PreStop: Se ejecuta justo antes de morir el pod --> por ejemplo las varibles de entorno o lo que se necesite

spec:
containers:
- name: nginx
  image: nginx
  lifecycle:
    postStart:
      exec:
        command: ["/sbin/bash", "-c", "echo hello > /usr/share/message"]


	
	
	