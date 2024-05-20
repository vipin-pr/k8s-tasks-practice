Username: Martin

Build user information for martin in the default kubeconfig file: User = martin , client-key = /root/martin.key and client-certificate = /root/martin.crt (Ensure don't embed within the kubeconfig file)

Create a new context called 'developer' in the default kubeconfig file with 'user = martin' and 'cluster = kubernetes'

----------------------------------------------------------------------------------------

developer-role

'developer-role', should have all(*) permissions for services in development namespace

'developer-role', should have all permissions(*) for persistentvolumeclaims in development namespace

'developer-role', should have all(*) permissions for pods in development namespace

----------------------------------------------------------------------------------------

developer-rolebinding

create rolebinding = developer-rolebinding, role= 'developer-role', namespace = development

rolebinding = developer-rolebinding associated with user = 'martin'

----------------------------------------------------------------------------------------

kube-cofig

set context 'developer' with user = 'martin' and cluster = 'kubernetes' as the current context.

----------------------------------------------------------------------------------------

jekyll-node-service

Service 'jekyll' uses targetPort: '4000', namespace: 'development'

Service 'jekyll' uses Port: '8080', namespace: 'development'

Service 'jekyll' uses NodePort: '30097', namespace: 'development'

----------------------------------------------------------------------------------------

jekyll (pod)

pod: 'jekyll' has an initContainer, name: 'copy-jekyll-site', image: 'kodekloud/jekyll'

initContainer: 'copy-jekyll-site', command: [ "jekyll", "new", "/site" ] (command to run: jekyll new /site)

pod: 'jekyll', initContainer: 'copy-jekyll-site', mountPath = '/site'

pod: 'jekyll', initContainer: 'copy-jekyll-site', volume name = 'site'

pod: 'jekyll', container: 'jekyll', volume name = 'site'

pod: 'jekyll', container: 'jekyll', mountPath = '/site'

pod: 'jekyll', container: 'jekyll', image = 'kodekloud/jekyll-serve'

pod: 'jekyll', uses volume called 'site' with pvc = 'jekyll-site'

pod: 'jekyll' uses label 'run=jekyll'

----------------------------------------------------------------------------------------

jekyll-pvc

Storage Request: 1Gi

Access modes: ReadWriteMany

pvc name = jekyll-site, namespace = development

'jekyll-site' PVC should be bound to the PersistentVolume called 'jekyll-site'.

----------------------------------------------------------------------------------------

jekyll-pv

jekyll-site pv is already created. Inspect it before you create the pvc.