[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Lint](https://github.com/teremuhamblin/Test/actions/workflows/lint.yml/badge.svg)](../../actions)
[![Release](https://img.shields.io/github/v/release/teremuhamblin/Test)](../../releases)
[![Device](https://img.shields.io/badge/Device-Galaxy%20A7%20%282018%29-green)](https://wiki.lineageos.org/devices/)

# LineageOS — Samsung Galaxy A7 2018 (`a7y18lte`)

Dépôt professionnel du fichier produit **LineageOS** pour le Samsung Galaxy A7
(2018), codename `a7y18lte`. Il contient le fichier `lineage_a7y18lte.mk`
nécessaire à la compilation d'une ROM LineageOS pour cet appareil.

## ✨ Fonctionnalités

- Fichier produit conforme aux standards LineageOS (Apache 2.0)
- Support de toutes les variantes du Galaxy A7 (2018) — Exynos 7885
- Documentation de compilation complète (`docs/BUILDING.md`)
- CI GitHub Actions (lint Makefile + Markdown)
- Templates d'issues et guide de contribution

## 📱 Modèles compatibles

| Modèle | Référence | Région |
|--------|-----------|--------|
| Galaxy A7 (2018) | SM-A750F | International / Asie |
| Galaxy A7 (2018) | SM-A750FN | Europe |
| Galaxy A7 (2018) | SM-A750G | Amérique latine |
| Galaxy A7 (2018) | SM-A750GN | Asie du Sud-Est |
| Galaxy A7 (2018) | SM-A750N | Corée |
| Galaxy A7 (2018) | SM-A750C | Chine |

> ⚠️ Vérifiez la référence exacte de votre appareil
> (Paramètres → À propos du téléphone) avant de flasher une ROM.

## 🚀 Démarrage rapide

### Compilation

```bash
# 1. Initialiser l'arbre LineageOS
mkdir ~/lineage && cd ~/lineage
repo init -u https://github.com/LineageOS/android.git -b lineage-22.2 --git-lfs
repo sync -c -j8

# 2. Sources de l'appareil
git clone https://github.com/LineageOS/android_device_samsung_a7y18lte.git device/samsung/a7y18lte
git clone https://github.com/LineageOS/android_kernel_samsung_exynos7885.git kernel/samsung/exynos7885
git clone https://github.com/LineageOS/proprietary_vendor_samsung.git vendor/samsung

# 3. Ce dépôt (fichier produit)
git clone https://github.com/teremuhamblin/Test.git vendor/lineage/product/a7y18lte

# 4. Build
source build/envsetup.sh
lunch lineage_a7y18lte-userdebug
mka bacon
```

La ROM compilée se trouve dans `out/target/product/a7y18lte/`.
Guide détaillé : [docs/BUILDING.md](docs/BUILDING.md).

### Installation sur l'appareil

1. Débloquez le bootloader (OEM unlock dans les options développeur).
2. Flashez une recovery personnalisée (TWRP) via Odin ou Heimdall.
3. Effacez les données (factory reset) depuis la recovery.
4. Flashez le zip de la ROM, puis éventuellement les GApps (MindTheGapps).
5. Redémarrez — le premier boot peut prendre plusieurs minutes.

## 📁 Structure du dépôt

```
.
├── lineage_a7y18lte/
│   └── lineage_a7y18lte.mk   # Fichier produit LineageOS
├── docs/
│   └── BUILDING.md           # Guide de compilation détaillé
├── .github/
│   ├── workflows/lint.yml    # CI : lint Makefile + Markdown
│   └── ISSUE_TEMPLATE/       # Templates bug / feature
├── CONTRIBUTING.md           # Guide de contribution
├── CHANGELOG.md              # Historique des versions
├── LICENSE                   # Apache 2.0
└── README.md
```

## 🤝 Contribuer

Les contributions sont bienvenues ! Consultez
[CONTRIBUTING.md](CONTRIBUTING.md) pour commencer.

## 📄 Licence

Ce projet est sous licence **Apache 2.0**, comme le projet LineageOS.
Voir [LICENSE](LICENSE).
