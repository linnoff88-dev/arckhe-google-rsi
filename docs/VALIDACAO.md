# Validação — 19/09/2026

## Guia

- Navegador Chromium real via Playwright: larguras 320, 390, 768 e 1440px, sem overflow horizontal da página.
- Cinco imagens locais carregadas e âncoras internas resolvidas.
- Comparador: 550 → 317 (42,4%) e 3.200 → 1.879 (41,3%); números calculados a partir da tabela original.
- Quiz: respostas correta e incorreta apresentam explicação; estado selecionado acessível.
- Tema claro/escuro: alternância e persistência após recarregar confirmadas.
- Console: nenhum erro JavaScript observado.
- Links locais: todos existem; nenhum placeholder do template restante.
- Revisão visual em desktop/mobile e tema claro; corrigida a altura responsiva do hero e o contraste do texto dos botões claros.
- Figuras originais preservadas; SHA-256 e origem em fontes/imagens.json.
- Capa social renderizada como composição tipográfica do projeto com a figura original creditada; não é imagem científica nova.

## Catálogo

Worktrees isoladas preservam alterações existentes no portal e nas buscas. Fonte do portal regenerada com `npm run gen:data`; traduções EN/ES geradas pelo script existente. Os nove testes do portal e TypeScript (`tsc --noEmit --incremental false`) passaram.

## Limites

O vídeo não foi retranscrito; foi analisado o resumo integral fornecido e confrontado com fontes primárias. Os anexos no clipboard remoto não concluíram a leitura. Não houve execução do código científico Dream-RSI, que não é o propósito desta entrega.

## Publicação confirmada

- GitHub Pages: execução `35444406211` concluída com sucesso; guia, cinco figuras, capa, análise e plano responderam HTTP 200.
- Portal: commit `eb343dc`, push em `NeiMaldaner/portal`.
- Buscas: commit `fd6c290`, push em `inematds/inemabuscas` pelo remoto correto `inemabuscas` (o `origin` desse clone aponta para outro repo).
- PRO: commit `747329f`, push em `inematds/inemapro`.
- Base gerada: 18.277 itens, com 277 cursos, 235 projetos, 157 páginas wiki, 2.457 resumos, 12.312 clips, 1.393 lives, 6 itens Telegram e 1.440 prompts. Nenhum ID anterior removido; um novo ID adicionado.
- Classificação confirmada para `projeto:google-rsi-guia`; 100% dos cursos/projetos classificados. O normalizador inclui o segmento `guia` no ID.
- Os 41 testes do content-base passaram. Somados aos 9 do portal: 50 testes, além das verificações de navegador e TypeScript.
- Vercel não foi consultado: publicação dos catálogos considerada concluída pelos pushes.
