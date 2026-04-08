# Wing Fighter — Légion Manager
## Guide complet d'utilisation et de déploiement

---

## 📦 Ce qu'il y a dans ce package

| Fichier | Rôle |
|---|---|
| `index.html` | L'application complète (à renommer depuis legion-manager.html) |
| `manifest.json` | Permet l'installation en PWA sur iPhone/Android |
| `TUTO.md` | Ce guide |

---

## 🚀 Mise en ligne sur GitHub Pages (gratuit, 10 min)

### Étape 1 — Créer un compte GitHub
- Va sur https://github.com
- Clique **Sign up** → compte gratuit

### Étape 2 — Créer un dépôt
- Clique le **+** en haut à droite → **New repository**
- Nom : `wing-fighter-legion` (ou ce que tu veux)
- Coche **Public**
- Coche **Add a README file**
- Clique **Create repository**

### Étape 3 — Uploader les fichiers
- Dans ton dépôt → **Add file** → **Upload files**
- Glisse-dépose : `index.html` et `manifest.json`
- En bas → **Commit changes**

### Étape 4 — Activer GitHub Pages
- Dans ton dépôt → onglet **Settings**
- Menu gauche → **Pages**
- *Source* → **Deploy from a branch**
- Branche : **main** → dossier **/ (root)**
- Clique **Save**

### Étape 5 — Ton URL est prête en ~2 min
```
https://ton-pseudo.github.io/wing-fighter-legion
```

---

## 📱 Installer sur iPhone (mode App)

1. Ouvre l'URL dans **Safari** (pas Chrome)
2. Appuie sur l'icône **Partager** (carré avec flèche ↑)
3. Scroll vers le bas → **"Sur l'écran d'accueil"**
4. Donne un nom → **Ajouter**

L'app apparaît comme une vraie appli sur ton écran d'accueil, plein écran, sans barre Safari.

---

## 🗺 Structure de l'application

### Onglet Accueil
- **Statistiques globales** : nombre de joueurs, total d'events, taux de participation
- **MVP de la légion** : joueur avec le score cumulé le plus élevé
- **Derniers événements** : les 5 plus récents avec score total légion
- **Classement général** : top 5 par score cumulé toutes catégories

### Onglet Joueurs
**Liste des joueurs** avec pour chaque fiche :
- Emoji personnalisé + pseudo + BP (puissance)
- Rang (Chef / Co-Chef / Officier / Élite / Membre)
- Build principal visible en badges (arme MG, drones)
- Score cumulé + nombre d'events joués

**En cliquant sur un joueur** → 4 sous-onglets :
- **Build** : les 6 slots d'équipement (MG, WG, MS, AR, Fighter, Drones)
- **Stats** : saisie des stats d'attaque + aperçu dégâts PvP rapide
- **Historique** : tous les events avec son score, score cumulé total
- **Notes** : champ libre (disponibilités, stratégie, observations)

### Onglet Événements
**Créer un événement** :
- Type : Legion War / Boss Challenge / Tournoi / Legion Hunt
- Nom personnalisable + date
- Saisie directe des scores par joueur
- Classement automatique après saisie

**Historique des events** : tri par date, total légion, taux de participation

### Onglet Calc PvP
Calculateur basé sur les formules officielles de combat PvP (document v0) :

**Stats d'attaque** → peut charger les stats d'un joueur existant  
**Modificateurs globaux** :
- DBDMULT = F(DBD/1000) où DBD = Defense Break − Déf. ennemie
- IRMULT = F(IR/100) où IR = Damage Inc. − Damage Red. ennemie
- FIDMULT = FID/100 si FID ≥ 50, sinon 50/(100+2×(50−FID))

**Résultats** :
- MG : WpCoeff × aMGA × DBDMULT × F((IR+wIR)/100) × FIDMULT
- WG : 0.09 × aWGA × DBDMULT × F((IR+wIR)/100) × FIDMULT  
- MS : 0.225 × aMSA × DBDMULT × F((IR+wIR)/100) × FIDMULT

Coefficients MG : Conqueror = 0.07575 / Destroyer & Thor = 0.078755

---

## 💾 Stockage des données

**Tout est stocké localement** dans le navigateur (localStorage).  
Aucune donnée n'est envoyée sur un serveur.

> ⚠️ Si tu **vides le cache** de ton navigateur, les données sont perdues.  
> Pour les sauvegarder : fais une **capture d'écran** des données importantes  
> ou exporte via le bouton Export (à ajouter dans une future version).

---

## 🔧 Prochaines évolutions possibles

- Export JSON / import des données (sauvegarde externe)
- Calculateur drones, sentinelles, mechs, crit/dodge (formules déjà codées dans le calc PvP standalone)
- Comparateur de builds entre joueurs
- Graphiques d'évolution des scores par event
- Mode "lecture seule" partageable avec les membres
- Intégration base de données (Supabase) pour partage en temps réel

---

## ❓ Problèmes fréquents

**L'app ne s'affiche pas correctement**  
→ Vide le cache du navigateur → recharge

**Mes données ont disparu**  
→ LocalStorage vidé. Pour éviter ça, n'utilise pas la navigation privée.

**L'icône n'apparaît pas sur l'iPhone**  
→ Vérifie que tu es sur Safari (pas Chrome) → recommence la procédure d'ajout

**Je veux ajouter un type d'event**  
→ Ouvre `index.html` dans un éditeur de texte → cherche `const EVENTS=` → ajoute ton event dans le tableau

---

## 📐 Architecture technique (pour aller plus loin)

L'app est un **fichier HTML unique** avec :
- **React 18** chargé via CDN (aucune installation requise)
- **Babel Standalone** pour transpiler le JSX dans le navigateur
- **LocalStorage** pour la persistance des données
- **CSS custom properties** pour le thème
- **PWA** : installable via manifest.json

Pas de build, pas de npm, pas de node_modules.  
Pour modifier : ouvre `index.html` dans n'importe quel éditeur de texte.

---

*Wing Fighter Légion Manager — construit avec Claude*
