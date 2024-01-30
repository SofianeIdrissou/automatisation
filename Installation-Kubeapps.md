## Installer d'abord 'helm':
- l'installation est aussi simple que de télécharger un binaire helm pré-compilé.

## Installation de kubeapps : 
- <helm repo add bitnami https://charts.bitnami.com/bitnami>

## Création d'un nouvel espace de noms (namespace) : 
- <kubectl create namespace kubeapps> 

## utiliser Helm pour installer la charte Kubeapps à partir du référentiel Bitnami : 
- <helm install kubeapps --namespace kubeapps bitnami/kubeapps >

## Créer un identifiant de démonstration avec lequel accéder à Kubeapps et Kubernetes : 

## Créer un compte de service Kubernetes et utiliser un jeton (token) d'API pour s'authentifier auprès du serveur d'API Kubernetes via Kubeapps :

- <kubectl create --namespace default serviceaccount kubeapps-operator>
- <kubectl create clusterrolebinding kubeapps-operator --clusterrole=cluster-admin --serviceaccount=default:kubeapps-operator>
<cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Secret
metadata:
  name: kubeapps-operator-token
  namespace: default
  annotations:
    kubernetes.io/service-account.name: kubeapps-operator
type: kubernetes.io/service-account-token
EOF>

## Accéder à Kubeapps :
- <kubectl port-forward --namespace kubeapps service/kubeapps 8080:80> : avec un forward en lui allouant le port 8080.

## Authentication : 
### Récupération du jeton : 
- [Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($(kubectl get --namespace default secret kubeapps-operator-token -o jsonpath='{.data.token}')))

### Important : 
- Un compte de service est une entité Kubernetes qui représente une identité avec des autorisations spécifiques à l'intérieur du cluster. Il est souvent utilisé pour autoriser des processus ou des applications à accéder aux ressources du cluster.
- Dans ce cas, la commande crée un compte de service nommé "kubeapps-operator" dans le namespace par défaut. Une fois le compte de service créé, il peut être utilisé pour configurer les autorisations et les rôles nécessaires pour le fonctionnement de l'opérateur ou de l'application associée.
- Il est important de noter que la création du compte de service ne lui accorde pas automatiquement des autorisations supplémentaires. Les autorisations doivent être configurées séparément en utilisant des rôles et des liens de rôle (Role Bindings) appropriés pour spécifier les droits d'accès nécessaires au compte de service.

