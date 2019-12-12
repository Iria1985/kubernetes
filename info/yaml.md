apiVersion: la versi�n de la api de k8s que se va a utilizar
kind: tipo de objeto que se va a crear
Metadata: Muy �tiles para las b�squedas
spec: Especificaciones t�cnicas


Crea el objeto pero nada mas
kubectl create -f fichero.yml 

Crea objeto y/o lo modifica
kubectl -f fichero.yml

Cuando creamos un pod
El valor de la propiedad kind es pod
Podemos indicar recursos requeridos y los recursos l�mite. 

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
imagePullPolicy: pol�tica de recuperaci�n de imagen  
	IfNotPresent: si no est� cacheada la baja
	Always:siempre la pide aunque est� cacheada
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




LOS NODOS TIENE QUE TENER ETIQUETAS PARA PODER HACER UN CONSTRAIN

kubectl label nodes nombrenodo 


apiVersion: v1
kind: Pod
metadata:
 name: nginx
spec:
containers:
- name: nginx
  image: nginx
noseSelector:
  type: tipo1
	
	
nodeName: es una forma m�s simple para la restricci�n de ejecuci�n de un Pod.

spec:
containers:
- name: nginx
  image: nginx
NodoName:
nombredelnodo


Si se cae el nodo se queda sin servicio. No recomendado sobretodo si se usan nodos en la nube.


##La pol�tica de restartPolice

Never
Always
OnFailure: se reinicia si el Pod falla. En caso de ser eliminado por el sistema o por el usuario no se reinicia.

	
	
	
# REPLICASET
apiVersion: apps/v1
kind: ReplicaSet

apiVersion: extensions/v1beta1
kind: ReplicaSet
metadata:
	name: nginx
spec:
	replicas: 2
	selector:
		matchLabels:
			app: nginx
	templates:
		metadata:
			labels:
				app: miApp
			spec:
				containers:
				- image: couva/application
				  name: application




#DEPLOYMENT

apiVersion: aaps/v1
kind: Deployment


casi siempre crearemos deployments
propiedades del deployment

replicas: 
revisionHistoryLimits:
selector:
	matchLables:
	matchExpressions:
strategy: Recreate|RollingUpdate
template: describe los pods que tiene que crear




EJEMPLO

apiVersion: extensions/v1beta1
kind: Deployment
metadata:
	name:nginx
spec:
	revisionHistoryLimit: 2
	strategy:
		type: RollingUpdate
	replicas: 2
	template:
		metadata:
			�abels
			app: miApp
		spec:
			containers.
				-image: civa/applicacion
				 name; aplicacion
				 
				 
				 
#SERVICIOS

apiVersion: v1
kind: Service

propiedades basicas
type
selector
ports:
	name:
	port: puerto interno
	targetport: puerto externo
	protocol:
	nodeport: externo



apiVErsion: v1
kind: Service
metadata:
	name: nginx
spec:
	tyoe: ClusterIP
	ports:
    - name: http
	  port: 80
	  targetPort: http
	selector:
		app: nginx
	

	
LOS SERVICIOS NUNCA SE CAEN --> ELLOS SE ENCARGARAN DE GESTIONAR LOS PUERTOS. UNA VEZ ASIGNADO UNO POR KUBERNETES SIEMPRE SER� EL MISMO

para eliminar todo lo que se haya de desplegado con el yml

kubectl delete -f nombrefichero.yml


para desplegar todo lo que est� en un yml
kubectl apply -f nombrefichero.yml

pero si hacemos un kubectl apply -f . instalar�amos todos los ymls de la carpeta actual.



