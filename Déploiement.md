## Déployer des applications : (Wordpress dans notre cas) : 
- Une fois que le tableau de bord Kubeapps est opérationnel, on peut commencer à déployer des applications dans notre cluster.
- Utiliser le bouton Déployer ou cliquer sur la page Catalogue dans le tableau de bord pour sélectionner une application dans la liste des packages dans l'un des référentiels configurés ( notre cas c'est une application wordpress).
- Kubeapps demande le nom de la version et les valeurs de l'application. Le formulaire est rempli par les valeurs ( YAML ), qu'on peut voir dans l'onglet à coté.
- Cliquer sur le bouton Déployer pour déployer l'application. On peut suivre le nouveau déploiement directement depuis le navigateur. L'état est affiché en haut, y compris le access URLet tout secret inclus avec l'application. On peut également consulter les ressources individuelles plus bas dans la page. Il indique également le nombre de pods prêts. Si on  passe notre curseur sur le status , on peut voir les charges de travail et le nombre de pods prêts et totaux qu'elles contiennent.

## Remarque : 
- Si on souhaite désinstaller/supprimer nore application, on peut le faire en cliquant sur le bouton Supprimer.