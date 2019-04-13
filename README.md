# Version

- **1.0.0-SNAPSHOT** : initialisation du projet

# Objectif

Configuration kubernetes permettant de déployer l'ensemble des microservices de l'application bank.

- serveur d'autorisation (https://github.com/langston8182/bank-oauth2-authorization-server)
- service utilisateur (https://github.com/langston8182/service-utilisateur)
- service d'interaction (https://github.com/langston8182/service-interaction)

# Deploiment des services

Deployer les service et deploiements
```
kubectl create -f authorization-service.yaml
kubectl create -f authorization-deployment.yaml
kubectl create -f authorization-cm.yaml
kubectl create -f utilisateur-service.yaml
kubectl create -f utilisateur-deployment.yaml
kubectl create -f db-service.yaml
kubectl create -f db-deployment.yaml
kubectl create -f db-secret
kubectl create -f role.yaml
kubectl create -f debug.yaml (pour debugger)
```

Executer la configuration de la base de données comme décrit ici https://github.com/langston8182/service-interaction en se connectant au pod de la base de donnée

```kubectl exec -ti db-deployment-<id> sh```

# Ports d'écoute a l'exterieur du cluster

- interaction-service : 30200
- authorization-service : 30090

# Kubernetes commandes

Prise en compte de la modification d'un fichier de configuration k8s
```kubectl replace -f nom_du_fichier```


Lister les pods, deploiements, services, secrets, configMap tout :
```
kubectl get po
kubectl get deployment
kubectl get svc
kubectl get all
kubectl get secret
kubectl get cm
```

Logs d'un pod :
```kubectl logs pod/authorization-deployment-774c6dfbb7-d26b8```

Suppression d'un deploiment, service :
```
kubectl delete deployment utilisateur-deployment
kubectl delete svc utilisateur-service
```

Supprimer les deploiements, services:
```
kubectl delete deployment --all
bubectl delete svc --all
```

Connexion a un container:
```kubectl exec -ti db-deployment-<id> sh```

Description d'un secret:
```kubectl describe secret db-secret```

Specification d'un secret:
```kubectl get secret db-secret -o yaml```

## Creer un secret
Creation d'un secret pour securiser le mot de passe ROOT pour l'acces a la base de donnees
\
Encrypter le mot de passe en base64
```echo -n 'admin' | base64```
Copier le code dans la configuration db-secret.yaml

# Lister les utilisateurs sur un navigateur web

Entrer l'url http://minikubeIp:30200/utilisateurs

Une redirection est faite sur le serveur d'autorisation oauth2 nous invitant a nous loguer.

# Contributeur

Cyril Marchive (cyril.marchive@gmail.com)
