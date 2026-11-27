<div align="center">

# LineageOS pour Samsung Galaxy A7 (2018)

## Codename : `a7y18lte` · SoC Exynos 7885

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Lint](https://github.com/teremuhamblin/Samsung-a7y18lte/actions/workflows/lint.yml/badge.svg)](https://github.com/teremuhamblin/Samsung-a7y18lte/actions)
[![Release](https://img.shields.io/github/v/release/teremuhamblin/Samsung-a7y18lte)](https://github.com/teremuhamblin/Samsung-a7y18lte/releases)
[![Device](https://img.shields.io/badge/Device-Galaxy%20A7%20(2018)-green)](https://wiki.lineageos.org/devices/)

</div>

---

Ce dépôt contient l'**arbre device LineageOS** (`lineage_a7y18lte/`) du Samsung Galaxy A7 (2018) : makefiles produit, configuration de la carte (`BoardConfig.mk`) et scripts d'extraction des blobs propriétaires.

## Sommaire

- [Fonctionnalités](#fonctionnalités)
- [Modèles compatibles](#modèles-compatibles)
- [Prérequis](#prérequis)
- [Compilation](#compilation)
- [Installation](#installation)
- [Dépannage](#dépannage)
- [Structure du dépôt](#structure-du-dépôt)
- [Contribuer](#contribuer)
- [Licence](#licence)

## ✨ Fonctionnalités

- Arbre device conforme aux standards LineageOS (`AndroidProducts.mk`, `device.mk`, `BoardConfig.mk`)
- Fichier produit `lineage_a7y18lte.mk`
- Scripts `extract-files.sh` et `setup-makefiles.sh` pour les blobs propriétaires
- Support des variantes du Galaxy A7 (2018) équipées de l'Exynos 7885
- Documentation de compilation ([`docs/BUILDING.md`](docs/BUILDING.md))
- CI GitHub Actions (lint Makefile + Markdown)
- Templates d'issues et guide de contribution

## 📱 Modèles compatibles

| Référence | Région |
|-----------|--------|
| SM-A750F | International / Asie |
| SM-A750FN | Europe |
| SM-A750G | Amérique latine |
| SM-A750GN | Asie du Sud-Est |
| SM-A750N | Corée |
| SM-A750C | Chine |

> ⚠️ Vérifiez la référence exacte de votre appareil (Paramètres → À propos du téléphone) avant de flasher une ROM.

## 🧰 Prérequis

- Linux 64 bits (Ubuntu LTS recommandé)
- 16 Go de RAM minimum (+ swap) et 250 Go d'espace disque libre
- Paquets de build Android, `repo`, `git` et `git-lfs`
- Connexion stable (le sync dépasse 100 Go)
- Un appareil sous firmware Samsung (ou ROM) pour extraire les blobs, ou un dépôt `vendor` déjà disponible

## 🚀 Compilation

```bash
# 1. Initialiser l'arbre LineageOS
mkdir -p ~/lineage && cd ~/lineage
repo init -u [https://github.com/LineageOS/android.git](https://github.com/LineageOS/android.git) -b lineage-22.2 --git-lfs
repo sync -c -j"$(nproc)" --no-clone-bundle --no-tags

# 2. Arbre device (ce dépôt)
# Les fichiers sont dans le sous-dossier lineage_a7y18lte/
git clone [https://github.com/teremuhamblin/Samsung-a7y18lte.git](https://github.com/teremuhamblin/Samsung-a7y18lte.git) ~/src/Samsung-a7y18lte
mkdir -p device/samsung
ln -s ~/src/Samsung-a7y18lte/lineage_a7y18lte device/samsung/a7y18lte

# 3. Kernel
git clone [https://github.com/LineageOS/android_kernel_samsung_exynos7885.git](https://github.com/LineageOS/android_kernel_samsung_exynos7885.git) kernel/samsung/exynos7885

# 4. Blobs propriétaires (vendor/samsung/a7y18lte)
cd device/samsung/a7y18lte
./extract-files.sh          # depuis l'appareil (adb) ou un dump de firmware
# ./setup-makefiles.sh      # régénère les makefiles vendor si besoin
cd ~/lineage

# 5. Build
source build/envsetup.sh
lunch lineage_a7y18lte-userdebug
mka bacon
```

La ROM se trouve dans `out/target/product/a7y18lte/`.
Guide détaillé : [docs/BUILDING.md](docs/BUILDING.md).

> ℹ️ `extract-files.sh` appelle en général `setup-makefiles.sh` lui-même. Lancez ce dernier seul uniquement pour régénérer les makefiles.

## 📲 Installation

> ⚠️ Débloquer le bootloader **efface toutes les données** et peut annuler la garantie. Faites une sauvegarde complète avant de commencer.

1. Activez les options développeur, puis **OEM unlock**.
2. Redémarrez en mode Download et confirmez le déblocage du bootloader.
3. Flashez une recovery personnalisée avec Odin ou Heimdall.
4. Dans la recovery, effectuez un factory reset.
5. Flashez le zip de la ROM, puis éventuellement les GApps (MindTheGapps).
6. Redémarrez. Le premier démarrage peut durer plusieurs minutes.

## 🛠️ Dépannage

| Problème | Piste |
|----------|-------|
| `lunch` ne trouve pas la cible | Vérifiez que `device/samsung/a7y18lte/AndroidProducts.mk` existe, puis relancez `source build/envsetup.sh` |
| Fichiers vendor manquants | Relancez `extract-files.sh` et vérifiez `vendor/samsung/a7y18lte` |
| Erreur mémoire pendant le build | Réduisez `-j` et ajoutez du swap |
| Bootloop au premier démarrage | Refaites un factory reset et vérifiez la recovery et la variante |

## 📁 Structure du dépôt

```
.
├── lineage_a7y18lte/
│   ├── Android.bp
│   ├── Android.mk
│   ├── AndroidProducts.mk      # Déclare les produits disponibles
│   ├── BoardConfig.mk          # Configuration matérielle / carte
│   ├── device.mk               # Configuration commune de l'appareil
│   ├── lineage_a7y18lte.mk     # Fichier produit LineageOS
│   ├── extract-files.sh        # Extraction des blobs propriétaires
│   └── setup-makefiles.sh      # Génération des makefiles vendor
├── docs/
│   └── BUILDING.md             # Guide de compilation détaillé
├── .github/
│   ├── CONTRIBUTING.md
│   ├── workflows/lint.yml      # CI : lint Makefile + Markdown
│   └── ISSUE_TEMPLATE/         # Templates bug / feature
├── ROADMAP.md
├── CHANGELOG.md
├── LICENSE                     # Apache 2.0
└── README.md
```

## 🤝 Contribuer

Les contributions sont bienvenues. Consultez [CONTRIBUTING.md](CONTRIBUTING.md) pour commencer.

## 📄 Licence

Projet sous licence **Apache 2.0**, comme LineageOS. Voir [LICENSE](LICENSE).

---
*Projet non affilié à Samsung ni à LineageOS. Vous flashez à vos propres risques.*
