# 🔐 StaticCrypt Automatic Protection

## Quick Start

### 1. Le secret GitHub est configuré ? ✓

```
GitHub → Settings → Secrets and variables → Actions
STATICCRYPT_PASSWORD = [TON_MOT_DE_PASSE]
```

### 2. Fais tes modifications sur le fichier `index.html`

```bash
# Sur la branche develop
git checkout develop
# ... Edit index.html ...
git add index.html
git commit -m "feat: ta modification"
git push origin develop
```

### 3. ✨ Le workflow se déclenche automatiquement !

```
GitHub Actions → StaticCrypt Protection
- Télécharge index.html depuis main
- Applique la protection avec staticrypt
- Commit automatique sur main
- Déploie sur GitHub Pages
```

### 4. Vérifier le résultat

Attends 2-3 minutes, puis **hard refresh** :
```
https://abs17.github.io/nugital/ 
(Cmd+Shift+R sur Mac / Ctrl+Shift+R sur Windows)
```

---

## Tester localement avant push

### Option 1 : Générer et vérifier

```bash
npm install -g staticrypt

# Générer la version protégée (crée dossier encrypted/)
staticrypt index.html -p "MON_MOT_DE_PASSE" --short

# Ouvrir pour vérifier
open encrypted/index.html

# Si OK, remplacer le fichier original
cp encrypted/index.html index.html
rm -rf encrypted/

# Commit et push
git add index.html
git commit -m "protect: version protégée"
git push origin develop
```

### Option 2 : Utiliser npm scripts

```bash
npm install

# Mode interactif (demande le mot de passe)
npm run protect:interactive

# Mode avec password en dur (modifier package.json d'abord)
npm run protect
```

---

## 🔧 Configuration

### Changer le mot de passe

1. **GitHub Settings** → **Secrets** → Edit `STATICCRYPT_PASSWORD`
2. Entre le nouveau mot de passe
3. Déclenche le workflow :
   ```bash
   git commit --allow-empty -m "Trigger protection update"
   git push origin develop
   ```

### Fichiers importants

- `.github/workflows/staticcrypt.yml` → Workflow automation
- `.staticrypt.json` → Config staticrypt (généré auto)
- `package.json` → Scripts npm pour test local
- `.gitignore` → Ignore les fichiers générés

---

## 📊 Architecturel

```
develop branch (source)
    ↓ git push
GitHub Actions Workflow
    ↓ runs: staticrypt index.html
main branch (protected)
    ↓ GitHub Pages
https://abs17.github.io/nugital/ (🔐 Password Protected)
```

---

## ✅ Checklist de configuration

- [x] Secret `STATICCRYPT_PASSWORD` configuré sur GitHub
- [x] Workflow `.github/workflows/staticcrypt.yml` en place
- [x] GitHub Pages pointant vers branche `main`
- [x] Fichier `index.html` avec contenu stratégie 1000€
- [x] `package.json` avec scripts staticrypt
- [x] `.gitignore` configuré

---

## 🚨 Troubleshooting

### La page n'est pas protégée

**Problème** : Vois le HTML non-protégé directement
**Solution** :
1. Vérifier le secret : GitHub Settings → Secrets (doit être ≠ vide)
2. Vérifier les logs : GitHub → Actions → dernière run
3. Hard refresh : Cmd+Shift+R (vider le cache)
4. Attendre 2-3 min (le déploiement peut être lent)

### Erreur "index.html not found" dans le workflow

**Problème** : Workflow échoue à générer le fichier
**Solution** :
1. Vérifier que `index.html` existe localement
2. Vérifier que `staticrypt` est installé : `npm list -g staticrypt`
3. Check password length : minimum 8 caractères (avec --short flag, pas de limite min)

### Conflit de merge entre develop et main

**Problème** : Git complains about conflicts
**Solution** :
```bash
git fetch origin
git checkout main
git pull origin main
# Puis re-merge develop si nécessaire
```

---

## 📝 Commandes utiles

```bash
# Vérifier la version de staticrypt
npm list -g staticrypt

# Test rapide
echo "<!DOCTYPE html><html><body>Test</body></html>" > test.html
staticrypt test.html -p "test" --short
[Vérifier que encrypted/test.html est créé]

# Voir config staticrypt
cat .staticrypt.json

# Vérifier branche GitHub Pages
git show-branch main develop
```

---

## 📚 Documentation complète

Voir `/memories/repo/staticrypt-automation.md` pour le guide technique complet avec tous les détails.

---

**Dernière mise à jour** : 10 avril 2026
**Workflow** : Automatique à chaque push sur `develop`
**Status** : ✅ Configuration active
