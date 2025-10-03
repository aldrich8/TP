# TP
TP docker github 

# Déploiement CI/CD d'une page HTML via GitHub Actions

## 1. Objectif du projet
Ce repository contient une **page HTML simple** déployée automatiquement sur un serveur via **GitHub Actions**.  
Le but est de mettre en place un **pipeline CI/CD** permettant de :  
- Déployer automatiquement l’application sur un serveur SSH.  
- Vérifier la bonne intégration et le transfert des fichiers via un workflow GitHub.

---

## 2. Contenu du repository
- `index.html` : fichier HTML de l’application à déployer.  
- `.github/workflows/deploy.yml` : workflow GitHub Actions pour le déploiement.

---

## 3. Prérequis
Pour exécuter le workflow et le déploiement :  
- Un serveur Linux accessible en SSH.  
- Apache2 installé sur le serveur.  
- Un utilisateur non-root avec clé SSH configurée.  
- Les secrets GitHub suivants configurés dans `Settings → Secrets` :  
  - `SSH_HOST` : adresse IP ou domaine du serveur  
  - `SSH_USER` : utilisateur pour la connexion SSH  
  - `SSH_PORT` : port SSH  
  - `SSH_PRIVATE_KEY` : clé privée pour la connexion SSH

---

## 4. Déploiement automatique
Le workflow `deploy.yml` fait les opérations suivantes :  
1. Checkout du repository GitHub.  
2. Connexion SSH sécurisée au serveur cible.  
3. Copie du fichier `index.html` dans `/var/www/html/`.  
4. Vérification de la présence du fichier sur le serveur.  

---

## 5. Contraintes
- Le serveur doit être accessible depuis Internet (IP publique ou tunnel).  
- La connexion SSH doit se faire **sans mot de passe**, uniquement avec la clé privée.  
- Le workflow ne fonctionne que sur la branche `main`.

---

## 6. Problèmes rencontrés et solutions
| Problème | Solution |
|----------|---------|
| Le workflow ne se déclenchait pas | Déplacement correct de `deploy.yml` dans `.github/workflows/` et push sur la branche main |
| SSH non accessible depuis GitHub Actions | Utilisation d’une machine publique ou tunnel Ngrok/Tailscale |
| Fichier index.html mal placé | Mise à la racine du repo pour que le workflow le copie correctement |

---

## 7. Résultat
- Après `git push`, le workflow GitHub Actions se déclenche.  
- Le fichier `index.html` est copié automatiquement sur le serveur.  
- La page est accessible via `http://IP_DU_SERVEUR`.  
- Le processus est entièrement automatisé via CI/CD.
