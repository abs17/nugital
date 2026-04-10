# SYSCALL Egypt Master Partner Strategy - Nugital 🚀

Stratégie de lancement SYSCALL Égypte 2026 avec protection StaticCrypt automatisée.

## 🔐 Configuration du Mot de Passe

### 1. **Configurer le secret GitHub**

1. Va sur ton repo GitHub : `https://github.com/abs17/nugital`
2. **Settings** → **Secrets and variables** → **Actions** → **New repository secret**
3. Crée un secret nommé `STATICCRYPT_PASSWORD`
4. Entre le mot de passe que tu veux utiliser

**Exemple :**
```
Name: STATICCRYPT_PASSWORD
Secret: MonMotDePasseSecurise2026
```

### 2. **Le workflow s'exécutera automatiquement**

À chaque push sur `develop` ou `main` :
- ✅ GitHub Actions détecte le changement
- ✅ Installe StaticCrypt
- ✅ Génère `index-protected.html` avec le mot de passe
- ✅ Déploie automatiquement sur `gh-pages`

### 3. **Accès au site protégé**

- **URL de déploiement :** `https://abs17.github.io/nugital/`
- **Mot de passe :** Celui que tu as défini dans `STATICCRYPT_PASSWORD`

---

## 🛠️ Utilisation locale (optionnelle)

### Installer et tester localement :

```bash
# Installation
npm install

# Générer une version protégée (mode interactif - il te demandera le password)
npm run protect:interactive

# Ou avec le password en dur (modifier le script d'abord)
npm run protect
```

Après exécution, tu auras `index-protected.html` prêt à tester localement.

---

## 📝 Workflow détaillé

Le fichier `.github/workflows/staticcrypt.yml` fait :

1. **À chaque push** → Déclenche le job
2. **Checkout** → Récupère le code
3. **Setup Node.js** → Prépare l'environnement
4. **Install StaticCrypt** → Installe l'outil
5. **Generate Protected** → Crée la version chiffrée avec le mot de passe du secret
6. **Deploy to gh-pages** → Publie automatiquement

---

## 🔄 Flux de modification

Maintenant, tu peux **simplement faire** :

```bash
# 1. Faire tes modifications sur index.html
nano index.html

# 2. Commit et push
git add index.html
git commit -m "Mise à jour stratégie 1000€"
git push origin develop

# 3. ✨ GitHub Actions fait le reste automatiquement !
#    - Protection générée
#    - Déployée en ligne
#    - Zéro manipulation manuelle
```

---

## 🚨 Changement du mot de passe

Pour changer le mot de passe à l'avenir :

1. Va sur GitHub → **Settings** → **Secrets and variables** → **Actions**
2. Clique sur `STATICCRYPT_PASSWORD` et modifie la valeur
3. Fais un push vide ou modifie légèrement le fichier
4. Le workflow re-génère avec le nouveau password

```bash
# Push vide pour déclencher le workflow
git commit --allow-empty -m "Mise à jour password StaticCrypt"
git push origin develop
```

---

## 📊 Statut du Workflow

Tu peux voir l'historique des déploiements dans :
`https://github.com/abs17/nugital/actions`

---

## ✨ Avantages de cette setup

- ✅ **1 seul fichier à maintenir** : `index.html` (sans protection)
- ✅ **Automatique** : Protection regénérée à chaque push
- ✅ **Gratuit** : GitHub Actions inclus
- ✅ **Sécurisé** : Password en variable d'environnement (jamais en Git)
- ✅ **Facile** : Pas d'outils locaux obligatoires
- ✅ **Rapide** : Déploiement en ~30 secondes

---

## 💡 Notes

- Le `index.html` original reste **non-protégé** dans le repo
- Seul `index-protected.html` (généré) est déployé en ligne
- Les fichiers générés sont dans `.gitignore` (pas de commit)
- Le mot de passe est **sécurisé** dans les secrets GitHub

Bon, prêt ? 🚀
