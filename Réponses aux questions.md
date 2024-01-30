### Réponses des questions du sprint : 
### Définition : 
- "Kubeapps" est une interface utilisateur web qui permet de gérer et de déployer des applications dans un cluster Kubernetes.

## Le niveau de maturité du produit :
- le projet Kubeapps est relativement mature et a atteint un niveau de stabilité suffisant pour être utilisé en production par de nombreuses organisations. Cependant, on doit  noter que les niveaux de maturité des projets open-source évoluent rapidement et peuvent changer depuis cette date.


## La fréquence de mise à jour et plus généralement le cycle de vie du produit :
- c'est une frèquence assez régulière, pour corriger les erreurs rencontrées au fur et à mesur, la ils sont à la version v2.8.0


## Le niveau de support du produit :
- Il mettent à jour leur bugs d'une manière très courante et assez rigoureuse.

- Cependant, on peut lire ça sur leurs site web <Remarque : cette documentation de l'API est encore à un stade initial et est susceptible d'être modifiée. Avant de vous y connecter, veuillez nous envoyer un problème ou nous contacter via Slack pour en savoir plus sur votre cas d'utilisation et voir comment nous pouvons vous aider>.



## Comment sont stocké les données des services déployé : 
- Dans Kubeapps, les données des services déployés sont stockées dans le cluster Kubernetes lui-même. Kubeapps n'a pas sa propre base de données séparée pour stocker les données des applications ou des services déployés. Au lieu de cela, il utilise les ressources natives de Kubernetes pour stocker les informations relatives aux déploiements, services, réplicasets, pods, secrets, etc.



## Quels sont les méthodes d'authentification : 
# Authentification par jeton de service Kubernetes (Kubernetes Service Account Token) :
- Kubeapps peut être configuré pour utiliser l'authentification basée sur les jetons de service Kubernetes. Cela signifie que les utilisateurs s'authentifient en utilisant les jetons de service Kubernetes existants dans le cluster. Cette méthode d'authentification est souvent utilisée dans les clusters Kubernetes où l'authentification est gérée par la plateforme Kubernetes elle-même. Voici les étapes à suivre : 
### Créer un jeton de service Kubernetes :
<kubectl create serviceaccount kubeapps-user>

### Associer des rôles et des autorisations au jeton de service : 
<kubectl create clusterrolebinding kubeapps-user --clusterrole=cluster-admin --serviceaccount=default:kubeapps-user>

### Récupérer le jeton de service :

<kubectl get secret $(kubectl get serviceaccount kubeapps-user -o jsonpath='{.secrets[0].name}') -o jsonpath='{.data.token}' | base64 --decode >

# Authentification OIDC (OpenID Connect) : 
- Kubeapps prend en charge l'authentification via OpenID Connect, qui est un protocole d'authentification standard basé sur OAuth 2.0. Cela permet aux utilisateurs d'utiliser leurs identifiants OIDC pour se connecter à Kubeapps. L'authentification OIDC nécessite souvent une configuration supplémentaire, notamment la configuration d'un fournisseur OIDC et l'échange des clés de chiffrement. Voici les étapes : 
### Créer un fournisseur OIDC :
- un fournisseur OIDC auprès du fournisseur d'identité, tel que Keycloak, Okta, Auth0, etc

### Configurer les paramètres OIDC dans Kubeapps : 

### Configurer le fournisseur OIDC :

### Tester l'authentification OIDC : 


# Authentification avec un fournisseur d'identité tiers : 
- Kubeapps peut être configuré pour s'intégrer à des fournisseurs d'identité tiers tels que Keycloak, Okta, Auth0, etc. Cela permet aux utilisateurs de s'authentifier à l'aide de leurs identifiants de ces fournisseurs d'identité. Cette méthode d'authentification est utile dans les cas où l'organisation utilise déjà un fournisseur d'identité pour gérer l'authentification et la sécurité.

- Il est important de noter que la configuration de l'authentification dans Kubeapps peut varier en fonction de votre environnement spécifique et des options prises en charge par votre installation de Kubeapps. 

