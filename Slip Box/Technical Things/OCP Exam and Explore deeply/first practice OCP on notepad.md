#ocp #ocpexam #exams 

# Q.1-2-3
======================

## Q.1
$ htpasswd -c -b -B htpass-ex280 jobs jobs123
$ htpasswd -b -B htpass-ex280 wozniak wozniak123
$ htpasswd -b -B htpass-ex280 collins collins123
$ htpassd -b -B htpass-ex280 alderin alderin123

$ oc create secret generic htpass-idp-280 --from-file=htpasswd=/home/student/htpass-ex280 -n openshift-config

$ oc get secrets 

$ oc get ouath cluster -o yaml > ouath.yaml
$ vi oauth.yaml


spec:
  identityProviders:
  - name: htpass-ex280
    mappingMethod:claim
	type: HTPasswd
	htpasswd:
	  fileData: htpass-idp-ex280         //provide secret name
	  
	  
$ oc apply -f ouath.yaml	  
$ watch oc get pods
	    
 
$ oc login -u jobs -p jobs123
$ oc login -u wozniak -p wozniak123
$ oc login -u aldrin -p alderin123

// YOu must have loged in every user
$ oc login -u armstrong -p armstrong123


--------
## Q.2

$ oc adm policy add-cluster-role-to-user cluster-admin jobs 
// cluster role has been added to jobs
$ oc get clusterrole self-provisioner
$ oc get clusterrolebindings self-provisioner

// remove self-provisioner access

$ oc adm  remove role-from-group self-provisioner system:authenticated:auth
$ oc adm policy add-cluster-role-to-user self-provisioner wozniak
$ oc delete secret kubeadmin -n kube-system


------------
## Q.3
$ oc project apache
$ oc create quata -h
$ oc create quota ex280-quota --hard=cpu=2,memory=1Gi, pods=3, services=6, replicationcontrollers=3 --dry-run=client -o yaml > ex280-quota.yaml

--------

# Q.4-5-6

## Q.4
$ oc adm groups new commander 
$ 
...write here
## Q.5
$ oc create quata --help l less
=> Include --hard also

## Q.6
vim limits.yaml

apiversion: v1
kind: LimitRange
metadata: 
  name: ex280-limits
  namespace: bluebook
  
spec: 
  limits:
    - type: pod
	  max: 
	    cpu: "500m"
		memory: "300Mi"
	  min: 
	    cpu: "10m"
		memory: "100Mi"
		
	- type: container
	  max: 
	    cpu: "500m"
		memory: "300Mi"
	  min:
	    cpu: "10m"
		memory: "100Mi"
		
	  defaultRequests:
	    memory: "100Mi"
		cpu: "100m"
		
wq!


oc project
$ oc project bluebook
$ oc get limitranges

oc apply -f limitranges.yaml



-------------
# Q.7-8-9-10

Que-7 :

$ oc create new project area51
$ oc get all


$ oc new-app --name ocxart --image=quay.io/redhattrainning/hello-world-nginx

$ oc get pods
$ oc get svc

//in exam 
$ sh newcert

---

$ openssl genrsa --out private.key
$ openssl req -new -key private.key -out redhat.csr
//fill the info


// 3rd thing
$ openssl x509 -req -in redhat.csr --signkey private.key -days 1000 -out redhat.crt


$ oc get route
$ oc create route edge --service oxcart --hostname oxcart.apps.ocp4.example.com --key private.key --cert redhat.cert

// once execute edge willl be create
$ oc get route


-------


Que 8:

$ oc new-project lerna

// application will be there

$ oc get deployment
$ oc scalele deployment hydra --replicas 5

// or $ oc edit deployment hydra


---
Que 9)

$ oc new-project gru
$ oc new-app ...

$ oc get pods

$ oc edit deployment scala
   // in resource 
   
   
      resources:
	    requests:
		  cpu: '25m'
		limits:
		  cpu: '100m'
		  
		  
or $ oc get deployment scala -o yaml > scala-dep.yaml


$ oc get pods
$ oc describe pod scala 

// verify the changes 

$ oc autoscale deployment scala -h
$ oc autoscale deployment scala --cpu-percent 60 --min 6 --max 40

$ oc get pods   // verify the changes pods should be restarted.

-----

Que 10: configure a secret

$ oc new-project math
$ oc create secret generic magic --from-literal-Decoder_Ring=ASD1244DJFKSJKLA43JKdedfkav

$ oc get secrets
// verify wether secret is created


------ 
# Q. 11-12-13


Que-11: configure environment

$ oc new-app --name ... // may provide applications

$ oc project math
$ oc get deployment
$ oc set env deployment/qed --from secret/magic
$ oc get pods ( // pods will restarts)
$ oc describe pod qed ( // verify env // thing like ring will be there )

--------
Que-12:
// practice
$ oc new-project apples
$ oc new-app oranges --image quay.io/redhattrainning/helloworld-nginix:v1
$ oc expose svc oranges

---

Q.13
$ oc create serviceaccount ex280-sa
$ oc adm policy add-scc-to-user anyuid -z ex280-sa
// cluster role anyuid has been added

// verify
$ oc describe serviceaccounts ex280-sa
$ oc get serviceaccounts ex280-sa -o yaml

// how to change exciding memory. 

 ---
# Q. 14-15-16
 
 $ Helm repo add <repo name> < repo url>
 $ helm install <app name> <repo>
 
 ---
 Q.15
 
 oc project voyager
 oc get all
 
 $ oc set probe deployment.apps/voyager --liveness --open-tcp=8080 --initial-delay-seconds=3 --timeout-seconds=10
 
 ---
 Q.16
 
 $ oc adm must-gather --dest-dir /home/student/clusterData
 $ tar -cvzf /home/student/ex280.clusterID.tar.gz /home/student/ex280-cluster-data
 $ sh <scriptfile> /home/student/ex280-clusterID.tar.gz
 
 
 ----
 
 # Q. 17-18-19

 Q.17 
 $ helm repo list
 $ helm repo add ex280-repo https://helm.ocp4.example.com/charts
 
 $ helm search repo --version
 
 $ heml install etherpad ex280-repo/eherpad
 $ vim values.yaml
 $ helm uninstall etherpad 
 
 ---
 
 Q.18
 
 $ oc get-projects
 $ oc new-project marathon
 $ oc project marathon
 $ oc create deployment.apps/scaling --image=quay.io/redhattrainning/scaling
 
 $ // check for scc
 
 $ oc create cronjob scaling --image=quay.io/redhattrainning/scaling --schedule "05 04 02 * *"
 $ oc create sa ex280-ocpsa
 $ oc adm policy add-scc-to-user anyuid -z ex280-ocpsa
 $ oc edit cronjob scaling
 Spec: 
   successfullJobHistory:13
 wq!
 
 $ oc get pods
 
 ----
 Q.19 : installing operator
 
 $ oc whoami --show-console
 
 
operators >> operatorhub >> fileIntegrity operator >> channel statble >> updates Automatic >> click on install


 ----



wq!

$ cat quata-limits.yml >> project-template.yaml
note: inside the project-template.yml file make sure parameter section should be write at the end.

$ oc create -f project-template.yaml -n openshift-config
$ oc get template -n openshift-config

$ oc edit projects.config.openshift.io -o yaml

spec:
  projectRequestTemplate:
    name: project-request

$ watch oc get pods -n openshift-apiserver  [$ pods restarted\]



=================================================

?? see more about oc get cluster role binding - deepseek



Note : clusterrolebinds me selfprovisioner binding hai. usko remove karna padega. 



# Q.20- 21-22
 -- Need Practice on it.

----

# Further 

1) Do practice of Q.21-22 well..
2) Visualising approach of doing question paper
3) by timer solve Q. Paper in 2 hours.

Lets see have you got confidence 



[[Practice OCP Exam - Considering time and Resolve Doubts]]