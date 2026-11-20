# Análise do material — Dream-RSI

Consulta: 19/09/2026. Base: resumo integral fornecido pelo usuário, site original, artigo v1 e repositório dos autores. O vídeo não foi retranscrito nesta análise. Os caminhos de clipboard enviados dependem de uma montagem remota que não entregou o conteúdo durante a leitura; o texto colado na conversa foi a base editorial disponível.

## Diagnóstico

A síntese captura bem a importância de melhorar decisões de exploração. Sua melhor contribuição pedagógica é separar “executar bem” de “escolher bem o próximo experimento”. Precisa, porém, delimitar o significado de história, de simulação, de custo e de autoaperfeiçoamento. O trabalho não é um simulador de toda a evolução científica nem uma demonstração de retreinamento autônomo do modelo-base.

Referência identificada: Tong Zheng et al., **Dream-RSI: Recursive Self-Improvement through Evolving Worlds**, arXiv:2609.14858v1, 14/09/2026. Afiliações incluem Google, Google DeepMind, University of Maryland e University of Virginia. É um preprint; a existência do texto não equivale a validação independente ou revisão por pares.

## Matriz de afirmações

| Material recebido | Verificação / ajuste editorial |
|---|---|
| Melhorar a escolha dos experimentos é central | Confirmado. A política programa a exploração; o agente de código fica fixo. |
| A história das pesquisas vira um mundo | Especificar: árvores estruturadas de execuções e seus resultados, não toda a história da ciência. |
| Árvore tecnológica com Hinton, GPUs, LLMs, AlphaGo e AlphaFold | Analogia introdutória. Não corresponde ao conjunto experimental do Dream-RSI; evitar narrativa linear de causalidade. |
| Milhares de candidatos com zero execuções reais | Refere-se à avaliação por replay sem refazer o agente de descoberta e o avaliador. Não mede custo total zero; geração de políticas e histórico têm custos. |
| Só a melhor estratégia vai para o mundo real | Política selecionada pela avaliação histórica é redeployada. Não existe garantia de que será a melhor no futuro. |
| O histórico cresce recursivamente | Confirmado: exploração produz árvores, replay seleciona política, nova exploração amplia o conjunto. |
| A IA melhora a si mesma | Delimitar a metaexploração. Não há atualização dos pesos do agente de código nessa comparação. |
| Política fixa não aprende | Refere-se ao controle da exploração; o agente ainda observa feedback no trabalho. Evitar afirmar que toda política fixa ignora todo o contexto. |
| Gemini RSI / Gemini 3.7 Flash vence | O nome do método é Dream-RSI. Gemini-3.7-Flash consta no artigo e no site. A média Lasso de 2.350,6 ms é a menor da tabela, não uma vitória universal. |
| Métrica menor é sempre melhor | Errado como generalização. Lasso usa runtime menor; KernelBench mostra desempenho maior; matemática alterna a direção conforme tarefa. |
| Menos compute quando avança, mais quando fica difícil | Comportamento observado na análise ConvDiv; não transformar em uma lei invariável do método. |
| Orientar demais piora | Ablação de orientação semântica específica; não conclusão geral contra instruções ou memória. |
| AlphaEvolve, Borg e milhões de dólares | A fonte DeepMind confirma recuperação média de 0,7% dos recursos de compute. “Milhões” não é uma cifra verificada no material consultado. |
| Várias IAs formando uma cadeia de melhoria | Cenário prospectivo útil para discussão. Não é o sistema completo que este paper demonstrou. |
| Trabalho fundacional | Interpretação editorial, não resultado mensurável. Apresentar como possível relevância para infraestrutura de pesquisa. |
| Treinar com corte histórico e redescobrir avanços | Experimento mental atribuído a Hassabis no resumo; não validado como experimento deste trabalho. Não usar citação literal atribuída sem fonte direta. |

## Resultados que podem entrar no material

Lasso: com Gemini-3.1-Pro, exploração fixa usa 550 chamadas e termina com runtime médio de 3.587,1 ms; Dream-RSI usa 317 e obtém 2.931,0 ms. Redução de chamadas calculada: `(550-317)/550 = 42,36%`. A razão é `550/317 = 1,735×`; redução percentual e fator não são a mesma forma de medida.

Com Gemini-3.7-Flash: 3.200 → 1.879 chamadas, redução de 41,28%; runtime 2.516,7 → 2.350,6 ms. O agregado reúne seis datasets. Algumas colunas individuais favorecem a política fixa: não afirmar superioridade em cada dataset.

O fator aproximado de 162× vem de `51.200/317`, comparando SimpleTES com outro modelo. Distinguir essa comparação de sistema completo da comparação controlada contra Recursive Fixed Exploration.

KernelBench: VGG16 e LayerNorm atingem desempenho comparável com 2,43× e 1,79× menos gerações; ConvDiv e ConvMax obtêm 2,09× e 1,44× mais desempenho com orçamento comparável. São quatro tarefas, não todo tipo de kernel GPU.

Matemática: soma–diferença 1,145427 (maior melhor); autocorrelação 1,456375 (menor melhor); empacotamento de círculos 2,635983 (maior melhor). O SimpleTES tem autocorrelação melhor (1,453675), usando 51.200 gerações contra menos de 1.000 do sistema descrito. A política fixa também fica ligeiramente à frente de Dream-RSI em autocorrelação (1,456001).

## Questões metodológicas para ensinar

A política só pode observar o prefixo revelado. O apêndice B explicita a interface e restrições: não consultar scores futuros nem codificar IDs vencedores. O replay só garante fidelidade aos resultados armazenados; a cobertura de ações inéditas é limitada. Manter a política vigente no conjunto de candidatas impede piora na pontuação daquele replay, mas não assegura generalização. O aprendizado pode favorecer peculiaridades das árvores usadas para selecionar a política.

Separar quatro contas: custo da coleta histórica; custo de desenvolver políticas; custo de percorrer o replay; custo de executar o programa final. O paper enfatiza chamadas/gerações de descoberta e performance downstream; extrapolação para dinheiro exige medição adicional.

## Destino das 14 referências do resumo

1. Vídeo YouTube: fonte secundária motivadora; link preservado, sem fingir nova transcrição.
2. Dream-RSI: referência central identificada; paper, site e repo fornecidos.
3. RSI: conceito explicado no escopo operacional do paper.
4. Gemini: nome do modelo confirmado no experimento, sem inferir disponibilidade pública de produto.
5. AlphaEvolve: contexto e comparação de mecanismos, fonte primária DeepMind.
6. Borg: componente de infraestrutura no resultado AlphaEvolve, não benchmark Dream-RSI.
7. AlphaGo e 8. AlphaFold: contexto ilustrativo; não evidência do método.
9. Geoffrey Hinton e 10. Jensen Huang/GPUs: narrativa histórica simplificada, não causalidade demonstrada aqui.
11. Demis Hassabis: atribuição não verificada; não converter paráfrase em citação.
12. Transformers e 13. LLMs: glossário e contexto, sem necessidade de uma história completa da arquitetura.
14. World models: distinguir modelo aprendido de dinâmica de um replay que consulta resultados já realizados.

## Glossário editorial

- Política de exploração: código que escolhe ramos, paralelismo e parada.
- Discovery tree: árvore de tentativas registradas e relações de descendência.
- Replay: reavaliar escolhas consultando resultados guardados.
- Off-policy: avaliar uma política usando experiência coletada por outra, dentro das restrições do histórico.
- Baseline: referência de comparação; precisa de orçamento e condições claros.
- Downstream: desempenho do programa descoberto em sua tarefa final.
- Ablation / ablação: comparação que altera um componente para avaliar sua contribuição.
- Generalização: desempenho fora das situações usadas para ajustar/selecionar a política.

## Fontes primárias

- [Site Dream-RSI](https://www.dream-rsi.com/).
- [Artigo v1 completo](https://arxiv.org/html/2609.14858v1).
- [Registro bibliográfico](https://arxiv.org/abs/2609.14858).
- [Repositório oficial](https://github.com/zhengkid/Dream-RSI): em 19/09, README informa código em preparação; não prometer instalação executável completa.
- [AlphaEvolve, DeepMind](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/).
- [Vídeo de origem](https://www.youtube.com/watch?v=thR9_VYJiQo): secundário.

## Imagens

Cinco arquivos originais locais: figuras 1, 2, 3(b), 4 e 6. As legendas em português são externas às figuras; os pixels originais foram preservados. `fontes/imagens.json` registra origem, data, crédito e SHA-256. Direitos dos respectivos titulares; nenhuma licença ampla foi presumida. O material anexado por imagem não foi necessário para validar resultados e não substitui figuras científicas.
