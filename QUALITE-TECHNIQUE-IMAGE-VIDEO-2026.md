# Qualité technique des modèles génératifs : résolution, bits, HDR, latitude

**Pour décider d'un pipeline niveau cinéma. État au 24 juin 2026. Sources primaires + presse tech vérifiée.**

## La vérité que le marketing cache

Trois confusions à dissiper d'abord, parce que tout le reste en découle :

1. **Résolution native n'est pas résolution affichée.** Presque tous les « 4K » sont des **upscales**. Le modèle génère à 1-2 mégapixels (image) ou 720p-1080p (vidéo), puis agrandit.
2. **Précision n'est pas plage dynamique.** Le « 16-bit float » qu'on voit annoncé est souvent du **faux float** : du 8-bit display-referred mis dans un conteneur float. Plus de précision (anti-banding), zéro stop de dynamique en plus.
3. **Le goulet, c'est le VAE.** Les modèles de diffusion décodent dans un espace **sRGB 8-bit display-referred**. Le décodeur a appris à restituer du sRGB, pas du linéaire scène. Sauver en EXR n'ajoute aucune latitude : ce que le VAE a cramé en blanc est blanc, définitivement.

## Image : résolution native réelle

| Modèle | Native réelle | « 4K » ? | Bits réels |
|---|---|---|---|
| SDXL | 1024² (~1 MP) | upscale | 8-bit sRGB |
| FLUX.2 (dev/pro) | jusqu'à 2048² | au-delà = upscale | 8-bit (float au décodage, extractible en EXR) |
| FLUX 1.1 Ultra | jusqu'à 4 MP | natif jusqu'à 4 MP | 8-bit |
| Qwen-Image, SD 3.5, HiDream, Sana, Z-Image | ~1 MP à 2 MP | upscale au-delà | 8-bit sRGB |

**Règle** : ne jamais générer en 4K direct (ça crashe sous 24 Go et n'ajoute pas de vrai détail). Générer net en natif, puis upscaler.

## Vidéo : le tableau de vérité

| Modèle | Native réelle (vs annoncée) | Bits réels | HDR / log / espace | Export | Verdict |
|---|---|---|---|---|---|
| **Luma Ray3** | 1080p natif ; **EXR 16-bit limité à 540p/720p** ; **4K = upscale** | **10/12/16-bit** | **HDR oui**, ACES2065-1 (AP0) | **EXR 16-bit**, MP4 SDR | ✅ le seul produit fini en 16-bit HDR natif, mais petit format |
| **LTX-2** (ouvert) | base ~720p → **4K = upscale latent two-stage** | **16-bit** (voie HDR) | **HDR latitude grade**, LogC3, scène-linéaire | **EXR 16/32-bit**, ProRes 4444 LogC3 ; MP4 8-bit standard | ✅ 16-bit dans les poids open source (HF `LTX-2.3-22b-IC-LoRA-HDR`) |
| **Kling 3.0** | **4K natif revendiqué**, 60fps | **8-bit** | non, Rec.709 présumé | MP4/MOV/WEBM | 4K le plus crédible, mais 8-bit |
| **Veo 3.1** | ~720p/1080p → **4K = upscale (admis par Google)**, 24fps | **8-bit** | non, Rec.709 | MP4 H.264 + AAC | 8-bit, 4K marketing |
| **Sora 2 / Pro** | ≤1080p natif (pas de 4K) | **8-bit** | non, Rec.709 | MP4 H.264 | 8-bit |
| **Runway Gen-4** | 720p natif → 4K upscale | **conteneur 10-bit, source 8-bit** | non, Rec.709 de fait | MP4 ; **ProRes 4444 .mov** (Pro) | conteneur 10-bit + alpha (compositing), pas de vraie latitude |
| **Wan 2.2** (ouvert) | selon pipeline | 8-bit défaut → **EXR 16/32-bit extractible** | non par défaut ; EXR linéaire possible | MP4 8-bit ; EXR via ComfyUI | extraction = précision, pas HDR |
| **HunyuanVideo** (ouvert) | selon pipeline | 8-bit défaut → **EXR/ProRes 10-bit extractible** | non par défaut | MP4 8-bit ; EXR via SaveVideoHQ | idem (et hors-licence UE, cf. catalogue) |

*Les quatre propriétaires (Veo, Kling, Sora, Runway) ne publient pas de spec officielle de profondeur de bits ; le 8-bit Rec.709 se déduit du conteneur H.264 SDR.*

## Qui ment sur le « 4K natif »

- **Veo 3.1** : upscale, et **Google l'admet** (« upscaling to 1080p and 4K » sur son blog). Ce sont les médias qui titrent « native 4K ».
- **LTX-2** : exagère. Pipeline two-stage à upsampler latent (x1.5/x2 avant le décodage VAE), pas un calcul natif de 8 M pixels par frame.
- **Kling 3.0** : seul à revendiquer sérieusement le 4K natif au stade diffusion. Plausible, mais aucun white paper ni benchmark tiers ne le prouve.

## Le verdict latitude, chiffré et sans complaisance

| Source | Latitude réelle |
|---|---|
| RAW / log caméra | **12-14 stops** récupérables (l'info existe dans le fichier) |
| Sortie IA 8-bit | **~1-2 stops** de manœuvre avant banding visible |

Sur du 8-bit IA : le matching, l'ambiance, la teinte, le regrain sont **faisables et beaux**. Le sauvetage d'exposition, le relight agressif, le pull de hautes lumières sont un **mythe** : l'information n'a jamais été encodée.

## Le protocole pipeline cinéma (ce qui marche vraiment)

### 1. Génération / sortie ComfyUI
- Jamais le `SaveImage` natif (PNG 8-bit). → pack **`ComfyUI-HQ-Image-Save`** (spacepxl), node **`Save EXR`** en **scene-linear Rec.709** (`sRGB_to_linear = true`), pris **avant tout node qui clampe**.
- Le tenseur en sortie de `VAEDecode` est déjà float32 : le format n'est pas le problème, c'est l'espace display-referred du VAE. On récupère la précision float, pas des stops.
- Anti-banding : dithering / micro-bruit avant toute réduction de bits.

### 2. Upscale (le seul vrai ajout d'information)
Ces modèles **hallucinent du détail plausible**, donc ajoutent de la texture réelle qui casse le banding :
- **Topaz Starlight 2.5 Precise** (conçu pour la vidéo IA 720p→4K) : le plus pertinent pour la vidéo.
- **Gigapixel** : fidèle, conservateur (continuité documentaire).
- **SUPIR / Bloom** : plans héros, mais ils inventent (audit visuel obligatoire).

### 3. Étalonnage Resolve / ACES
- Importer en **EXR 16-bit** (ou séquence EXR), timeline **32-bit float**.
- **IDT honnête** : source = sRGB / Rec.709. Ne **jamais** la déclarer log (banding garanti).
- Deband + **regrain en float**, corrections réparties sur plusieurs nodes (pas un node extrême).
- Passer en log/Rec.2020 sert à **matcher** du vrai matériel, ça ne crée pas de latitude.

### 4. Master / finition
- **Séquence EXR 16-bit** ou **ProRes 4444 / DNxHR 444**.
- Réduction 8-bit seulement à la toute fin (le banding apparaît surtout à la réduction de bits, donc dither/regrain en amont, en float).

## Conclusion pour un pipeline d'auteur

Pour une vraie latitude d'étalonnage, viser **Luma Ray3 en 540p/720p EXR ACES** ou **LTX-2 EXR LogC3**, puis upscaler (Topaz). Tout le reste (Veo, Kling, Sora, Runway hors le ProRes de compositing) livre du **8-bit Rec.709 qui plafonne le grade à 1-2 stops**. La qualité cinéma se gagne à l'aval (EXR + 32-bit float + débande + regrain + master 16-bit), jamais en croyant le « 16-bit » ou le « 4K natif » du marketing.

---

*Les specs évoluent vite ; se reporter aux sources officielles avant tout usage à enjeu.*
