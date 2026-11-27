# Guide de contribution

Merci de votre intérêt pour ce projet ! Voici comment contribuer efficacement.

## Signaler un bug

Ouvrez une issue avec le template **Bug report** et incluez :

- Modèle exact de l'appareil (ex. SM-A750FN)
- Version de LineageOS et date du build
- Étapes pour reproduire le problème
- Logs (`logcat`, `dmesg`) si pertinents

## Proposer une modification

1. Forkez le dépôt et créez une branche : `git checkout -b feature/ma-fonctionnalite`
2. Commitez avec des messages clairs au format
   [Conventional Commits](https://www.conventionalcommits.org/) :
   `feat: ajout du support de la variante SM-A750C`
3. Poussez la branche et ouvrez une Pull Request.
4. Assurez-vous que la CI (lint) passe.

## Conventions

- Respectez la licence Apache 2.0 : chaque nouveau fichier doit inclure
  l'en-tête de licence LineageOS.
- Indentation : 4 espaces dans les fichiers `.mk`.
- Un commit = une modification logique.
