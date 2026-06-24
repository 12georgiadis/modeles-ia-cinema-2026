# Le studio à une personne : pipeline hybride live + IA, souverain

**Workflow concret, juin 2026. Tourne sur une flotte GPU grand public (RTX 4090 / 5090) + un iPhone.**

L'idée : filmer un acteur réel, le poser dans un décor génératif, le relighter pour qu'il y appartienne, assembler et restyler, sans studio, sans LED wall, sans cloud propriétaire. Une seule personne tient toute la chaîne. Chaque brique est documentée publiquement et la majorité tourne en local.

> **Cartel.** Cette approche hybride (tracking iPhone + relighting IA + décor en splats + assemblage moteur temps réel + restyle) est portée publiquement par plusieurs équipes, notamment le film *Pathways* de l'Entertainment Technology Center (USC) et le workflow indépendant documenté par World Labs avec Lightcraft et Beeble. Leurs workflows sont leur travail ; ce document n'en est pas la paraphrase, c'est une cartographie des **outils publics** disponibles et de leur mise en œuvre sur une flotte GPU souveraine. Voir leurs sources directes : [World Labs × Lightcraft, étude de cas](https://www.worldlabs.ai/case-studies/lightcraft) · [The Bends / ETC USC](https://www.thebendsfilm.com/media).

---

## Vue d'ensemble

| Phase | Outil | Où ça tourne | Coût |
|---|---|---|---|
| 1. Captation + tracking caméra | **Lightcraft Jetset** (iPhone/iPad) | iPhone | Free, ou Pro 20$/mois (4K + LiDAR), Cine 80$/mois (cinéma) |
| 2. Décor génératif | **Marble** (World Labs) | cloud, export local | 20-35$/mois (export + droits commerciaux dès le tier Pro) |
| 3. Relighting de l'acteur | **Beeble Studio** (SwitchLight 3.0) | **local, RTX 4090/5090 Windows** | 500$/an indie |
| 4. Assemblage / rendu | **Unreal Engine** | local | gratuit |
| 5. Restyle (optionnel) | **Wan VACE** dans ComfyUI | **local, RTX 5090** | gratuit |
| 6. Finition / fidélité | chaîne EXR + DaVinci Resolve | local | gratuit |

Budget récurrent : ~80$/mois d'abonnements + compute local gratuit. Tout le lourd (relight, restyle, rendu) tourne sur tes machines.

---

## Phase 1 — Captation et tracking caméra (iPhone)

**Lightcraft Jetset** transforme l'iPhone en tracker caméra temps réel (ARKit, sans marqueur, 220 g, compatible gimbal DJI RS). On filme l'acteur (fond vert ou décor réel), et l'app enregistre la **trajectoire caméra** synchronisée.

- **Free** : HD, export des scènes vers Blender ou Unreal.
- **Pro (20$/mois)** : 4K, scan LiDAR, marqueurs optiques, déclenchement à distance.
- **Cine (80$/mois)** : GenLock, calibration d'objectif, vraie caméra cinéma, flux **FreeD → Unreal Live Link** pour la donnée caméra en direct.
- Nouveautés : support **Gaussian Splats**, compositing cinématique en direct. Exporte vers **Blender, Unreal, Nuke, Maya, C4D**.

*Sortie : footage de l'acteur + données de tracking caméra (le décor CG bougera exactement comme l'iPhone.)*

## Phase 2 — Décor génératif (Marble)

**Marble (World Labs)** : à partir d'une image (ou plusieurs), génère un **monde 3D en Gaussian splats** explorable, avec profondeur et cohérence spatiale.

- Export **splats** (2 M full ou 500k allégé, `.ply`/`.spz`) ou **mesh** (OBJ/FBX) pour **Unreal / Blender / Houdini**.
- Free : 4 générations/mois. **Standard 20$** : 12 gén, multi-image. **Pro 35$** : 25 gén, expansion de scène, **droits commerciaux**. (Export PLY/GLB = plan payant requis.)
- Alternative souveraine : scanner un vrai lieu en splats (PortalCam, ou photogrammétrie → splat local) quand tu veux du réel plutôt que du génératif.

*Sortie : un décor 3D importable dans Unreal, déjà éclairé et cohérent.*

## Phase 3 — Relighting de l'acteur (Beeble Studio, en local)

C'est la brique clé pour que l'acteur **appartienne** au décor, et elle tourne **sur tes machines Windows**.

**Beeble Studio** (moteur SwitchLight 3.0) tourne en local sur le GPU :
- convertit image/vidéo en **passes PBR complètes** : normales, base color, roughness, metallic, specular, **alpha et depth**, en **EXR 16-bit multi-canaux** ;
- relight avec point/area/sun/video lights et **HDRI** (donc avec l'éclairage du décor Marble) ;
- **4K, jusqu'à 1 h de vidéo, tout en local**, les fichiers ne quittent pas la machine ;
- **500$/an** indie, 3000$/an pro. Windows → tourne sur **BEQUIET (4090) ou TORRENT/NOMAD (5090)**.

*Sortie : l'acteur détouré, relighté pour matcher le décor, en EXR 16-bit avec alpha et depth.*

## Phase 4 — Assemblage et rendu (Unreal Engine)

Dans Unreal :
- importer le **décor splat/mesh** (phase 2) ;
- appliquer la **trajectoire caméra** Jetset (FreeD / Live Link) ;
- composer l'**acteur relighté** (phase 3) à sa profondeur ;
- ajouter les éléments CG (fumée, feu, foule, objets) ;
- rendre la scène (séquence EXR de préférence).

## Phase 5 — Restyle optionnel (Wan VACE, en local)

Pour unifier l'esthétique ou pousser une direction graphique : **Wan VACE dans ComfyUI**, en local sur la **5090**.
- transfert de style d'une image de référence sur toute la séquence, **cohérence temporelle** ;
- **depth / pose / ControlNet** intégrés pour tenir la structure pendant le restyle ;
- LoRA depth + tile pour la précision.
- Alternative API : Runway Gen-4.5 (cohérence forte, mais cloud propriétaire).

## Phase 6 — Finition et fidélité

Principe : l'IA inverse le pipeline, la fidélité se reconstruit après chaque génération (réparation des artefacts → upscale → conversion HDR → master EXR).

> **Cartel.** La méthode de référence pour cette reconstruction (du 8-bit IA dégradé au master 16-bit HDR) a été développée et documentée par le film *The Bends* (ETC, USC). Voir leur workflow directement : [The Bends](https://www.thebendsfilm.com/media) · [VP-Land, 8-bit AI to 16-bit cinema](https://www.vp-land.com/p/8-bit-ai-video-to-16-bit-cinema-quality).

En best practice générale (outils publics) :
- upscaler avec un modèle qui reconstruit du détail (Topaz, SUPIR) ;
- étalonner dans **Resolve** (timeline 32-bit float, IDT honnête, deband + regrain en float) ;
- master **EXR 16-bit** ou **ProRes 4444 / DNxHR 444**.

Rappel de lucidité : une sortie IA reste display-referred (~1-2 stops de latitude). On gagne la structure, la résolution et le matching, pas la dynamique d'un RAW caméra.

---

## Cartographie sur la flotte

| Phase | Machine |
|---|---|
| Captation Jetset | iPhone |
| Décor Marble | cloud → import local |
| **Relight Beeble Studio** | **BEQUIET 4090 ou 5090 Windows** |
| Assemblage Unreal | 5090 (TORRENT) |
| **Restyle Wan VACE / ComfyUI** | **5090 (TORRENT)** |
| Finition / grade | Mac ou 5090 |

## Ce que ce pipeline prouve

Un cinéaste seul peut filmer un acteur réel, le placer dans un monde génératif, l'y intégrer par un relighting physiquement correct, et finir en qualité d'étalonnage, avec un budget d'abonnements de l'ordre de 80$/mois et du calcul local qu'il possède. La dépendance au cloud propriétaire se réduit à la génération de décors (Marble), remplaçable par du scan réel. Le reste est souverain.

---

*Sources : lightcraft.pro/jetset (specs + tiers), worldlabs.ai/Marble (export + pricing), beeble.ai/beeble-studio + CineD (SwitchLight 3.0, on-prem, PBR 16-bit EXR), runcomfy/VACE Wan (video-to-video ComfyUI), Runway Gen-4.5. Outils et prix à revérifier avant tout engagement.*
