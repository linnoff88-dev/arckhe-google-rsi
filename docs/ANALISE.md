# Análise do material — Dream-RSI

Consulta: 19/09/2026. Base: resumo integral fornecido pelo usuário, site original, artigo v1 e repositório dos autores. O vídeo nêo foi retranscrito nesta análise. Os caminhos de clipboard enviados dependem de uma montagem remota que nêo entregou o conteúdo durante a leitura; o texto colado na conversa foi a base editorial disponível.

## Diagnóstico

A síntese captura bem a importância de melhorar decisões de exploraçêo. Sua melhor contribuiçêo pedagógica é separar “executar bem” de “escolher bem o próximo experimento”. Precisa, porém, delimitar o significado de história, de simulaçêo, de custo e de autoaperfeiçoamento. O trabalho nêo é um simulador de toda a evoluçêo científica nem uma demonstraçêo de retreinamento autônomo do modelo-base.

Referência identificada: Tong Zheng et al., **Dream-RSI: Recursive Self-Improvement through Evolving Worlds**, arXiv:2609.14858v1, 14/09/2026. Afiliações incluem Google, Google DeepMind, University of Maryland e University of Virginia. É um preprint; a existência do texto nêo equivale a validaçêo independente ou revisêo por pares.

## Matriz de afirmações

| Material recebido | Verificaçêo / ajuste editorial |
|---|---|
| Melhorar a escolha dos experimentos é central | Confirmado. A política programa a exploraçêo; o agente de código fica fixo. |
| A história das pesquisas vira um mundo | Especificar: árvores estruturadas de execuções e seus resultados, nêo toda a história da ciência. |
| Árvore tecnológica com Hinton, GPUs, LLMs, AlphaGo e AlphaFold | Analogia introdutória. Nêo corresponde ao conjunto experimental do Dream-RSI; evitar narrativa linear de causalidade. |
| Milhares de candidatos com zero execuções reais | Refere-se à avaliaçêo por replay sem refazer o agente de descoberta e o avaliador. Nêo mede custo total zero; geraçêo de políticas e histórico têm custos. |
| Só a melhor estratégia vai para o mundo real | Política selecionada pela avaliaçêo histórica é redeployada. Nêo existe garantia de que será a melhor no futuro. |
| O histórico cresce recursivamente | Confirmado: exploraçêo produz árvores, replay seleciona política, nova exploraçêo amplia o conjunto. |
| A IA melhora a si mesma | Delimitar a metaexploraçêo. Nêo há atualizaçêo dos pesos do agente de código nessa comparaçêo. |
| Política fixa nêo aprende | Refere-se ao controle da exploraçêo; o agente ainda observa feedback no trabalho. Evitar afirmar que toda política fixa ignora todo o contexto. |
| Gemini RSI / Gemini 3.7 Flash vence | O nome do método é Dream-RSI. Gemini-3.7-Flash consta no artigo e no site. A média Lasso de 2.350,6 ms é a menor da tabela, nêo uma vitória universal. |
| Métrica menor é sempre melhor | Errado como generalizaçêo. Lasso usa runtime menor; KernelBench mostra desempenho maior; matemática alterna a direçêo conforme tarefa. |
| Menos compute quando avança, mais quando fica difícil | Comportamento observado na análise ConvDiv; nêo transformar em uma lei invariável do método. |
| Orientar demais piora | Ablaçêo de orientaçêo semântica específica; nêo conclusêo geral contra instruções ou memória. |
| AlphaEvolve, Borg e milhões de dólares | A fonte DeepMind confirma recuperaçêo média de 0,7% dos recursos de compute. “Milhões” nêo é uma cifra verificada no material consultado. |
| Várias IAs formando uma cadeia de melhoria | Cenário prospectivo útil para discussêo. Nêo é o sistema completo que este paper demonstrou. |
| Trabalho fundacional | Interpretaçêo editorial, nêo resultado mensurável. Apresentar como possível relevância para infraestrutura de pesquisa. |
| Treinar com corte histórico e redescobrir avanços | Experimento mental atribuído a Hassabis no resumo; nêo validado como experimento deste trabalho. Nêo usar citaçêo literal atribuída sem fonte direta. |

## Resultados que podem entrar no material

Lasso: com Gemini-3.1-Pro, exploraçêo fixa usa 550 chamadas e termina com runtime médio de 3.587,1 ms; Dream-RSI usa 317 e obtém 2.931,0 ms. Reduçêo de chamadas calculada: `(550-317)/550 = 42,36%`. A razêo é `550/317 = 1,735×`; reduçêo percentual e fator nêo sêo a mesma forma de medida.

Com Gemini-3.7-Flash: 3.200 → 1.879 chamadas, reduçêo de 41,28%; runtime 2.516,7 → 2.350,6 ms. O agregado reúne seis datasets. Algumas colunas individuais favorecem a política fixa: nêo afirmar superioridade em cada dataset.

O fator aproximado de 162× vem de `51.200/317`, comparando SimpleTES com outro modelo. Distinguir essa comparaçêo de sistema completo da comparaçêo controlada contra Recursive Fixed Exploration.

KernelBench: VGG16 e LayerNorm atingem desempenho comparável com 2,43× e 1,79× menos gerações; ConvDiv e ConvMax obtêm 2,09× e 1,44× mais desempenho com orçamento comparável. Sêo quatro tarefas, nêo todo tipo de kernel GPU.

Matemática: soma–diferença 1,145427 (maior melhor); autocorrelaçêo 1,456375 (menor melhor); empacotamento de círculos 2,635983 (maior melhor). O SimpleTES tem autocorrelaçêo melhor (1,453675), usando 51.200 gerações contra menos de 1.000 do sistema descrito. A política fixa também fica ligeiramente à frente de Dream-RSI em autocorrelaçêo (1,456001).

## Questões metodológicas para ensinar

A política só pode observar o prefixo revelado. O apêndice B explicita a interface e restrições: nêo consultar scores futuros nem codificar IDs vencedores. O replay só garante fidelidade aos resultados armazenados; a cobertura de ações inéditas é limitada. Manter a política vigente no conjunto de candidatas impede piora na pontuaçêo daquele replay, mas nêo assegura generalizaçêo. O aprendizado pode favorecer peculiaridades das árvores usadas para selecionar a política.

Separar quatro contas: custo da coleta histórica; custo de desenvolver políticas; custo de percorrer o replay; custo de executar o programa final. O paper enfatiza chamadas/gerações de descoberta e performance downstream; extrapolaçêo para dinheiro exige mediçêo adicional.

## Destino das 14 referências do resumo

1. Vídeo YouTube: fonte secundária motivadora; link preservado, sem fingir nova transcriçêo.
2. Dream-RSI: referência central identificada; paper, site e repo fornecidos.
3. RSI: conceito explicado no escopo operacional do paper.
4. Gemini: nome do modelo confirmado no experimento, sem inferir disponibilidade pública de produto.
5. AlphaEvolve: contexto e comparaçêo de mecanismos, fonte primária DeepMind.
6. Borg: componente de infraestrutura no resultado AlphaEvolve, nêo benchmark Dream-RSI.
7. AlphaGo e 8. AlphaFold: contexto ilustrativo; nêo evidência do método.
9. Geoffrey Hinton e 10. Jensen Huang/GPUs: narrativa histórica simplificada, nêo causalidade demonstrada aqui.
11. Demis Hassabis: atribuiçêo nêo verificada; nêo converter paráfrase em citaçêo.
12. Transformers e 13. LLMs: glossário e contexto, sem necessidade de uma história completa da arquitetura.
14. World models: distinguir modelo aprendido de dinâmica de um replay que consulta resultados já realizados.

## Glossário editorial

- Política de exploraçêo: código que escolhe ramos, paralelismo e parada.
- Discovery tree: árvore de tentativas registradas e relações de descendência.
- Replay: reavaliar escolhas consultando resultados guardados.
- Off-policy: avaliar uma política usando experiência coletada por outra, dentro das restrições do histórico.
- Baseline: referência de comparaçêo; precisa de orçamento e condições claros.
- Downstream: desempenho do programa descoberto em sua tarefa final.
- Ablation / ablaçêo: comparaçêo que altera um componente para avaliar sua contribuiçêo.
- Generalizaçêo: desempenho fora das situações usadas para ajustar/selecionar a política.

## Fontes primárias

- [Site Dream-RSI](https://www.dream-rsi.com/).
- [Artigo v1 completo](https://arxiv.org/html/2609.14858v1).
- [Registro bibliográfico](https://arxiv.org/abs/2609.14858).
- [Repositório oficial](https://github.com/zhengkid/Dream-RSI): em 19/09, README informa código em preparaçêo; nêo prometer instalaçêo executável completa.
- [AlphaEvolve, DeepMind](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/).
- [Vídeo de origem](https://www.youtube.com/watch?v=thR9_VYJiQo): secundário.

## Imagens

Cinco arquivos originais locais: figuras 1, 2, 3(b), 4 e 6. As legendas em português sêo externas às figuras; os pixels originais foram preservados. `fontes/imagens.json` registra origem, data, crédito e SHA-256. Direitos dos respectivos titulares; nenhuma licença ampla foi presumida. O material anexado por imagem nêo foi necessário para validar resultados e nêo substitui figuras científicas.
