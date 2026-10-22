# ArchiveAgent

A personal project by [Kalan Peace](https://kalanpeace.com/), built on a small budget. Site: [archiveagent.si](https://archiveagent.si/) (invite only).

**Theia** is the first model from ArchiveAgent. It reads a fashion photograph and names the **house**, the **season** and the **year**. It is Kimi K2.6 (Moonshot AI) fine-tuned with LoRA on Tinker (Thinking Machines). It is not a foundation model trained from scratch.

## Results

All photos are fresh: Theia never trained on any test photo, show or product.

| Test | Size | Theia | Claude Opus 5.5 | GPT-6.1 Sol | Gemini 3.1 Pro |
| --- | --- | --- | --- | --- | --- |
| Runway: house, season **and** year all right | 287 photos, 41 shows | **56.4%** | 28.6% | 26.1% | 23.0% |
| Runway: house only | 287 photos | **87.8%** | 74.2% | 66.2% | 49.5% |
| Product photos: name the house | 150 cases | **100%** | 98.7% | 95.3% | 55.3% |
| Blind runway: all three | 50 photos | **56.0%** | 22.0% | 20.0% | 26.0% |
| Exact product name | 75 products | 50.7% | **58.7%** | 52.0% | not completed |

On the runway test Kimi K3 scored 44.9% on all three, and Kimi K2.6, the model Theia started from, scored 12.2%.

**How it was tested.** Every model got the same photos and the same instructions through OpenRouter. Theia ran on Tinker. A decline or an answer that ran out of room counts as wrong. One run per system, scored by me. Labels are model-made and trusted by the owner. The scoring rules were written down, dated and hashed before any run.

## Where Theia does not win

- **Exact product names.** Claude Opus 5.5 named 58.7% of the 75 products and Theia 50.7%. With 75 products, a gap that size could be luck.
- **Part of Theia's skill on made-up model names is memory.** On the hardest slice (23 products with short invented names), 17 come from product lines that also appear in training photos. Whole product lines have not been held out yet.
- **Houses it never trained on.** Theia knows 14 houses well. On photos from houses it never saw, it names the house 57% of the time, against 90% on the others.
- **Studio product photos.** Season and year are mostly guesses.
- **It always answers,** even when unsure. It also reports how sure it is: keep its most confident 75% of answers and the house is right 98.6% of the time.
- **Scoring mistakes I found and fixed:** the scorer ignored pre-fall, a few product lines leaked between training and test, and "Louis Vuitton x Nike" was marked as the wrong house.
- It is a specialist, not a chat assistant.

## How it was made

- Start: Kimi K2.6, an open model from Moonshot AI.
- Training: 5,025 examples (3,000 runway, 2,025 product), one pass, 80 minutes on Tinker. **$18.35** to train, once.
- Cost to run: about $0.0014 per photo, measured from the runs.

## Hyperion

Hyperion is a chat agent. You give it up to six photos of one piece, it calls Theia to read them, searches shops for where to buy it, and shows every step with its time. In a small test of 17 requests there were no confident wrong answers; median time was about 11.5 seconds and cost about 2.4 cents per request. That is a small sample, not a guarantee. It identifies a piece; it cannot tell you whether it is real.

## Earlier test: four image models on one desktop GPU

Before Theia I tested four open image models on 86,874 runway photos on one RTX 5060. With the show hidden, SigLIP 2 found the right house 74.4% of the time, PE-Core-L 67.9%, CLIP ViT-B/16 52.2% and DINOv3-L 48.7% (random guessing: 8.7%). These models find similar photos; their scores are not comparable with the Theia tests.

## Data

Both datasets are gated on Hugging Face. They contain protocols, labels, raw answers and code; no photos are published here.

- [theia-bench](https://huggingface.co/datasets/kalanpeace/theia-bench): the test side of the Theia release.
- [local-image-models-bench](https://huggingface.co/datasets/kalanpeace/local-image-models-bench): the four-model test.

## Notes

ArchiveAgent and Theia are not affiliated with or endorsed by Moonshot AI or Thinking Machines. Kimi K2.6 is released under a modified MIT licence.

Contact: kalanpeace@gmail.com
