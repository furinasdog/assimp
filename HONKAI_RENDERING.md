# HonkaiRendering PMX material adaptation

Based on `ruyo/assimp` commit `06c4e29a3c873648a107de9c1ac50f687b4d50d8`, matching VRM4U's bundled Assimp 6.0.2 revision.

The change in `code/AssetLib/MMD/MMDImporter.cpp` carries existing PMX material fields into `aiMaterial`:

- flag `0x01`: `AI_MATKEY_TWOSIDED` (integer)
- flag `0x10`: `$mat.mmd.edgeEnabled` (integer)
- edge size: `$mat.mmd.edgeSize` (float)
- edge RGBA: `$mat.mmd.edgeColor` (`aiColor4D`)
- supported sphere mode: `$mat.mmd.sphereMode`; texture path: `aiTextureType_REFLECTION`
- custom toon texture path: `$tex.mmd.toonPath` (`aiString`); built-in shared toon indices are not file paths
- toon switch: `$mat.mmd.toonEnabled` (integer); custom index -1 disables toon while missing files and built-in indices retain fallback support

The existing PMX parser, geometry conversion, and other importers are unchanged. The upstream BSD license applies. User models and reference media are not included.

The consuming VRM4U fork documents its Windows build and UE regression checks in `HONKAI_RENDERING.md`. Validation compares imported face counts and material properties against the same models loaded by MMD Tools, outside UE before renderer testing.
