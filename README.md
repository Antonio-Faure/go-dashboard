# Go Dashboard

Single-page GitHub Pages app (un seul fichier `index.html`, sans dépendance sauf les fonts Google) pour suivre le solde d'abonnement OpenCode Go sur un cycle de facturation de 30 jours.

## Utilisation

Ouvrir `index.html` dans un navigateur, ou servir le dossier via GitHub Pages. Régler les 3 valeurs avec les barillets (molette, tactile, clic ou flèches du clavier) puis cliquer sur **Calculer** :

1. **Jours restants** dans le cycle (0–30)
2. **Heures restantes** dans le cycle (0–23, comme une horloge — le total ne peut jamais dépasser 720 h : à 30 jours les heures retombent à 0)
3. **Consommation mensuelle** en % (0–100) — vrai principe microscope : un seul curseur partagé, molette rapide (±1 point par cran) + molette fine (±0,1 point par cran), la valeur combinée s'affiche en dessous

## Calcul

- Temps écoulé % = `((30 − jours) × 24 + (24 − heures)) / 720 × 100`
- Solde = consommation % − temps écoulé %
  - Solde positif → **avance** (on consomme plus vite que le temps ne passe)
  - Solde négatif → **retard** (on consomme plus lentement, rythme prudent)
- Équilibre théorique = temps restant (`720 × (1 − consommation / 100)` converti en jours + heures) pour lequel la consommation correspondrait exactement au temps écoulé.

## Code couleur

- 🩵 Cyan : solde ≤ −10 (largement en retard — énorme marge, on peut consommer à toute berzingue)
- 🟢 Vert : solde entre −10 et 0 (en retard ou à l'équilibre — rythme sûr)
- 🟠 Orange : solde entre 0 et 10 points (en avance, à surveiller)
- 🔴 Rouge : solde entre 10 et 20 points (largement en avance, réduire l'usage)
- 🚨 Rouge vif : solde > 20 points (critique, le quota sera épuisé bien avant la fin du cycle)

## Design

Le CSS (thème sombre/clair, cartes, responsive breakpoint 560px, fonts Crimson Pro + DM Sans) est répliqué de `formules-physique-chimie.html`.
