# Guide de compilation — a7y18lte

## 1. Environnement

```bash
sudo apt install bc bison build-essential ccache curl flex g++-multilib \
  gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev \
  lib32readline-dev lib32z1-dev liblz4-tool libncurses5 \
  libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils \
  lzop pngcrush rsync schedtool squashfs-tools xsltproc zip \
  zlib1g-dev python3
```

## 2. Récupérer les sources

```bash
repo init -u [https://github.com/LineageOS/android.git](https://github.com/LineageOS/android.git) \
  -b lineage-22.2 --git-lfs
repo sync -c -j8
```

## 3. Sources spécifiques à l'appareil

| Composant | Emplacement |
| --- | --- |
| Device tree (ce dépôt, dossier `lineage_a7y18lte/`) | `device/samsung/a7y18lte` |
| Kernel (Exynos 7885) | `kernel/samsung/exynos7885` |
| Blobs propriétaires | `vendor/samsung/a7y18lte` |

## 4. Build

```bash
source build/envsetup.sh
lunch lineage_a7y18lte-userdebug
export USE_CCACHE=1
mka bacon -j$(nproc --all)
```

## 5. Dépannage

- **Erreur `PRODUCT_DEVICE not found`** : vérifiez que le device tree est bien
  dans `device/samsung/a7y18lte`.
- **Bootloop après flash** : reflashez la stock ROM via Odin, puis recommencez
  depuis une recovery propre.
- **Wi-Fi instable** : certains builds non officiels nécessitent un correctif
  « wififix » connu sur les modèles SM-A750F/FN.
