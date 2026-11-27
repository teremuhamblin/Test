# LineageOS — Samsung Galaxy A7 2018 (a7y18lte)

Produit **LineageOS** pour le Samsung Galaxy A7 (2018), codename `a7y18lte`.
Ce dépôt contient le fichier de produit (`lineage_a7y18lte.mk`) nécessaire à la
compilation d'une ROM LineageOS officielle ou personnalisée pour cet appareil.

## Modèles compatibles

Le codename `a7y18lte` regroupe toutes les variantes du Galaxy A7 (2018),
basées sur le SoC **Exynos 7 Octa 7885** :

| Modèle | Référence | Région |
|--------|-----------|--------|
| Galaxy A7 (2018) | SM-A750F | International / Asie |
| Galaxy A7 (2018) | SM-A750FN | Europe |
| Galaxy A7 (2018) | SM-A750G | Amérique latine |
| Galaxy A7 (2018) | SM-A750GN | Asie du Sud-Est |
| Galaxy A7 (2018) | SM-A750N | Corée |
| Galaxy A7 (2018) | SM-A750C | Chine |

> ⚠️ Vérifiez toujours la référence exacte de votre appareil
> (Paramètres → À propos du téléphone) avant de flasher une ROM.

## Prérequis

- Ubuntu 20.04+ (ou WSL2) avec 16 Go de RAM minimum et 300 Go d'espace disque
- `repo`, `git`, `android-sdk-build-tools` et les paquets de build LineageOS
- Déblocage du bootloader OEM sur l'appareil (OEM unlock dans les options développeur)

## Compilation

```bash
# 1. Initialiser l'arbre LineageOS
mkdir ~/lineage && cd ~/lineage
repo init -u https://github.com/LineageOS/android.git -b lineage-22.2 --git-lfs
repo sync

# 2. Cloner les sources de l'appareil
git clone https://github.com/LineageOS/android_device_samsung_a7y18lte.git device/samsung/a7y18lte
git clone https://github.com/LineageOS/android_kernel_samsung_exynos7885.git kernel/samsung/exynos7885
git clone https://github.com/LineageOS/proprietary_vendor_samsung.git vendor/samsung

# 3. Copier ce dépôt (fichier produit)
git clone https://github.com/<votre-compte>/lineage_a7y18lte.git vendor/lineage/product/a7y18lte

# 4. Préparer l'environnement et lancer le build
source build/envsetup.sh
lunch lineage_a7y18lte-userdebug
mka bacon
```

La ROM compilée se trouve dans `out/target/product/a7y18lte/`.

## Installation

1. Débloquez le bootloader (OEM unlock).
2. Flashez une recovery personnalisée (TWRP) via Odin ou Heimdall.
3. Redémarrez en recovery et effacez les données (factory reset).
4. Flashez le zip de la ROM puis éventuellement les GApps (MindTheGapps).
5. Redémarrez — le premier boot peut prendre plusieurs minutes.

## Structure du dépôt

```
.
├── lineage_a7y18lte/
│   └── lineage_a7y18lte.mk   # Fichier produit LineageOS
├── docs/
│   └── BUILDING.md           # Guide de compilation détaillé
├── .github/workflows/
│   └── lint.yml              # Vérification automatique (lint Makefile)
├── LICENSE                   # Apache 2.0
└── README.md
```

## Licence

Ce projet est sous licence **Apache 2.0**, comme le projet LineageOS.
Voir [LICENSE](LICENSE).
