# Quran Semantic Search Model

On-device, meaning-based ayah search for the [Quran - Furqan app](https://furqan.app): users can describe what they're looking for ("ayahs talking about the sea", "patience in hardship", "دو سمندر") in any of the app's languages and find matching ayahs offline.

## Download

Each version is published as a **release asset** (not committed to the repo):

```
https://github.com/app-furqan/quran-semantic-search/releases/download/v1/semantic_search.tar.xz
```

`semantic_search.tar.xz` (xz -6) extracts to `semantic_search/`:

| File | Contents |
|---|---|
| `model.onnx` | [EmbeddingGemma 2](https://huggingface.co/google/embeddinggemma-2) 4-bit ONNX, text-only, vocabulary pruned to the tokens of the Quran and all 115 app translations (identical embeddings to the full model for that text) |
| `tokenizer.json` | Matching pruned BPE tokenizer (Hugging Face format) |
| `vectors.bin` | int8 embeddings of all 6,236 ayahs (Arabic + English), 512 dims, scale 127 |
| `refs.bin` | uint16 little-endian `(surah, ayah)` pairs in row order |
| `manifest.json` | Dimensions and query prompt |

Built with `scripts/build_semantic_search_model.py` in the app repository.

## License

The model is EmbeddingGemma 2 by Google, licensed under the Apache License 2.0 (see [LICENSE](LICENSE)). It was modified by removing unused vocabulary and the image/audio/video inputs.
