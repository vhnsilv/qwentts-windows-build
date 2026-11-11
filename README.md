# qwentts-windows-build

Receita reproduzivel para compilar, em um runner Windows do GitHub Actions, o
[qwentts.cpp](https://github.com/ServeurpersoCom/qwentts.cpp) (MIT) nas variantes **CPU** e **Vulkan**.

Este repositorio contem **somente** esta documentacao e o workflow `.github/workflows/build-windows.yml`.
Nao contem codigo do upstream (e clonado no commit fixado), modelos, credenciais nem dados pessoais.

## Como funciona
- Execucao **somente manual** (`workflow_dispatch`), permissao `contents: read`, sem segredos, timeout de 60 min por job, sem retry.
- Upstream no commit `de2ad833e9bd5c06082231d1da637789f7562816`; submodulo ggml conferido em `210138933b22221ced02943b7b6e4308610ab530`.
- Variante Vulkan instala o Vulkan SDK `1.4.363.1` do LunarG apos conferir o SHA-256 `c02932bd9a968b22d404536108adaacac908c081cd6b0113f5bfefc523dd0a6a`.
- Flags: sem `-march=native` (AVX/AVX2/FMA/F16C/BMI2 explicitos, AVX-512 desligado), sem OpenMP, CRT estatico (`/MT`), CUDA desligado.
- Nenhum modelo (GGUF) e baixado.

## Artefato (retencao de 14 dias)
Por variante: `tts-server.exe`, `qwen-tts.exe`, `qwen-codec.exe`, `quantize.exe`, DLLs geradas pelo build (se houver),
`licenses/`, `MANIFEST.json` (commits, versoes, flags, DLLs dependentes, hashes), `SHA256SUMS.txt` e `SOURCE_COMMIT.txt`.

Confira os hashes antes de usar: `Get-FileHash <arquivo> -Algorithm SHA256` e compare com `SHA256SUMS.txt`.
Execute apenas em `127.0.0.1`. Binarios construidos por terceiros: use por sua conta e risco.

## Licencas
O qwentts.cpp, o ggml, o cpp-httplib e o yyjson sao MIT; as licencas vao dentro do artefato.
