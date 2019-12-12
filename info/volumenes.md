#EMPTY DIR
Empty Dir para cosas temporales
La duracion del volumen es la misma que la duracion del pod
se usa para compartir volumenes con los contenedores de un mismo pod

Los contenedores van a montar los volumenes

apiVersion: v1
kind: Pod
metadata:
	name: myapp
apec:
	containers:
	- name: myapp
	  image: nginx
	  volumeMounts:
	  	- mountPath: /myImages
	  	name: myimages
volumes:
	- name: myimages
		emptyDir: {}
		
/VAR/LIB/KUBELET/POD/POUID/VOLUMES/KUBERNETES.IO.DIR/VOLUMEMANE
		
# HOSTPATH

hostPath

compartimos una carpeta del host con un volumen en el contenedor. En este volumen indicamos path y typo

tipos de datos que tenemos

cadena vacía
directoryorcreate
directory
fileorcreate
file
socker, chardevice, blockdevice


apiVersion: v1
kind: Pod
...
spec:
	containers:
		- name: myapp
		  images: nginx
		  volumeMounts:
		  - mountPath: /mydata
		    name: my-volume
		
volumes:
	- name: my-volume
		hostPath: 
		
		
# CLOUDS

getPersistentDisk: google
awsElasticBlockStore: aws
azureDisk: azure
nfs: on-promise


gcePersistentDisk

volumes:
	- name: my-volumen
      gcePersistentDisk:
      	pdName: vol-eb
      	fsType: ext4
      	
 awsElasticBlockStore
 
 
 azure
 
 az disk create\
  --resource-group MC_myResource
  
  
  
  
  ## PERSISTETVOLUME
  recomendado a utilizar. Se necesita hacer un nuevo yml con el volumen y habra que montarlo en el deployment
  
  apiVersion: v1
  kinfd: PersitentVolume
  metadata:
  	name: nginx-pv-volume
  	labels:
  		type: local
  spec:
  	storateClassName: manual
  	capacity:
  		storage: 2Gi
  	accessmodes:
  		- ReadWriteOnce | ReadOnlyMany | ReadWriteMAny
  	hostPath:
  	path: /mnt/data
  	
 #PERSISTENT VOLUME CLAIM
 
 almacena un volumen por una capacidad por parte de un usuario
 
 cogemos un tamaño y me da igual que volumenes hay
 
 
 kind: PersistentVolumeClaim
 apiVersion: v1
 metadata:
 	name: nginx-pv-claim
 spec:
 	storageClassName: manual
 	accessMods:
 		-Read



# PERSISTENVOLUMECLAIMSDYNAMICS

crea un persistent volume a demanda. Se utiliza en cloud
peligro crear discos que luego son abandonados.

el cluster debe arrancar de una forma especifica para poder usarlo.
no se suele utilizar por que tiene un coste muy elevado
NO USAR 

