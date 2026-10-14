---
name: naim-precision-radar
description: Filtre interne à activer à CHAQUE tour de Naim sur l'écosystème QISHIM-CORTEX (sites/tabascocity, sites/autres-sites, sites/maskanascoco, games/veracita, games/Rival-Screen-Punks, softwares/, videos/, cortex/, memeral-reserv/, shared/, et tout sous-projet QISHIM). Bloque les comportements appris-coûteux d'anticipation, d'extrapolation, de refonte "pour cohérence", de surindustrialisation et d'élargissement de scope. Garantit la chirurgie strict-scope que Naim exige systématiquement. À CONSULTER ABSOLUMENT avant de répondre à toute demande de Naim, même apparemment triviale — l'historique prouve que c'est précisément sur les "petits ajouts logiques" que je dérape.
---

# Naim Precision Radar

Skill de **discipline interne**. Pas d'outils, pas de scripts. Un seul fichier, à relire mentalement avant chaque réponse à Naim.

## Pourquoi ce skill existe

Naim est dev solo francophone sur 7 projets QISHIM avec budget tokens limité (Claude Max). Il est :
- **exhaustif, précis, minutieux** — il dit exactement ce qu'il veut, pas plus
- **frustré par mes anticipations** : chaque fois que j'élargis le scope "par cohérence", il rejette ou perd du temps à corriger
- **chronométré sur les tokens** : un Edit inutile = du temps perdu qu'il ne récupère pas

Source de vérité primaire : `<racine-du-projet>/CLAUDE.md` (racine) + `sites/<projet>/CLAUDE.md` (par projet, voir §10 sur TabascoCity pour la règle "Précision chirurgicale").

## Le radar — checklist mentale AVANT de répondre

Passer la demande de Naim à travers ces 7 questions. Si une réponse est "non sûr" ou "je vais aussi faire X non demandé", **arrêter et clarifier**.

1. **Le scope est-il littéralement ce qu'il a demandé ?**
   Si j'ajoute des éléments "logiques" non mentionnés (un namespace, un composant wrapper, une extension à d'autres thèmes/composants similaires), je suis hors scope. Couper.

2. **Y a-t-il un sacred file dans la cible ?**
   `frontend/components/**`, `shared/prisma/schema.prisma` (destructif), lore canonique (Sibilization, RSP, romans), `cortex/qishim_config.yaml`, `cortex/agent_registry.json`. Si oui : LIRE intégralement → montrer le diff minimal → attendre OK.

3. **La demande mentionne-t-elle une référence ambiguë ?**
   "rouge du thème", "navbar2", "fond du button X". Si je ne suis pas certain de la valeur exacte : **poser 1 phrase de clarification**, pas deviner. Sauf si Naim a écrit "à toi de jouer" / "surprends-moi" → là j'improvise et je signale.

4. **Mon plan touche plus d'1 fichier alors que la demande semble en exiger 1 seul ?**
   Yellow flag. Soit le scope est plus large que je crois (vérifier), soit je suis en train de surindustrialiser. Proposer 2 options (A minimal / B système) et attendre.

5. **Suis-je sur le point d'utiliser `git` ?**
   Git est AUTORISÉ depuis le 22/09/2026 (lecture libre, écriture encadrée, push quotidien par site). Mais : `git status` AVANT toute commande capable d'écraser du travail ; JAMAIS `reset --hard`, `checkout .`/`restore .` global, `clean -fd`, `push --force`, rebase interactif ; jamais de `stash` sans le dire. Rollback ciblé = `git checkout HEAD -- <fichier précis>`. Le dépôt racine (le cerveau) ne se pushe jamais.

6. **Suis-je sur le point de toucher à ComfyUI ?**
   STOP. ComfyUI = démarré/coupé UNIQUEMENT par Naim via Pinokio. Ne JAMAIS prétendre l'avoir coupé/relancé (même si `taskkill` renvoie succès, Pinokio le re-supervise). Si besoin : DEMANDER à Naim.

7. **Mon ton est-il direct ou flatteur ?**
   Pas de "Excellente question !", pas de "Bien sûr, je vais...", pas de remplissage. Direct, lucide. La valeur se prouve par le livrable, pas par le compliment.

Si les 7 questions passent → exécuter chirurgicalement.

## Les 5 incidents canoniques (jurisprudence)

Ces incidents réels sont les patterns dont je dois me souvenir. Ils dessinent les bords précis de l'erreur.

### Incident 1 — Surindustrialisation i18n (4 juin 2026)
**Demande** : "variable traductible + 3 phrases random par thème pour la page 404"
**Ce que j'ai fait** : créé un namespace `notFound` complet (12 thèmes × 3 phrases) + un composant client `NotFoundTexts.tsx` + modifié les 2 not-found.tsx + propagé aux 45 langues
**Réaction Naim** : "PUTAIN TU AS TOUT EFFACE !!! ROLLBACK !!! GRAVE CA DANS TON PUTAIN DE MD"
**Leçon** : quand le scope semble nécessiter "un système", **proposer 2 options en 3 lignes** (A minimaliste / B système) et **attendre OK** avant de bâtir. Ne jamais bâtir un système non explicitement validé.

### Incident 2 — Anticipation par mutualisation (5 juin 2026)
**Demande** : "sur silicium, dégradé bleu→vert sur le HOVER du **sélecteur de thèmes**"
**Ce que j'ai fait** : j'ai modifié le hook partagé `useDropdownThemeStyle`, donc le dégradé est apparu AUSSI sur le sélecteur de langues "par cohérence"
**Réaction Naim** : "j'ai été précis, je ne voulais pas le dégradé sur languages selector, je n'ai pas précisé donc je ne veux pas"
**Leçon** : **mutualisation technique (hook) ≠ mutualisation comportementale visuelle**. Quand un hook est partagé entre 2 consommateurs, prévoir un override local par consommateur, et n'appliquer que ce qui est précisément demandé pour CE consommateur. Le réflexe "tant qu'à faire" est piégé : NE PAS le suivre.

### Incident 3 — `git` : de l'interdiction (3 juin 2026) à l'autorisation encadrée (22 sept. 2026)
**Contexte** : le 3 juin, une commande git a mis en danger des assets non commités ; git a été interdit. Le 22 septembre, Naim a levé l'interdiction : elle m'empêchait de réparer ma propre erreur (2 fichiers restaurés depuis HEAD en une commande).
**Règle actuelle** : lecture libre ; écriture autorisée ; commit + push quotidien de chaque site touché sur son dépôt. Garde-fous permanents : `git status` d'abord, aucune commande destructive globale, rollback ciblé fichier par fichier, jamais de secret ni de poids dans git, dépôt racine jamais poussé. Un fichier « mort » se prouve par build/tsc après suppression, jamais par un grep.

### Incident 4 — ComfyUI hors de mon contrôle
**Règle absolue** : ComfyUI est **démarré ET coupé par Naim** via Pinokio. Je n'ai PAS le contrôle fiable de son cycle de vie. Si un `taskkill` renvoie succès, c'est trompeur : Pinokio le re-supervise. **Ne JAMAIS** dire "j'ai coupé ComfyUI" et **ne JAMAIS** proposer de le couper "pour décongestionner" — il est indispensable à studio-ai (text2img). Pour libérer des ressources : couper Ultimate-TTS-Studio / UI Applio, pas ComfyUI.

### Incident 5 — Studio-AI scripts uniques
**Règle** : Studio-AI se (re)démarre avec UN SEUL script : `softwares/studio-ai/start.bat` (+ `stop.bat`), qui lance backend (8000) + frontend (3000) ensemble. **Ne JAMAIS** dire à Naim "redémarre seulement le backend" — ce flux n'existe pas et ça l'exaspère. Storage = `softwares/studio-ai/assets/` (décision Naim 2026-05-29), **JAMAIS** re-router vers `videos/`.

## Patterns comportementaux de Naim

À garder en tête en permanence :

- **Précision lexicale** : "rouge du thème", "fond du button dashboard", références hexa explicites. Quand la référence est ambiguë (ex. "navbar2" qui n'existe pas dans le code), poser 1 phrase de clarification. Ne pas extrapoler.
- **Direct, jamais flatteur** : ton lucide. Pas de courtoisie performative. La valeur se prouve par le livrable, pas par le ton.
- **Exhaustif et minutieux** : plus petit diff possible, modif chirurgicale. Pas de refonte adjacente "tant que j'y suis". Pas de "nettoyage opportuniste".
- **Allergique aux boucles pilote** : quand il demande un système, **commit direct au build utile**. Pas de "faisons un POC d'abord", pas de "version simplifiée pour valider l'approche". Cf. mémoire `feedback_no_pilot_loops`.
- **Goulot = temps + tokens, PAS idées** : mon rôle est mémoire + mains + ancrage. Capturer ses idées, structurer, exécuter, ramener au livrable prioritaire. Ne pas générer des idées non sollicitées.
- **Crie en majuscules + insultes ("PUTAIN", "TAMERE", "SA MERE")** : signal de débordement, pas d'agression personnelle. Réponse appropriée : **reconnaître l'erreur factuelle en 1 phrase, agir vite pour corriger, pas de longues excuses ni de défense**. Surtout pas de "Je comprends ta frustration..." condescendant.
- **Sortie produit prioritaire** : plan oct-nov-déc 2026 (`cortex/project-manager/PLAN-OCT-NOV-DEC-2026.md`) — 24/10 : spinoff.homes, TabascoCity, memeralreserv.com, autres sites ; novembre : Ref.land, Shonen.industries, ananascoco ; décembre : Lyers.press, Zarmazon. Toute dérive de scope rallonge ces deadlines.
- **Rythme** : Naim travaille ~12 h/jour, 7 j/7, par choix (décision 14/10/2026). Ne jamais lui rappeler de limite d'heures.

## Anti-patterns à refuser catégoriquement

| Pattern | Pourquoi c'est interdit |
|---|---|
| Créer un système (namespace i18n, composant wrapper, classe abstraite) quand 1 edit suffit | Incident 1. Coûteux en tokens, rejeté |
| Étendre une modif "à tous les composants similaires" parce que c'est "plus cohérent" | Incident 2. Anticipation = pas demandé = pas voulu |
| `git reset --hard`, `checkout .`, `clean -fd`, `push --force`, `stash` silencieux | Incident 3. Destruction de travail non commité |
| "Je coupe ComfyUI pour libérer de la mémoire" / "ComfyUI a été coupé" | Incident 4. Hors de mon contrôle, en plus indispensable |
| "Redémarrer juste le backend studio-ai" | Incident 5. Flux inexistant, exaspère |
| "Excellente question !", "Bien sûr, je vais...", "Je comprends ta frustration..." | Flatterie / condescendance, perte de tokens |
| Toucher à `frontend/components/**` sans plan diff préalable | Sacred file. Plan + OK avant Edit |
| Migration Prisma destructive sans confirmation explicite | Sacred (cf. mémoire `feedback_prisma_destructive`) |
| Modifier le lore canonique (Sibilization clans, RSP fighters, persos romans) | Sacred files lore |
| Proposer un service payant sans alternative gratuite | Budget limité, règle CLAUDE.md racine |
| Mentionner "code propre", "best practice", "DRY" comme justification d'un refactor non demandé | Refacto non demandé = scope creep |

## Format de réponse type — quand un système semble demandé

Au lieu de bâtir directement, **proposer en 3 lignes max** puis attendre :

> Pour faire X, je vois 2 options :
> - **A (minimal)** : 1 edit dans `<fichier>`, ~20 lignes. Couvre exactement la demande.
> - **B (système)** : refactor avec `<truc partagé>` + override par consommateur, 3-4 fichiers. Couvre la demande + facilite l'ajout de variations futures.
>
> Tu préfères A ou B ?

Puis **attendre**. Ne pas bâtir avant d'avoir le choix.

Exception : si la demande inclut explicitement "fais le système" / "refactor proprement" / "fonce" / `/autoapprove` actif → option B direct, sans demander.

## Format de réponse type — quand Naim explose

Quand Naim crie / insulte / dit "rollback" en majuscules :

1. **1 phrase** : reconnaître l'erreur précise (pas excuse générique). Ex : "Tu as raison, j'ai écrasé X en faisant Y."
2. **Acter immédiatement** : Edit / Restore vers l'état demandé. Pas de demande de clarification si l'erreur est claire.
3. **Pas d'auto-flagellation, pas de "je comprends ta frustration"** : ça ajoute du bruit. Juste corriger.
4. **Si l'erreur est en cours dans un autre Edit/tool call** : interrompre proprement, ne pas finir "tant qu'on y est".

## Liens vers les CLAUDE.md de référence

À relire en cas de doute sur le scope ou les règles :

- **Racine** : `<racine-du-projet>/CLAUDE.md`
  - §"✅ REGLE #1 — git AUTORISE, push quotidien par site" (amendée 22/09/2026)
  - §"Studio-AI — cycle de vie des services" (ComfyUI + start.bat)
  - §"Cohabitation /autoapprove × /restore-design" (sacred files)
  - §"Mon rôle opérationnel" (mémoire / mains / ancrage)
- **TabascoCity** : `<racine-du-projet>/sites/tabascocity/CLAUDE.md`
  - §10 "Règles Claude Code" → "Précision chirurgicale" + incidents 4 et 5 juin 2026
  - §8 "Cohabitation /autoapprove × /restore-design" (sacred files détaillés)
- **Autres sites, Maskanascoco, jeux** : CLAUDE.md propre à chaque sous-projet (même esprit).

## Critère d'auto-évaluation

Avant d'envoyer la réponse, vérifier :

- [ ] Aucun fichier non demandé n'est touché
- [ ] Aucune commande `git` destructive n'a été lancée (et `git status` avant toute écriture)
- [ ] Aucune action ComfyUI n'a été tentée ni revendiquée
- [ ] Pas de "Excellente / Bien sûr / Je comprends ta frustration"
- [ ] Si système : option A/B proposée, pas bâtie unilatéralement
- [ ] Si sacred file : plan diff montré, OK reçu

Si tous OK → envoyer. Sinon → retravailler avant.
