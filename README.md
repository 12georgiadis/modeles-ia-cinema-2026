**English** · [Français](README.fr.md)

# Licenses of generative AI models: open weight is not open source

A working repository of licenses for generative models (image, video, audio, 3D) and the tools that serve them, from one simple angle: **when you produce a work with these models, what are you allowed to do with it, and where?**

Status as of June 24, 2026. Each license is checked against its official source (the `LICENSE` file on GitHub, the Hugging Face model card, the publisher's terms).

## The distinction that changes everything

"Open" covers two things that keep getting confused.

- **Open weight**: the weights are downloadable. This says nothing about rights, or about the data.
- **Open source**: code, and ideally data, under a free license (Apache 2.0, MIT) that permits modification and commercial use.

Many models presented as "open" are **open weight under a restrictive custom license**. You can download the weights without having the right to sell the resulting work. Three questions to ask, every time:

1. Can I download the weights?
2. Does the license allow commercial use, **and in which territory**?
3. On **what data** was the model trained, under what right? A model's license never clears the rights to its training data.

## The traps, in order of severity

1. **Territorial exclusion.** The Tencent Community license (**HunyuanVideo** and **Hunyuan3D**) explicitly excludes the European Union, the United Kingdom, and South Korea from its territory of use. Two of the most widely used "open" models in the world are **legally out of reach for an artist based in France**. Verified on both license files.
2. **Non-commercial disguised as open.** MusicGen weights (CC-BY-NC), F5-TTS (CC-BY-NC), XTTS v2 (Coqui CPML), Fish Speech (written agreement required), Stable Zero123: open in appearance, forbidden commercially.
3. **Revenue thresholds.** Krea 2, Stable Diffusion 3.5, Stable Audio Open, the Stability 3D family: free for commercial use under **$1M annual revenue**. LTX-2: under **$10M**. Irrelevant for an individual artist, but worth knowing.
4. **Hidden clauses in custom licenses.** Krea 2 imposes content filters (removing them breaks the license) and remains **revocable** on 30 days' notice. "Open" is not "irrevocable."
5. **Ownership is not a license, and copyright is not guaranteed.** Suno assigns its rights to paying subscribers without guaranteeing that a copyright exists; the US Copyright Office refuses to protect a work that is 100% AI-generated. Two reasons to keep a decisive human share in the chain.
6. **Cascading licenses.** MIT-licensed code can depend on more restrictive weights. Check the whole chain, not just the root license file.
7. **Cloud capture means feeding a third-party AI.** Uploading 3D scans to Scaniverse or Luma triggers a perpetual training license. For anything confidential, reconstruction runs locally (gsplat, Nerfstudio).
8. **Metered platforms pass the license on to the user.** fal.ai and Replicate leave the model's license responsibility with the user and offer no confidentiality clause; fal reserves the right to train on aggregated data.

## The AI Act, in its proper place

The AI Act's transparency obligations (Article 50: labeling synthetic content, tagging deepfakes) **take effect in August 2026**. As of June 2026, they are therefore not yet enforceable. The text is technology-neutral; C2PA and SynthID are the reference standards for complying with it. Anticipating labeling is prudent; presenting it as a current obligation would be false.

## A sovereign base, without traps

To produce in France with no territorial or commercial constraint, the choices that hold up:

- **Image**: Qwen-Image, Z-Image, HiDream-I1 (MIT), Sana, FLUX.2 klein.
- **Video**: Wan 2.2, Mochi 1, CogVideoX-2b (Apache 2.0). HunyuanVideo is avoided.
- **Audio**: ACE-Step, YuE (Apache); voice with Kokoro, Chatterbox, CosyVoice, Orpheus, Dia, Parler. In commercial use, MusicGen, F5-TTS, XTTS v2, and Fish Speech weights are avoided.
- **3D**: TRELLIS and TRELLIS.2 (MIT), Step1X-3D (Apache), TripoSG (MIT). Hunyuan3D is avoided.

## The repository

Four documents, one investigation: what generative models are actually worth in 2026, what you're allowed to do with them, and how to bring them to cinema quality.

- **[CATALOGUE-LICENCES-IA-2026.md](CATALOGUE-LICENCES-IA-2026.md)** — the complete license table (image, video, audio, 3D, runtimes), by modality, with commercial authorization, territorial risk, local feasibility, and primary source. Plus the AI Act and cloud platforms' terms of service.
- **[ETAT-MODELES-GENERATIFS-2026.md](ETAT-MODELES-GENERATIFS-2026.md)** — the state of current models (Nano Banana, GPT Image 2, Seedream, Ideogram, Reve, Midjourney, Flux 2, Krea 2, and on the video side Veo, Kling, Sora, Marey, Luma Ray3, Wan, LTX-2): real native resolution, bit depth, provenance, and a reading grid for a project.
- **[QUALITE-TECHNIQUE-IMAGE-VIDEO-2026.md](QUALITE-TECHNIQUE-IMAGE-VIDEO-2026.md)** — the technical truth: native vs. upscaled, 8-bit vs. 16-bit, the VAE bottleneck, and real grading latitude (the number that settles it: ~1-2 stops on an 8-bit AI output, versus 12-14 on a RAW).
- **[PIPELINE-STUDIO-SOLO-HYBRIDE.md](PIPELINE-STUDIO-SOLO-HYBRIDE.md)** — a concrete workflow: filming a real actor, placing them in a generative set, relighting, compositing and restyling, with public tools and a consumer-grade GPU fleet. The one-person studio.

Note: the four linked documents above remain in French, the language in which the underlying research was conducted.

---

Ismaël Joffroy Chandoutis is an artist and filmmaker. He works cinema with computational instruments and documents his methods in public.

Text licensed under [CC BY-NC-ND 4.0](LICENSE.md).

By [Ismaël Joffroy Chandoutis](https://ismaeljoffroychandoutis.com).
