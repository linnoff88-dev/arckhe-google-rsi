# Dream-RSI — plano do projeto educativo

Versão 1.0.0 · 19/09/2026 · Projeto `google-rsi` · INEMA

## Proposta

Ensinar como agentes podem melhorar as decisões de pesquisa usando históricos de experimentos como ambientes de replay. O participante deve sair capaz de explicar o ciclo, ler uma comparação experimental e reconhecer onde a evidência termina. O projeto não promete construir uma IA autônoma que melhore indefinidamente.

A entrega inicial é uma landing + guia de projeto. Este plano não escolhe nem implementa um template de curso HTML: se a expansão virar um curso de trilhas/módulos, decidir com o usuário entre formato-curso-v5 e formato-curso-v2 antes de produzi-lo.

## Público e caminhos

Público inicial proposto: adultos interessados em IA e educadores, sem exigência de programação. Desenvolvedores podem seguir uma extensão técnica opcional. A linguagem começa com exemplos cotidianos e apresenta cada termo técnico após a ideia concreta.

- Entrada rápida: guia visual, leitura de uma figura e atividade de compreensão, em cerca de 20–30 minutos.
- Percurso orientado: oito encontros de aproximadamente 30 minutos; 4 horas propostas, não duração de material já gravado.
- Extensão prática: 2–4 horas para um laboratório didático e um relatório; estimativa a validar no piloto.

## Objetivos verificáveis

1. Distinguir solução candidata, agente executor, avaliador e política de exploração.
2. Representar uma rodada como árvore de tentativas e explicar o replay.
3. Separar custo de descoberta, qualidade final e custo total do sistema.
4. Identificar vazamento de futuro e overfitting ao histórico.
5. Comparar estratégias em um cenário não usado para ajustá-las.
6. Comunicar um resultado com baseline, métrica, orçamento e limite de generalização.

## Sequência editorial proposta

| Encontro | Pergunta central | Conteúdo | Atividade | Evidência de aprendizagem |
|---|---|---|---|---|
| 1. Escolher antes de executar | Qual experimento merece o orçamento? | Exploração, exploração de alternativas versus aprofundamento; analogia do mapa | Distribuir 10 fichas entre três hipóteses e justificar | Justificativa distingue valor esperado e qualidade de execução |
| 2. O mapa das tentativas | O que precisa ser registrado? | Nós, relações pai-filho, resultados, falhas e custo; figura 2 | Desenhar uma árvore com sucessos e falhas | Registro permite reconstruir a ordem sem inventar resultados |
| 3. Repetir decisões, não experimentos | O que um replay sabe? | Histórico como ambiente; espaço realizado; observação parcial | Percorrer a mesma árvore com duas ordens | Explica por que ramo ausente não pode ser avaliado |
| 4. A política de exploração | O que pode mudar sem trocar o modelo? | Escolha de ramos, paralelismo, parada; figura 1 | Comparar política fixa e adaptativa sob igual orçamento | Separa agente de política e identifica condição controlada |
| 5. O ciclo recursivo | De onde vem o próximo mundo? | Exploração real, histórico acumulado, seleção e nova rodada | Completar um diagrama e apontar custos | Localiza a recursão na metaexploração, sem confundir com treino de pesos |
| 6. Ler resultados | “Melhor” em qual eixo? | Lasso, KernelBench, matemática; figuras 3 e 4 | Calcular redução de chamadas e comparar baselines | Usa corretamente 42,4% versus 1,74× e distingue runtime de chamadas |
| 7. Desconfiar com método | Quando um replay engana? | Vazamento, generalização, cobertura do histórico, ablação; figura 6 | Auditar uma política que conhece os nós vencedores | Rejeita vazamento e propõe teste em árvores reservadas |
| 8. Defender uma conclusão | O que os dados autorizam dizer? | RSI, AlphaEvolve, possibilidades futuras versus fatos | Apresentar um relatório de uma página | Cada afirmação tem fonte ou rótulo de hipótese |

Cada encontro futuro deve conter: objetivo explícito, explicação de 600–900 palavras, uma figura ou exemplo necessário, exercício, gabarito comentado e referências. Estimativa editorial total: 4.800–7.200 palavras, mais atividades. Não é conteúdo já concluído.

## Laboratório didático proposto

Aplicação estática no navegador, sem login, API paga ou execução de código arbitrário. Deve estar sempre rotulada como **dados sintéticos; demonstração educativa; não reprodução do Dream-RSI**.

### Dados e observabilidade

Cada nó: `id`, `parentId`, `branch`, `attempt`, `valid`, `score`, `cost`, `errorClass`. A interface revela `score` e diagnóstico somente após a visita. Nós futuros não podem ser lidos pela API da política. O usuário pode inspecionar toda a árvore apenas no modo de revisão posterior, separado da execução.

Cenários: melhora rápida que estagna; começo ruim seguido de recuperação; falhas de execução; ramo caro que não compensa; distribuição de teste diferente da de desenvolvimento. O resultado não deve ser programado para a estratégia adaptativa vencer sempre.

### Estratégias e comparação

- Fixa: rodada entre ramos com igual número de tentativas.
- Gulosa: aprofunda o melhor resultado observado.
- Diversificada: reserva uma fração do orçamento para ramos pouco visitados.
- Adaptativa simples: ajusta aprofundamento/parada com base em progresso observado.

Comparar com mesmo orçamento, mesmas árvores, mesma disponibilidade de ações e sementes fixas. Registrar todas as políticas tentadas para evitar selecionar só a melhor retrospectivamente. Manter conjuntos separados de desenvolvimento e teste; parâmetros são congelados antes do teste.

### Métricas e saídas

Melhor score válido, nós consultados, custo sintético acumulado, quantidade de falhas e curva qualidade × orçamento. Exibir custo de replay separadamente do custo sintético das tentativas. Exportar JSON e CSV com configuração, seed, políticas e resultados. A melhoria na simulação não se traduz automaticamente em economia de GPU ou dinheiro.

### Limite do primeiro laboratório

O MVP compara regras escritas por humanos sobre árvores congeladas. Não possui agente de geração de políticas, pesquisa real nem coleta automática de novos mundos. A introdução manual de uma nova árvore pode demonstrar o conceito de expansão, mas não deve ser vendida como implementação do sistema científico completo.

## Arquitetura e entregas

| Etapa | Entrega | Dependência | Critério de aceite | Estado |
|---|---|---|---|---|
| Base | Análise, fontes, cinco figuras, plano, landing e interação de resultados | Fontes originais | Referências verificáveis; figuras locais; mobile e controles funcionais | Implementada nesta entrega |
| Conteúdo | Oito encontros e gabaritos | Revisão pedagógica e escolha de formato se virar curso | Toda atividade mede um objetivo; números têm contexto | Planejada |
| Laboratório | Replay estático e exportação | Esquema de dados e conteúdo dos encontros 2–7 | Sem acesso ao futuro; orçamento respeitado; reprodução por seed | Planejada |
| Piloto | Aplicação com 5–8 participantes | Conteúdo e laboratório prontos | Registrar erros, dúvidas, tempo e revisão necessária | Planejada |
| Extensão | Uma reprodução técnica pequena | Código oficial, licença, orçamento e ambiente avaliados | Comparação controlada e custo completo documentado | Condicional |

Proposta de execução: 1 ciclo de revisão das fontes; 2 ciclos de conteúdo; 2 ciclos de laboratório/validação; 1 ciclo de piloto. São blocos de trabalho, sem datas prometidas. Editor científico, autor pedagógico e desenvolvedor podem ser papéis da mesma pessoa, mas a revisão deve ser explicitamente registrada.

## Avaliação do projeto final

Relatório: pergunta → dados → política → baseline → orçamento → resultado → limite.

Rubrica de 0 a 2 pontos em cinco critérios: definição do problema; comparação justa; leitura das métricas; controle de vazamento/generalização; clareza e rastreabilidade. Meta proposta: 8/10, com obrigatoriedade de não usar informação futura. Resultado negativo bem documentado é válido.

## Riscos e proteções

- Exagero de RSI: explicar que o modelo-base permanece fixo nos experimentos descritos.
- Confundir analogia e método: “história da IA” é enquadramento; as árvores reais pertencem às execuções estudadas.
- Tratar replay como oráculo: expor lacunas de cobertura e necessidade de novas execuções.
- Comparar quantidades incompatíveis: anotar unidades, baseline e modelo ao lado de cada número.
- Desatualização: conferir versão do paper e release do código antes de cada revisão.
- Recursos visuais: preservar créditos e proveniência; não atribuir licença de redistribuição inexistente.
- Dificuldade excessiva: começar sem código; abrir matemática e implementação como aprofundamento.

## Publicação e manutenção

Repo `inematds/google-rsi`; guia em `guia/index.html`; imagens locais em `guia/assets`; documentação em `docs`. GitHub Pages da raiz, URL `/google-rsi/guia/`. Portal: categoria **projeto com guia**, não curso concluído. Derivados de busca e PRO regenerados dos catálogos, sem edição manual.

A cada revisão: registrar data, fontes alteradas e afirmações afetadas em CHANGELOG; atualizar todos os marcadores de versão juntos. A versão atual é 1.0.0.
