# Modèles génératifs 2026 : qualité technique, résolution réelle, provenance

**État au 24 juin 2026.**

Objectif : distinguer le natif du marketing dans les modèles génératifs (image, vidéo), comprendre la vérité technique (résolution, profondeur de bits, latitude d'étalonnage) et la provenance, et savoir lire un projet de cinéma IA avec les bonnes questions.

---

## 1. Modèles image, paysage actuel

Hiérarchie réelle de juin 2026 (les versions de 2024-2025 type SDXL ne sont plus la référence, voir note de bas de page).

### Fermés / API (qualité et texte en tête)

| Modèle | Sorti | Résolution | Force | Note |
|---|---|---|---|---|
| **Nano Banana Pro** (Gemini 3 Pro Image) | 2026 | jusqu'à 4K | raisonnement, texte, savoir monde réel | le haut de gamme Google |
| **Nano Banana 2** (Gemini 3.1 Flash Image) | 18 juin 2026 | jusqu'à 4K | qualité Pro à vitesse Flash | tout récent |
| **GPT Image 2** (OpenAI) | 2026 | 1K / 2K / **4K natif** (3840×2160) | **texte ~99%**, photoréalisme, édition subject-lock | rendu « propre » mais peu typé |
| **Seedream 4.5** (ByteDance) | déc 2025 | **4K natif (4096²)** | photoréalisme, jusqu'à 14 refs, typographie | le 4K natif le plus solide |
| **Seedream 5.0** (ByteDance) | 2026 | **4K natif (~3840²) en 2-3 s** | vitesse + 4K | le plus rapide en haute-rés |
| **Imagen 4** (Google, Fast/Standard/Ultra) | 2026 | haute-rés | photoréalisme, adhérence au prompt | brique des produits Google |
| **Ideogram 4.0** | 3 juin 2026 | haute-rés | **typographie « belle »** | le roi du texte stylé |
| **Reve 1.0** | 2026 | haute-rés | linework, expressions, style, texte intégré | a pris la tête des blind tests Artificial Analysis |
| **Recraft V4** | 2026 | haute-rés | **design, vecteurs, identité de marque** | l'outil des graphistes |
| **Midjourney V8.1** | défaut 10 juin 2026 | **2K natif (HD, sans upscale)** | esthétique, photoréalisme, Omni Reference | V7 = avr 2025, déjà ancien |

### Ouverts / open weight (cf. catalogue licences pour les pièges)

| Modèle | Licence | Résolution native | Note |
|---|---|---|---|
| **FLUX.2** (dev/klein/pro) | klein Apache 2.0 ; dev non-commercial ; pro API | jusqu'à 2048² | dev = poids non-commerciaux, outputs libres |
| **Krea 2** (RAW + Turbo) | Krea 2 Community (< 1M$, filtres, révocable) | 12B, ~1-2 MP | sorti 22 juin 2026, fait pour le fine-tune / LoRA |
| **Qwen-Image** | Apache 2.0 | ~1-2 MP | libre, solide, lourd (20B) |
| **Z-Image Turbo** | Apache 2.0 | léger (6B) | efficient, faible VRAM |
| **HiDream-I1 Full** | MIT | 17B | libre, lourd |
| **Sana** (NVIDIA) | code Apache + poids NVIDIA Open Model | très léger (8-12 Go) | commercial OK (checkpoint courant) |

*La résolution annoncée « 4K » des modèles ouverts est presque toujours un upscale : ils génèrent net à 1-2 MP, puis agrandissent.*

---

## 2. Modèles vidéo, paysage actuel

| Modèle | Type | Résolution native (vs annoncée) | Bits / HDR | Point clé |
|---|---|---|---|---|
| **Veo 3.1** (Google) | API | ~720p/1080p → **4K = upscale (admis Google)**, 24fps + audio | 8-bit Rec.709 | watermark SynthID obligatoire |
| **Kling 3.0** (Kuaishou) | API | **4K natif revendiqué** (non prouvé), 60fps | 8-bit Rec.709 | le claim 4K le plus crédible |
| **Sora 2 / Pro** (OpenAI) | API | ≤1080p natif | 8-bit | app dépréciée 26 avr, API 24 sept 2026 |
| **Runway Gen-4** | API | 720p natif → 4K upscale | **conteneur ProRes 4444 10-bit + alpha, mais source 8-bit** | bon pour le compositing |
| **Marey** (Moonvalley) | API | cinéma-grade | — | **entraîné 100% sur données licenciées** (Vimeo, B-roll cleared). Le modèle « propre » juridiquement. Édition par calques (avant/milieu/arrière-plan). 14,99$/mois |
| **Luma Ray3** | API | 1080p natif ; **EXR 16-bit limité à 540p/720p** ; 4K = upscale | **16-bit HDR natif, ACES2065-1** | seul produit fini en vrai 16-bit HDR |
| **LTX-2** (Lightricks) | ouvert | base ~720p → 4K upscale latent | **16-bit EXR LogC3** (HF `LTX-2.3-22b-IC-LoRA-HDR`) | 16-bit dans les poids open. HDR de grade, pas HDR10 |
| **Wan 2.2** (Alibaba) | ouvert (Apache 2.0) | TI2V-5B sur 24 Go | 8-bit défaut, EXR extractible | le cheval de trait open, propre côté licence |
| **HunyuanVideo** (Tencent) | ouvert | lourd (13B) | 8-bit défaut, EXR extractible | **licence exclut l'UE** (cf. catalogue) |

---

## 3. La vérité technique (les questions qui démasquent un projet)

### Résolution : natif n'est pas affiché
La quasi-totalité des « 4K » sont des **upscales**. Le modèle calcule 1-2 MP (image) ou 720p-1080p (vidéo), puis agrandit. Vrais 4K natifs : Seedream 4.5/5 (image), Kling 3.0 (vidéo, revendiqué). **Veo 3.1 upscale et Google l'admet.**

### Bits : 8-bit partout, sauf deux exceptions
- **8-bit Rec.709** = quasi tout le monde (mp4 H.264/H.265).
- **Vrai >8-bit** : Luma Ray3 (16-bit HDR ACES) et LTX-2 (16-bit EXR LogC3). C'est tout.
- **Faux 16-bit** : extraire un EXR depuis Wan/Hunyuan donne de la **précision** (anti-banding), pas de la **dynamique**.

### Le goulet, c'est le VAE
Les modèles de diffusion décodent dans un espace **sRGB 8-bit display-referred**. Le décodeur a appris à restituer du sRGB, pas du linéaire scène. Donc sauver en EXR n'ajoute aucune latitude : **ce que le VAE a cramé en blanc est blanc, définitivement**.

### Latitude d'étalonnage : le chiffre qui tranche
- RAW / log caméra : **12-14 stops** récupérables.
- Sortie IA 8-bit : **~1-2 stops** avant que ça casse (banding).
- Faisable : matching, ambiance, teinte, regrain. Mythe : sauvetage d'exposition, relight agressif.

---

## 4. Reconstruire la fidélité après génération

Le principe à retenir : **l'IA inverse le pipeline du film.** Au cinéma classique, la fidélité descend de la caméra vers la livraison ; avec des images génératives, elle doit être **reconstruite après chaque génération** (réparation des artefacts → upscale → conversion HDR → master EXR). C'est multi-phases, pas un bouton magique.

> **Cartel.** Le pipeline de référence qui amène du 8-bit IA dégradé jusqu'à un master cinéma 16-bit HDR a été développé et documenté publiquement par l'équipe du film *The Bends* (Entertainment Technology Center, USC). Leur méthode multi-phases est leur travail : plutôt que de la paraphraser, voir directement les sources — [The Bends, média](https://www.thebendsfilm.com/media) · [VP-Land, 8-bit AI to 16-bit cinema](https://www.vp-land.com/p/8-bit-ai-video-to-16-bit-cinema-quality) · [Topaz Video](https://www.topazlabs.com/topaz-video).

**Côté local, en best practice générale** (outils publics) : sortir de ComfyUI avec le pack `ComfyUI-HQ-Image-Save` (spacepxl), node `Save EXR` en scene-linear pris avant tout node qui clampe ; upscaler avec un modèle qui reconstruit du détail (Topaz, SUPIR) ; étalonner dans Resolve en timeline **32-bit float**, IDT honnête, deband + regrain en float ; master EXR 16-bit ou ProRes 4444 / DNxHR 444, réduction 8-bit seulement à la fin.

**Honnêteté à garder :** un master EXR issu d'une sortie IA reste « référencé 8-bit » en gamut. On gagne la **structure** (résolution, format, précision, latitude de matching), pas la dynamique d'une vraie capture.

---

## 5. Provenance et C2PA (pour juger l'éthique d'un projet)

### L'état du C2PA en 2026
- **Caméras** : Sony (α9 III, α1 II, et le PXW-Z300, première caméra vidéo C2PA), Canon, Leica, Fujifilm, Panasonic ont des modèles compatibles. **Nikon Z6 III : C2PA ajouté puis suspendu** après une faille de signature, certificats révoqués, non rétabli début 2026.
- **Modèles IA** : OpenAI, Adobe Firefly, Google Imagen **embarquent du C2PA** identifiant le contenu généré.
- **Pas universel** : l'adoption est réelle mais partielle, et le C2PA se retire facilement (capture d'écran, ré-encodage).

### Le calendrier réglementaire
**AI Act, art. 50** (marquage des contenus synthétiques, étiquetage des deepfakes) : **exécutoire en août 2026**. Donc en juin 2026, c'est une anticipation prudente, pas encore une obligation. C2PA et SynthID sont les standards de référence pour y répondre.

### Trois familles de modèles selon la provenance (grille utile pour juger un projet)
1. **Clean models** : entraînés sur données licenciées ou cleared (Moonvalley **Marey** = 100% licencié ; Adobe Firefly ; Google ; NVIDIA + Getty). Juridiquement sûrs.
2. **Writs and warrants** : fournisseurs qui assurent la défense juridique.
3. **Wild wild web** : tout le reste (données scrapées, provenance opaque).

---

## 6. Synthèse : quoi mettre dans un pipeline qualité cinéma

- **Image, qualité + texte** : GPT Image 2, Nano Banana Pro, Seedream 4.5/5 (4K natif). **Souverain/local** : Qwen, Z-Image, HiDream, Flux.2.
- **Vidéo, latitude réelle** : Luma Ray3 (540p/720p EXR ACES) ou LTX-2 (EXR LogC3), puis upscale. **Vidéo propre juridiquement** : Marey (licencié). **Souverain** : Wan 2.2 (éviter HunyuanVideo en France).
- **Finition** : reconstruire la fidélité après génération (réparation → upscale → HDR → 16-bit EXR ; méthode de référence *The Bends*, cf. cartel §4), Resolve 32-bit float, IDT honnête, deband + regrain float, master EXR / ProRes 4444.
- **Provenance** : C2PA / Content Credentials, viser les clean models, anticiper l'AI Act d'août 2026.

---

## 7. Grille de lecture d'un projet de cinéma IA

- Quelle **résolution native** réelle, et où se fait l'upscale ?
- Sortie **8-bit ou 16-bit** ? Comment la latitude d'étalonnage est-elle gérée ?
- Pipeline de **reconstruction de fidélité** après génération (le projet a-t-il pensé l'aval, ou croit-il au 4K/16-bit du marketing) ?
- **Provenance** des modèles : clean, writs, ou wild web ? Conscience de l'AI Act et du C2PA ?
- **Part humaine** dans la chaîne (copyright US refusé si 100% IA) : où est la décision d'auteur ?
- Le projet confond-il **précision et plage dynamique**, **open weight et open source**, **natif et upscalé** ?

---

*Note SDXL / SD 3.5 : encore utilisables et bien outillés (ComfyUI, LoRA), mais ce ne sont plus la référence de qualité en 2026. À mentionner comme socle technique mature, pas comme état de l'art.*

*Sources principales : Google DeepMind / blog.google (Nano Banana), OpenAI (GPT Image 2), seed.bytedance.com (Seedream), Ideogram, Midjourney docs, Moonvalley/CineD (Marey), Luma (Ray3), Lightricks (LTX-2), VP-Land + Topaz (The Bends / ETC USC), c2pa.org + presse C2PA, digital-strategy.ec.europa.eu (AI Act). Vérifier en `ffprobe`/`mediainfo` sur un fichier réel avant tout usage à enjeu.*
