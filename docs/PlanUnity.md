# Plan de migration — du prototype JavaFX au jeu Unity vendable

## Vue d'ensemble

On **garde tout le travail de design** (mécaniques, équilibrage, classes) déjà présent dans
`src/main/java/sio/realisationslam/` et on le **réimplémente en C# dans Unity**. Le code
JavaFX servira de référence (il marche, il décrit exactement les règles), mais ne sera
pas porté tel quel : Unity impose une architecture différente (composants, scène, prefabs).

On garde ce dépôt comme **archive du prototype** (branche `prototype-javafx`) et on
ouvre un **nouveau dépôt git** pour le projet Unity.

## Étape 0 — Mise en place (1 journée)

- [x] Renommer le jeu : **Ascension** (dossier `Ascension-Jeu-RPG`). Ne plus utiliser l'ancien nom dans aucune publication.
- [ ] Installer **Unity Hub** puis **Unity 6 LTS** (module *Windows Build Support*).
- [ ] Nouveau projet Unity · template **2D (Built-in RP ou URP 2D)**.
- [ ] Git init + `.gitignore` Unity (celui de github/gitignore) + `Git LFS` pour `Assets/**`.
- [ ] Créer la page itch.io en **private** dès le premier build jouable (feedback boucle).

## Étape 1 — Vertical slice (2–4 semaines)

Objectif : **étages 1 à 5, avec un boss** et une mécanique de fin d'étage, jouables de A à Z
avec des assets gratuits. Pas une ligne de plus avant que ça soit fun.

### Architecture des scripts (équivalence avec le prototype Java)

| Java (prototype)             | C# (Unity)                                   | Rôle |
|------------------------------|----------------------------------------------|------|
| `Hero`, `Ennemi`, `Boss`     | `CharacterStats` (ScriptableObject ou classe) | PV, ATQ, DÉF, mana, XP |
| `Attaque`, `AttaqueMagique`, `AttaqueSpeciale` | `ISkill` + classes `SkillDamage`, `SkillBuff` | skills en **ScriptableObjects** (réglables dans l'éditeur, pas de code) |
| `Defense`, `DefensePassive`, `DefenseActive` | `StatusEffect` (buffs/débuffs à durée)      | le système à refaire proprement (le prototype a des bugs ici) |
| `Potion`, `Boutique`         | `ItemData` (SO), `ShopManager`               | inventaire data-driven |
| `Tour`, `HelloController`    | `RunManager` + `FloorManager` + `CombatState` | machine à états : Exploration → Combat → Récompense → Choix |
| FXML / labels                | UI Toolkit ou Canvas + Prefabs               | l'UI est visuelle, plus du texte brut |

### Ordre de travail

1. Scène de combat : 2 sprites + barres de vie + un bouton « Attaquer » qui fait des dégâts.
2. Machine à états du tour (`CombatState`) : tourJoueur → animations → tourEnnemi → retour.
3. Implémenter les 3 classes du héros avec leurs 3 attaques (`ISkill` → ScriptableObjects).
4. Statuts : bouclier, buff ATQ/DÉF à durée (ça remplace tout le code « toursDefense/toursPotion » buggé).
5. 4 ennemis + 1 boss selon le GDD §4.
6. Transition fin d'étage : choix boutique / trésor / repos.
7. Build WebGl → page itch.io privée → retour joueuses/amies.

**Critère de succès** : tu meurs de rire en le jouant, et tu y retourves tout seul le lendemain.

## Étape 2 — Contenu complet v1 (1–3 mois)

- [ ] 25 étages avec 5 bosses distincts (patterns différents).
- [ ] 8 ennemis avec un comportement propre à chacun.
- [ ] 12 capacités, 6 potions, 6 équipements (tous en ScriptableObject, réglable sans code).
- [ ] Méta-progression après la mort.
- [ ] Sauvegarde locale (`JsonUtility`, PAS `BinaryFormatter`).
- [ ] Musiques + sons (libres au début).
- [ ] Playtests avec 5–10 personnes + itérations.

## Étape 3 — Vente (qui coûte de l'argent)

### itch.io d'abord

- Build WebGL + Windows (7zip). Prix de lancement test : **5 €**.
- Devlogs + screenshots réguliers pour créer une audience.

### Steam ensuite (recommandé, ~100 $ de frais unique)

- Compte Steamworks → Tax interview → page du jeu.
- Page : 5 screens + 1 trailer (60 s max) — c'est la page qui vend, pas le jeu.
- Période d'attente obligatoire de **2 semaines** entre la soumission de page et la sortie.
- **Wishlist** : objectif réaliste avant sortie, ~1 000 wishlists minimum pour être « visible » (mécanique Steam).
- Prix final selon qualité perçue : **8–12 €** (un jeu > 1 h et fini à 8 € vend très mal ; un jeu bien poli à 10 € passe).
- Sortie en « Coming soon » 1–2 mois avant le jour J pour récolter les wishlists.

## Coût total estimé

| Poste | Coût |
|-------|------|
| Unity Personal | 0 € |
| Packs d'assets (art, audio) | 20–80 € |
| Steam Direct fee | ~100 $ |
| Site / trailer (CapCut, gratuit) | 0 € |
| **Total** | **~150–200 €** |

## Règles anti-échec (à relire chaque semaine)

1. **Une seule mécanique à la fois** : on ne passe à la suite que quand l'étape est jouable.
2. **Aucun art custom avant la fin de l'étape 2** : ce sont les assets achetés qui porteront le style.
3. Builds WebGL → itch.io **chaque vendredi**, même moche : la boucle feedback est ce qui sauve les projets.
4. Si une feature n'est pas dans le GDD §8, elle attend la v1.1.
