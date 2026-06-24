# Licences des modèles IA génératifs : open weight n'est pas open source

Un répertoire de travail des licences des modèles génératifs (image, vidéo, audio, 3D) et des outils qui les servent, du point de vue d'une question simple : **quand on produit une œuvre avec ces modèles, qu'a-t-on le droit d'en faire, et où ?**

État au 24 juin 2026. Chaque licence est relevée sur sa source officielle (fichier `LICENSE` sur GitHub, model card Hugging Face, conditions de l'éditeur).

## La distinction qui change tout

« Open » recouvre deux choses qu'on confond sans cesse.

- **Open weight** : les poids sont téléchargeables. Cela ne dit rien des droits, ni des données.
- **Open source** : code, et idéalement données, sous licence libre (Apache 2.0, MIT) qui autorise la modification et le commercial.

Beaucoup de modèles présentés comme « open » sont **open weight sous licence custom restrictive**. On peut télécharger les poids sans avoir le droit de vendre l'œuvre produite. Trois questions à poser, à chaque fois :

1. Puis-je télécharger les poids ?
2. La licence autorise-t-elle le commercial, **et sur quel territoire** ?
3. Sur **quelles données** le modèle a-t-il été entraîné, avec quel droit ? La licence du modèle ne purge jamais le droit des données.

## Les pièges, par ordre de gravité

1. **Exclusion territoriale.** La licence Tencent Community (**HunyuanVideo** et **Hunyuan3D**) exclut explicitement l'Union Européenne, le Royaume-Uni et la Corée du Sud de son territoire d'usage. Deux des modèles « open » les plus utilisés au monde sont **juridiquement hors de portée pour un artiste établi en France**. Vérifié sur les deux fichiers de licence.
2. **Non-commercial déguisé en open.** Poids MusicGen (CC-BY-NC), F5-TTS (CC-BY-NC), XTTS v2 (Coqui CPML), Fish Speech (accord écrit requis), Stable Zero123 : open d'apparence, interdits en commercial.
3. **Seuils de chiffre d'affaires.** Krea 2, Stable Diffusion 3.5, Stable Audio Open, famille Stability 3D : gratuit en commercial sous **1 M$ de CA annuel**. LTX-2 : sous **10 M$**. Sans objet pour un artiste, à connaître quand même.
4. **Clauses cachées des licences custom.** Krea 2 impose des filtres de contenu (les retirer rompt la licence) et reste **révocable** à 30 jours. « Open » n'est pas « irrévocable ».
5. **Propriété n'est pas licence, et le copyright n'est pas garanti.** Suno assigne ses droits aux abonnés payants sans garantir qu'un copyright existe ; le Copyright Office américain refuse de protéger une œuvre 100 % générée par IA. Deux raisons de garder une part humaine décisive dans la chaîne.
6. **Licences en cascade.** Un code MIT peut dépendre de poids plus restrictifs. On vérifie la chaîne entière, pas seulement le fichier de licence racine.
7. **Capture en cloud, c'est nourrir une IA tierce.** Téléverser des scans 3D sur Scaniverse ou Luma déclenche une licence perpétuelle d'entraînement. Pour du confidentiel, la reconstruction tourne en local (gsplat, Nerfstudio).
8. **Les plateformes au compteur reportent la licence sur l'utilisateur.** fal.ai et Replicate laissent la responsabilité de la licence du modèle à l'utilisateur et n'offrent pas de clause de confidentialité ; fal se réserve l'entraînement sur les données agrégées.

## L'AI Act, à sa juste place

Les obligations de transparence de l'AI Act (article 50 : marquage des contenus synthétiques, étiquetage des deepfakes) **entrent en vigueur en août 2026**. En juin 2026, elles ne sont donc pas encore exécutoires. Le texte est neutre technologiquement ; C2PA et SynthID sont les standards de référence pour y répondre. Anticiper le marquage est prudent, le présenter comme une obligation actuelle serait faux.

## Une base souveraine, sans piège

Pour produire en France sans contrainte territoriale ni commerciale, les choix propres :

- **Image** : Qwen-Image, Z-Image, HiDream-I1 (MIT), Sana, FLUX.2 klein.
- **Vidéo** : Wan 2.2, Mochi 1, CogVideoX-2b (Apache 2.0). On évite HunyuanVideo.
- **Audio** : ACE-Step, YuE (Apache) ; voix Kokoro, Chatterbox, CosyVoice, Orpheus, Dia, Parler. On évite, en commercial, les poids MusicGen, F5-TTS, XTTS v2, Fish Speech.
- **3D** : TRELLIS et TRELLIS.2 (MIT), Step1X-3D (Apache), TripoSG (MIT). On évite Hunyuan3D.

## Le dépôt

Quatre documents, une même enquête : ce que valent vraiment les modèles génératifs en 2026, ce qu'on a le droit d'en faire, et comment les amener à une qualité cinéma.

- **[CATALOGUE-LICENCES-IA-2026.md](CATALOGUE-LICENCES-IA-2026.md)** — le tableau complet des licences (image, vidéo, audio, 3D, runtimes), par modalité, avec autorisation commerciale, risque territorial, faisabilité locale et source primaire. Plus l'AI Act et les CGU des plateformes cloud.
- **[ETAT-MODELES-GENERATIFS-2026.md](ETAT-MODELES-GENERATIFS-2026.md)** — l'état des modèles actuels (Nano Banana, GPT Image 2, Seedream, Ideogram, Reve, Midjourney, Flux 2, Krea 2, et côté vidéo Veo, Kling, Sora, Marey, Luma Ray3, Wan, LTX-2) : résolution native réelle, profondeur de bits, provenance, et une grille de lecture d'un projet.
- **[QUALITE-TECHNIQUE-IMAGE-VIDEO-2026.md](QUALITE-TECHNIQUE-IMAGE-VIDEO-2026.md)** — la vérité technique : natif vs upscale, 8-bit vs 16-bit, le goulet du VAE, et la latitude d'étalonnage réelle (le chiffre qui tranche : ~1-2 stops sur une sortie IA 8-bit, contre 12-14 sur un RAW).
- **[PIPELINE-STUDIO-SOLO-HYBRIDE.md](PIPELINE-STUDIO-SOLO-HYBRIDE.md)** — un workflow concret : filmer un acteur réel, le poser dans un décor génératif, le relighter, assembler et restyler, avec des outils publics et une flotte GPU grand public. Le studio à une personne.

---

Ismaël Joffroy Chandoutis est artiste et cinéaste. Il travaille le cinéma avec des instruments computationnels et documente ses méthodes en public.

Texte sous licence [CC BY-NC-ND 4.0](LICENSE.md).
