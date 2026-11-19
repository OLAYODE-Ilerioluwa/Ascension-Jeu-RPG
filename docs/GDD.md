# GDD — « Ascension » (nom de travail)

> Nom définitif à choisir : **« Tower of Hell » est à renommer obligatoirement** (marque déposée de Roblox).
> Idées : *Ascension*, *La Tour Oubliée*, *Spire of Ashes*, *Babel Infernale*.

## 1. Concept en une phrase

Un **RPG roguelite tour par tour** où on grimpe une tour de plus en plus dangereuse : chaque étage est un combat, chaque 5e étage un boss, et entre les deux on construit son personnage avec argent, potions, équipement et nouvelles compétences.

**Références vendeuses** : *Slay the Spire* (structure de la tour), *Monster RPG / Persona* (rond de combat, 3 classes), *Vampire Survivors* (courtes sessions).

## 2. Piliers de design

1. **Chaque étage compte** — on perd ses progrès si on meurt (roguelite) → tension permanente.
2. **3 classes, 3 styles** — Guerrier (brut, bouclier), Archer (crit, esquive), Mage (mana, AoE) réellement joués différemment.
3. **Décision à chaque fin d'étage** — boutique OU salle de trésor OU repos : risque vs gain.
4. **Una partie = 30–45 min.** Ni plus (testage lourd), ni moins (sens de la progression).

## 3. Boucle de jeu core

```
Étage N : COMBAT → butin → CHOIX (boutique / trésor / repos) → Étage N+1
                                                              ↓
                        Boss tous les 5 étages → étage 25 = boss final → VICTOIRE
```

- **Combat** : tour par tour classique — Attaque / Attaque magique (mana) / Attaque spéciale (cooldown) / Défense / Potion / Analyse.
- **Progression** : XP → niveau → dégâts et PV augmentent, 1 point de compétence à répartir.
- **Argent** : chaque ennemi lâche de l'or ; sert en boutique (potions, équipment, capacités).
- **Méta-progression (roguelite)** : ce qui est débloqué après la mort (nouvelles capacités, bonus de départ) → rend l'échec utile.

## 4. Combat

- 2 entités à l'écran : héros (gauche) vs ennemi (droite), barres de PV/mana visibles, log remplacé par **bulles de texte flottantes** et animations.
- Dégâts = `attaque × multiplicateur − défense ennemie`, minimum 1. Crit 10 % (x2).
- **Types d'ennemis (à enrichir à 10–12)** :
  | Ennemi | PV | Dégâts | Défense | Or | Spécial |
  |--------|----|--------|---------|----|---------|
  | Goblin | 70 | 20 | 10 | 150 | rapide (2 actions/3 tours) |
  | Squelette | 50 | 15 | 0 | 100 | se relève une fois à 25 % PV |
  | Troll | 80 | 20 | 20 | 200 | régénère 5 PV/tour |
  | Dragon (élite) | 150 | 25 | 10 | 400 | brûlure 3 tours |
  | **Boss** (tous les 5) | 200 | 35 | 15 | 750 | capacité spéciale tous les 3 tours |
- **Finalité** : 25 étages, 5 boss (1 boss unique par palier, avec un pattern propre), boss final à l'étage 25.

## 5. Boutique et potions

- Boutique s'ouvre **tous les 2 étages** entre les combats (bug corrigé vs prototype).
- 3 slots de potions, chacune **limitée en quantité** (achat → consommation réelle).
- Potions : Soin (+30 PV), Puissance (+10 ATQ, 2 tours), Robustesse (+10 DÉF, 2 tours), Mana (+50 %), Antidote, Foulée (fuir l'étage).

## 6. Art direction

- **Pixel art 2D** (16:9), police pixel lisible (ex. *Pixelify Sans*, CC0).
- Personnages/monstres : paquets d'assets libres ou achetés (itch.io asset packs, 5–15 €, *Kenney*, *LimeZu*).
- Palette : fonds sombres de tour, avec une couleur d'accent par étage (plus on monte, plus ça chauffe : bleu → violet → rouge).
- **UI** : cartes de la tour (chemin visualisé), pas de texte de log — feedback visuel + sons.

## 7. Audio

- Musique de combat, musique de boss, ambiance par palier (3 pistes suffisent au lancement).
- Sons : coup, coup magique, défense, prise de dégâts, niveau gagné, achat. Sources : *freesound.org*, *sfxr* pour générer.

## 8. Contenu de lancement (MVP vendable)

| Quantité | Quoi |
|----------|------|
| 3 classes | Guerrier, Archer, Mage |
| 25 étages | dont 5 boss |
| 8 ennemis | dont 4 élites |
| 12 capacités | 4 par classe |
| 6 potions, 6 équipements | boutique |
| 1 méta-progression | déblocage de capacités après la mort |
| Sauvegarde locale | paramètres, runs, stats |
| 1 langage | français (trad EN à ajouter ensuite) |

## 9. Hors scope v1 (matériel pour la suite = DLC / updates)

- Personnages additionnels, défi quotidien, classement en ligne, New Game+, traduction EN, mode coop.

## 10. Choix techniques

- **Moteur : Unity 6 (Personal)** — gratuit en dessous de 200k $ de CA.
- Langage : **C#**.
- Dump de `Tower of hell` → nommer le projet **Ascension** (ou nom retenu) dès le premier commit Unity.
- Vcs : git, avec **Unity LFS** (pas de commit de la Library/).

## 11. Journal des risques

| Risque | Mitigation |
|--------|------------|
| Nom → marque déposée de Roblox | renommer immédiatement |
| Portage mécaniques long | vertical slice d'abord (étages 1–5 jouables) |
| Assets / DA coûteux | packs libres ou achetés, jamais art custom au début |
| Scope creep | tout ce qui n'est pas dans la section 8 est **refusé pour v1** |
| Pénibilité combat (pauses de 5 s) | animations rapides (< 1 s), aucune pause bloquante |
