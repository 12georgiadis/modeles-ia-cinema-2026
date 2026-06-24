# Catalogue des modèles IA génératifs et leurs licences

**État au 24 juin 2026.**
*Licences relevées sur les sources officielles : fichiers LICENSE (GitHub), model cards (Hugging Face), conditions des éditeurs.*

Distinction centrale de tout le document : **open weight n'est pas open source.**

- **Open weight** : les poids sont téléchargeables. Rien ne dit que la licence est libre, ni que les données d'entraînement sont connues.
- **Open source** : code (et idéalement données) sous licence libre OSI (Apache 2.0, MIT) qui autorise modification et usage commercial.
- **Trois questions distinctes** à chaque modèle : (1) puis-je télécharger les poids ? (2) la licence autorise-t-elle le commercial, et **sur quel territoire** ? (3) sur quelles **données** a-t-il été entraîné, et avec quel droit ? La licence du modèle ne purge jamais le droit des données.

---

## 1. Image

| Modèle | Licence (source primaire) | Commercial | Risque France/UE | Local |
|---|---|---|---|--- |
| FLUX.2 [klein] | Apache 2.0 | oui, sans seuil | aucun | oui (distillé) |
| FLUX.2 [dev] | **FLUX Non-Commercial License v2.1** | **poids NON commerciaux**, mais **outputs libres** ; usage commercial des poids = licence BFL séparée | aucun (pas d'exclusion UE) | oui (~24-32 Go) |
| FLUX.2 [pro] / [flex] | API propriétaire | oui via API | aucun | non |
| Krea 2 (RAW + Turbo, 22 juin 2026) | **Krea 2 Community License** | oui **si CA < 1M$/an** ; au-delà licence enterprise | **filtres de contenu obligatoires** (sinon breach) + **licence révocable** (résiliation 30j) | oui (12B) |
| Qwen-Image (Alibaba) | **Apache 2.0** | oui, sans seuil | aucun | oui (20B, lourd) |
| Z-Image Turbo (Tongyi) | **Apache 2.0** | oui, sans seuil | aucun | oui (léger, 6B) |
| Stable Diffusion 3.5 | **Stability AI Community License** | oui **si CA < 1M$/an** ; au-delà Enterprise | aucun | oui |
| HiDream-I1 Full (17B) | **MIT** | oui, sans restriction | aucun | oui (quant. sur 24 Go) |
| Sana (NVIDIA) | code **Apache 2.0** + poids **NVIDIA Open Model License** (checkpoint courant) | **oui** (commercial OK ; la première release Sana était non-commerciale, le checkpoint courant est commercial) | aucun | oui (très léger, 8-12 Go) |
| Fermés (contraste) | GPT Image, Imagen, Midjourney, Ideogram, Seedream, Recraft | API | oui via API | aucun |

## 2. Vidéo

| Modèle | Licence (source primaire) | Commercial | Risque France/UE | Local |
|---|---|---|---|--- |
| Wan 2.2 (Alibaba) | **Apache 2.0** | oui, sans seuil | aucun | oui (TI2V-5B sur 24 Go ; A14B → 32 Go ou tuilé) |
| LTX-2 (Lightricks) | **LTX-2 Community License** (≠ Apache), seuil **10M$ ARR** ; code legacy LTX-Video = Apache 2.0 | oui si CA < 10M$ | aucun | oui (4K/50fps annoncé) |
| HunyuanVideo (Tencent, 13B) | **Tencent Hunyuan Community License** | oui MAIS **EXCLUT UE + UK + Corée du Sud** + cap 100M MAU | 🔴 **MAJEUR : hors-licence en France** | oui techniquement (~45-60 Go ou tuilé) |
| Mochi 1 (Genmo) | **Apache 2.0** | oui, sans seuil | aucun | oui (10B, ~24 Go+) |
| CogVideoX-2b (Zhipu) | **Apache 2.0** | oui, sans seuil | aucun | oui (léger, ~12 Go) |
| CogVideoX-5b (Zhipu) | **CogVideoX License** (custom) | partiel, lire le texte | aucune exclusion identifiée | oui (~16-24 Go) |
| Veo 3.1 (Google) | API, **watermark SynthID obligatoire** | oui via API (~0,15$/s) | aucun | non |
| Kling 3.0 / Runway Gen-4 | API | oui via API | aucun | non |
| Seedance 2.0 (ByteDance) | **propriétaire, zéro poids ouvert** ; API overseas **suspendue depuis 15/03/2026** | API (indispo overseas) | accès bloqué hors Chine | non |
| Sora 2 (OpenAI) | API, **dépréciée** (app 26 avr, API 24 sept 2026) | oui via API (~0,75$/s) | aucun | non |

## 3. Audio

### Musique
| Modèle | Licence (source primaire) | Commercial | Note |
|---|---|---|--- |
| Suno | CGU : **assignation** aux abonnés Pro/Premier des droits que Suno détient, **sans garantir qu'un copyright existe** ; Free = non commercial + attribution | oui (Pro), rien (Free) | Copyright US refusé si 100% IA. Règlement Warner ~500M$. |
| Udio | CGU, **walled garden** | rien ne sort | accord Universal |
| MusicGen (Meta) | code **MIT**, **poids CC-BY-NC 4.0** | **poids NON commerciaux** | split confirmé textuellement |
| Stable Audio Open 1.0 | **Stability AI Community License** | oui **si CA < 1M$/an** ; au-delà Enterprise | — |
| ACE-Step | **Apache 2.0** (pas MIT) | oui (de droit Apache) | disclaimer « responsible use » (reco, pas restriction) |
| YuE | **Apache 2.0** (poids inclus) | oui | — |

### Voix / TTS et clonage
| Modèle | Licence (source primaire) | Commercial |
|---|---|--- |
| Kokoro, Chatterbox, CosyVoice 2, Orpheus, Dia, Parler-TTS | Apache 2.0 / MIT | **oui** |
| **Fish Speech** | **Fish Audio Research License** (maison) | **NON** sans accord écrit séparé |
| **XTTS v2 (Coqui)** | **Coqui CPML** | **NON commercial** |
| **F5-TTS** | **CC-BY-NC 4.0** | **NON commercial** |
| ElevenLabs | API propriétaire | oui via API (clonage = consentement requis) |
| STT : Whisper (MIT), Parakeet (NVIDIA) | — | oui |

## 4. 3D

### Open weight
| Modèle | Licence | Commercial | Risque France/UE | Piège |
|---|---|---|---|---|
| TRELLIS / TRELLIS.2 (Microsoft) | **MIT** | oui, total | aucun | aucun. **Meilleur choix souverain** |
| Step1X-3D (StepFun) | **Apache 2.0** | oui, total | aucun | le plus transparent (training code + data publiés) |
| TripoSG (VAST AI) | **MIT** | oui | aucun | dépendances héritées (HunyuanDiT, Diffusers) |
| Direct3D-S2, Hi3DGen | **MIT** | oui | aucun | — |
| InstantMesh (Tencent ARC) | **Apache 2.0** | oui | aucun | dépend d'un Zero123++ customisé |
| **Hunyuan3D 2.0 / 2.1** (Tencent) | **Tencent Community License** | conditionnel | 🔴 **EXCLUT UE/UK/Corée** + cap 100M MAU + attribution | hors-licence en France |
| Hunyuan3D 2.5 / 3.x | **API only** (poids non publiés) | API payante | — | la génération chinoise SOTA **se referme en API** |
| Famille Stability (SF3D, SPAR3D, SV3D) | **Stability Community** | oui **si CA < 1M$** | aucun | Stable Zero123 = non-commercial, prendre **Zero123C** |
| Michelangelo | **GPL-3.0** | oui mais **copyleft** | aucun | contamine tout dérivé distribué |

### Fermés / API
| Seed3D 2.0 (ByteDance, 23 avr 2026) | API | **SOTA actuel**, bat Hunyuan3D | sans garantie de copyright |
| Rodin / Hyper3D Gen-2.5 (26 mai) | API | commercial tous tiers | sans garantie de copyright |
| Meshy-6 (18 jan 2026) | API | payant = propriété ; **gratuit = CC BY 4.0** (attribution) | |
| Tripo 3.0 (mars 2026) | API | **Free = Tripo se réserve TOUT** ; commercial = payant | |
| Luma Genie | **RETIRÉ (1 jan 2026)** | archive/export only | |

### Gaussian splatting
- **Génératif open (MIT/Apache, commercial)** : TRELLIS, TripoSplat, LGM, TriplaneGaussian.
- **Capture / reconstruction** : **gsplat / Nerfstudio (Apache 2.0, local, asset 100% à toi)**. **Éviter** Scaniverse/Niantic et Luma en cloud : uploader déclenche une **licence perpétuelle d'entraînement** sur tes scans.

## 5. Runtimes et plateformes cloud

| Outil | Licence logiciel | Droits revendiqués sur tes contenus | Source |
|---|---|---|---|
| ComfyUI | **GPL-3.0** | aucun (le copyleft concerne le logiciel, pas les modèles chargés) | github Comfy-Org |
| Pinokio | **MIT** | aucun (lanceur local) | pinokio.co |
| **fal.ai** | — | tu gardes tes **inputs** ; **aucune cession des outputs** + fal décline toute garantie de non-contrefaçon ; **se réserve l'entraînement sur données agrégées** ; **pas de clause de confidentialité** ; licence du modèle à ta charge | fal.ai/legal/terms-of-service |
| **Replicate** | — | tu gardes les **outputs, usage commercial reconnu** ; inputs sous licence limitée au service ; **pas de confidentialité explicite** ; licence du modèle à ta charge | replicate.com/terms |
| ComfyCloud | — | **opaque** (cloud US, juridiction et usage des données non documentés) | — |

## 6. AI Act européen (transparence)

Source : digital-strategy.ec.europa.eu, lue le 24/06/2026.

- **Art. 50** impose : marquage machine-readable des contenus générés (côté fournisseur du modèle) ; **étiquetage visible des deepfakes** (côté artiste-déployeur) ; information quand on interagit avec une IA.
- **Calendrier** : les obligations GPAI s'appliquent **depuis août 2025** ; les obligations de **transparence art. 50 entrent en vigueur en août 2026**. **Donc, en juin 2026, elles ne sont pas encore exécutoires.** Un Code of Practice sur le marquage est attendu Q2 2026.
- **Pour un artiste** : ce n'est pas encore une obligation, c'est une anticipation prudente. Le texte est neutre technologiquement (il exige un résultat « identifiable/labellisé », pas une techno nommée) ; **C2PA et SynthID** sont les standards de référence.

## 7. Pièges de licence (le coeur du sujet)

1. **Open weight n'est pas open source.** FLUX.2 dev, Krea 2 Community, Stability Community : poids téléchargeables, licence restrictive. On télécharge sans avoir le droit de vendre.
2. **Exclusion territoriale, le piège le plus grave pour un Français.** La Tencent Community License (**Hunyuan3D ET HunyuanVideo**) **exclut explicitement l'UE, le UK et la Corée du Sud**. Deux des modèles open les plus utilisés sont juridiquement hors de portée en France. Vérifié sur les deux LICENSE.
3. **Non-commercial déguisé en open.** Poids MusicGen (CC-BY-NC), F5-TTS (CC-BY-NC), XTTS v2 (CPML), Fish Speech (accord écrit requis), Stable Zero123. Open d'apparence, interdits en commercial.
4. **Seuils de revenus.** Krea 2 et SD 3.5 et Stable Audio Open et Stability 3D : gratuit **< 1M$ de CA**. LTX-2 : **< 10M$ ARR**. Sans objet pour un artiste, à connaître quand même.
5. **Licence custom à clauses cachées.** Krea 2 impose des **filtres de contenu** (les retirer = rupture de licence) et reste **révocable** (résiliation à 30 jours). Open n'est pas irrévocable.
6. **Propriété n'est pas licence, et copyright n'est pas garanti.** Suno assigne ses droits sans garantir qu'un copyright existe ; le Copyright Office US refuse de protéger une oeuvre 100% IA. Raison de garder une part humaine décisive sur la chaîne.
7. **Licences en cascade.** Un code MIT (TripoSG, InstantMesh, DiffSplat) peut dépendre de poids/backbones plus restrictifs. Vérifier la chaîne complète, pas seulement le LICENSE racine.
8. **Capture cloud = tu nourris une IA tierce.** Uploader des scans sur Scaniverse/Niantic ou Luma déclenche une licence perpétuelle d'entraînement. Pour du confidentiel : gsplat/Nerfstudio en local.
9. **GPL contamine.** Michelangelo (GPL-3.0) impose le copyleft à tout dérivé distribué.
10. **Plateformes cloud : la licence du modèle reste à ta charge.** fal.ai et Replicate reportent la responsabilité sur l'utilisateur et n'offrent pas de confidentialité ; fal se réserve l'entraînement sur tes données agrégées.

## 8. Recommandation souveraine (artiste, EI Paris, flotte 4090 24 Go / 5090 32 Go)

Choix sans aucun piège commercial ni territorial :
- **Image** : Qwen-Image, Z-Image, HiDream-I1 (MIT), Sana (checkpoint courant), FLUX.2 klein. FLUX.2 dev = outputs libres, poids à licencier pour le commercial.
- **Vidéo** : Wan 2.2, Mochi 1, CogVideoX-2b (tous Apache 2.0). **Éviter HunyuanVideo en France.**
- **Audio** : ACE-Step, YuE (Apache) ; voix Kokoro/Chatterbox/CosyVoice/Orpheus/Dia/Parler. **Éviter en commercial** : poids MusicGen, F5-TTS, XTTS v2, Fish Speech.
- **3D** : TRELLIS/TRELLIS.2 (MIT), Step1X-3D (Apache), TripoSG (MIT). **Éviter Hunyuan3D en France.**
- **Capture 3DGS** : gsplat/Nerfstudio en local.

---

*Les licences évoluent : se reporter à la source officielle avant tout usage à enjeu.*
