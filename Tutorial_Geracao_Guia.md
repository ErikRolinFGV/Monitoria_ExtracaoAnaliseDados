# Como montar o seu próprio guia de consulta

*Material de monitoria | Extração e Análise de Dados | FGV Comunicação*

Eu tenho um guia de consulta que uso para a prova: um notebook com trinta seções, uma para cada coisa que a prova cobra, cada uma com o trecho de código pronto para copiar e uma linha de palavras-chave para achar por `Ctrl+F`. Mostrei ele na monitoria.

Não vou distribuir o arquivo, e o motivo não é mesquinhez: **montar a cola é metade do estudo.** Quando você escreve a linha de busca com as palavras que o enunciado usa, testa cada trecho e descobre que não sabe explicar um deles, você aprende. Quando você baixa a cola pronta de outra pessoa, você tem um PDF que não vai achar nada dentro na hora do desespero.

O que eu posso fazer, e é o que este documento faz, é te contar exatamente como eu gerei o meu.

**Este tutorial parte de um fato:** no plano gratuito o guia não sai numa tacada só. Já testamos. Então em vez de torcer para o limite aguentar, o processo abaixo é dividido em **duas etapas**, com o corte num lugar escolhido por mim, e não onde o limite resolver cair. Cada etapa é uma conversa nova e independente. Se a sua conta aguentar tudo de uma vez, melhor, e a seção 5 explica o atalho.

---

## 1. Os arquivos

Está tudo na pasta `documentos_guia/` deste repositório. Baixe o repositório (botão verde **Code**, ou `git clone`) e abra a pasta. Cada etapa anexa um conjunto diferente, e as seções 3 e 4 dizem qual.

Duas regras que valem para as duas etapas:

**Use a `resolucao_simulado.ipynb` que está dentro de `documentos_guia/`**, não a da raiz. É o mesmo conteúdo, sem os gráficos guardados como imagem: 123 KB em vez de 375 KB. Aqueles 252 KB de diferença são texto codificado que o modelo não aproveita e que você paga de novo a cada mensagem da conversa.

**Não anexe os notebooks das aulas.** Somam 199 KB e repetem em prosa o que os `comandos_XX.md` dizem em tabela, em 22 KB. Eles estão na pasta para você consultar, e para o caso de faltar algo de uma aula específica. Se isso acontecer, anexe só aquele, numa mensagem separada.

**Antes de gerar, abra e rode a resolução.** O guia sai muito melhor se você já tiver visto o código funcionando, porque aí você reconhece o que o modelo te entrega em vez de aceitar no escuro.

> Os `comandos_XX.md` são meus, e resumem os notebooks do professor, que ficam em https://github.com/mateuspestana/extracao_analise_2026 . Na dúvida sobre qualquer trecho, a palavra final é a dele.

---

## 2. Modelo e orçamento

Use o **Claude**, em [claude.ai](https://claude.ai). Modelo: o melhor que o seu plano oferecer, **Sonnet** dá conta, **Opus** erra menos em código. Coloque o esforço em **High** ou **Max** e ligue o raciocínio estendido se o botão aparecer.

Três regras de orçamento, porque o limite é por quantidade de mensagens e **cada mensagem carrega tudo que veio antes, anexos inclusive**:

1. **Conversa nova para cada etapa.** Conversa que já tem assunto dentro começa com o orçamento gasto.
2. **Anexos e prompt na mesma mensagem.**
3. **Nada de mensagem sem conteúdo.** Sem "ok", sem "pode seguir", sem "perfeito, obrigado". Se a resposta parar no meio, escreva só `CONTINUAR`, uma palavra.

---

## 3. Etapa 1: da §00 à §18

É a metade que cobre **cinco das oito questões do simulado**: limpeza, tabelas e gráficos. Ela vem primeiro de propósito. Se a etapa 2 der errado, você ainda tem em mãos a parte que mais cai.

**Anexe** (155 KB): os `comandos_05.md`, `comandos_06.md` e `comandos_10.md`, o `Simulado.ipynb` e a `resolucao_simulado.ipynb` da pasta. Cole o prompt abaixo na mesma mensagem.

```
Escreva a PRIMEIRA METADE de um notebook de consulta rápida para uma prova
prática de análise de dados. Comece pela primeira célula já nesta resposta. Sem
introdução, sem plano, sem me pedir confirmação de nada: a primeira linha da
sua resposta é o título do notebook.

CONTEXTO
Sou aluno de Comunicação Digital na FGV, na disciplina de Extração e Análise de
Dados. A prova é prática, em sala, num ambiente Python no navegador, individual
e sem IA. Posso consultar material próprio, e este notebook é o que eu vou
abrir durante a prova para procurar coisas com Ctrl+F. Ele não é para rodar, é
para copiar trecho e adaptar.

O ORÇAMENTO, QUE É A RESTRIÇÃO MAIS IMPORTANTE
Estou no plano gratuito e a resposta vai ser cortada se você escrever demais.
Guia enxuto completo vale mais que guia detalhado pela metade. Portanto:
- no máximo UMA frase de explicação por seção, e só onde existe armadilha de
  verdade. Seção sem armadilha vai com título, linha Ctrl+F e código, nada mais;
- no máximo 12 linhas de código por seção;
- nada de níveis, variações, "opção A / opção B" ou casos raros. Um caminho por
  seção. Se houver uma alternativa que cai na prova, ela é UMA linha comentada
  dentro do mesmo bloco;
- nada de texto de abertura, de transição ou de encerramento entre as seções.
Se a sua resposta for cortada no meio, eu escrevo CONTINUAR e você retoma
exatamente da célula onde parou, sem recomeçar, sem resumir e sem se desculpar.

DE ONDE VEM O CONTEÚDO
Os arquivos comandos_XX.md são a fonte dos comandos: use o que está neles. Se
incluir um comando que não aparece em nenhum anexo, escreva "(não caiu nas
aulas)" ao lado, para eu saber o que é apoio e o que é chute.
Os exemplos usam os nomes de coluna do caso Festival ViraBairro, que está no
simulado e na resolução anexados: id_publicacao, tema, formato, data_publicacao,
alcance, taxa_engajamento_pct e as demais que aparecerem. Nada de coluna_x.
Da resolução você pode tirar nomes de coluna e armadilhas. Não pode tirar
número, resultado nem resposta pronta das questões, e não resolva o simulado.

FORMATO
Célula Markdown com o título e a busca, seguida de célula de código. Assim:

    # §04 · Duplicatas

    `Ctrl+F:` duplicidade, duplicata, registro repetido, drop_duplicates, por id

    `drop_duplicates()` sem argumento só apaga linhas idênticas em todas as
    colunas. Se o enunciado disser "duplicidade por id_publicacao", use `subset`.

    # TROQUE: a coluna de identificador
    print("duplicadas:", bruto.duplicated(subset="id_publicacao").sum())
    limpo = bruto.drop_duplicates(subset="id_publicacao", keep="first").copy()
    # se pedir linha inteira repetida: bruto.drop_duplicates()

A linha `Ctrl+F:` é o que faz o guia funcionar. Use as palavras que aparecem
nos enunciados do simulado anexado, com sinônimos. `# TROQUE:` marca a linha
que eu edito ao adaptar.

COMECE POR UM CABEÇALHO
No máximo 4 linhas, e em seguida uma tabela "Mapa rápido", com as colunas "Se a
questão pede" e "Vá para". Uma linha por tipo de pedido, escrita com as palavras
do enunciado, apontando para o § certo. Cerca de 30 linhas, cada uma com no
máximo 10 palavras. Inclua também as linhas que apontam para §19 a §30, que eu
vou escrever depois: modelos, threshold, importâncias, clusterização, erros e
frases de resposta. Essa tabela é a primeira coisa que eu leio na prova.

AS SEÇÕES DESTA ETAPA, NESTA ORDEM, UMA POR TAREFA
§00 Imports
§01 Carregar o CSV
§02 Olhar a base antes de mexer (head, shape, dtypes)
§03 Valores ausentes, mostrando só as colunas que têm ausência
§04 Duplicatas
§05 Padronizar texto e categoria (grafias diferentes da mesma coisa)
§06 Converter data. ARMADILHA PRINCIPAL DA PROVA, e a única seção que pode ter
    duas frases: sem format o pandas adivinha pela primeira linha e mata como
    NaT o que não encaixa, e dayfirst=True troca dia e mês das datas ISO. Mande
    conferir .min() e .max() depois de converter
§07 Coluna numérica que veio como texto
§08 Ausências e valores inválidos
§09 Criar coluna calculada (taxa, percentual)
§10 Tabela resumo por UMA coluna (groupby, agg, reset_index, sort_values)
§11 Tabela resumo por DUAS colunas
§12 Os N maiores, ordenar, ranking
§13 Filtrar linhas
§14 Data: dia, hora, dia da semana
§15 Gráfico de barras vertical, com título, nome de eixo e fonte
§16 Gráfico de barras horizontal
§17 Gráfico de linhas ao longo do tempo
§18 Dispersão com linha de referência

PARE NA §18. Não escreva §19 nem nada depois dela, não anuncie o que viria a
seguir, não escreva conclusão. A última coisa da sua resposta é a célula de
código da §18.
```

**Quando terminar, salve.** Copie tudo para um notebook chamado `Guia_Rapido_Consulta.ipynb` e guarde. Esse arquivo é o insumo da etapa 2, então não pule este passo.

---

## 4. Etapa 2: da §19 à §30

**Conversa nova.** Não continue a anterior: ela já está carregando 155 KB de anexo que a etapa 2 não usa.

**Anexe** (cerca de 47 KB): o `Guia_Rapido_Consulta.ipynb` que você salvou, os `comandos_11.md`, `comandos_12.md` e `comandos_13.md`, e o `Simulado.ipynb`.

O guia da etapa 1 entra no lugar da resolução: ele já tem os nomes de coluna e já mostra o formato, então o modelo copia a si mesmo em vez de precisar deduzir tudo de novo. É isso que faz esta etapa custar um terço da primeira.

```
Anexei um notebook de consulta que eu montei, que vai da §00 à §18, e os
materiais de aula das partes que faltam. Continue esse mesmo notebook, da §19
à §30. Comece pela célula da §19 já nesta resposta, sem introdução, sem
resumir o que já existe e sem me pedir confirmação de nada.

SIGA O FORMATO DO NOTEBOOK ANEXADO, exatamente: célula Markdown com o título no
padrão "# §NN · Nome curto", depois a linha "`Ctrl+F:` " com as palavras que o
enunciado usaria e os sinônimos, depois no máximo UMA frase de explicação e só
onde existe armadilha de verdade, e então a célula de código com "# TROQUE:"
marcando a linha que eu edito. Use os mesmos nomes de coluna que já estão lá
(id_publicacao, tema, formato, data_publicacao, alcance, taxa_engajamento_pct e
as demais do caso Festival ViraBairro).

ORÇAMENTO: estou no plano gratuito. No máximo 12 linhas de código por seção,
nada de níveis nem de variações, um caminho por seção, e alternativa que cai na
prova vira UMA linha comentada dentro do mesmo bloco. Se a resposta for cortada,
eu escrevo CONTINUAR e você retoma da célula onde parou, sem recomeçar.

CONTEÚDO: tire os comandos dos comandos_XX.md anexados. Se usar um comando que
não aparece em nenhum anexo, escreva "(não caiu nas aulas)" ao lado. Não
resolva o simulado, não invente número nem resultado.

AS SEÇÕES QUE FALTAM
§19 Regressão, classificação ou clusterização? (só um quadro de decisão, sem
    código)
§20 Montar X e y, get_dummies e vazamento
§21 Treino e teste (stratify só em classificação, nunca em regressão)
§22 Regressão: estimar um número (MAE, R², modelo bobo)
§23 Criar o rótulo por percentil
§24 Classificação: treinar e comparar modelos
§25 Métricas e matriz de confusão
§26 Ajustar o corte (threshold)
§27 Importâncias e coeficientes
§28 Clusterização com KMeans (uma seção só: não cai no simulado)
§29 Deu erro. Uma tabela de no máximo 10 linhas, colunas "mensagem", "o que é",
    "vá para §". Inclua os erros que NÃO aparecem em vermelho, aqueles em que o
    código roda e entrega número errado
§30 Frases prontas para os campos de resposta em Markdown, com lacunas do tipo
    ____ para eu preencher com os números da minha tela. Dez frases, uma ou duas
    linhas cada, cobrindo: mediana, MAE, R², causalidade, tamanho da amostra,
    empate entre categorias, justificar decisão de limpeza, justificar o corte
    escolhido, vazamento, e limitação de generalização

Se precisar cortar alguma coisa por falta de espaço, corte das seções de modelo.
Nunca corte a §29 nem a §30.
```

Cole o resultado no fim do mesmo arquivo e o guia está inteiro.

---

## 5. Os dois atalhos, se sobrar limite

**Se a etapa 1 terminar e você ainda tiver folga**, não abra conversa nova: escreva na mesma conversa "Agora continue da §19 à §30, mesmo formato" e cole a lista de seções da etapa 2. Sai mais barato, porque os anexos já estão pagos.

**Se a resposta parar no meio de uma etapa**, escreva `CONTINUAR`. Se parar duas vezes e você sentir que não chega ao fim, peça o resto seco: "Termine do §NN em diante só com título, linha `Ctrl+F` e código, sem nenhuma frase de explicação." Guia completo e feio bate guia bonito que acaba no §17.

---

## 6. Depois que o notebook está inteiro, que é onde ele fica bom

As mensagens que sobraram valem mais que as que você gastou. Em ordem de retorno:

**"Na §NN a linha `Ctrl+F` está fraca. Acrescente as palavras que a questão N do simulado usa."** Abra o simulado do lado e compare seção por seção. Essa parte só você pode fazer bem, porque é a sua cabeça que vai procurar. Se você sempre pensa "tabelinha por tema" e o guia só diz "agrupamento", você não vai achar na hora.

**"Explique o trecho da §NN como se eu nunca tivesse visto."** Faça isso em todo bloco que você não saberia explicar em voz alta. E aí vem a regra mais importante deste documento inteiro:

> **Se você não entende um trecho, tire ele do guia.** Código que você não entende não te salva na prova: você cola, dá erro, e não sabe nem por onde começar a consertar. Um guia de vinte seções que você domina vale mais que um de trinta que você decorou.

**Rode tudo.** Abra o notebook, aponte para as bases de `dados/` e execute. O que não rodar, conserte ou corte. Trecho de guia que não roda é armadilha, não apoio.

**Confira a costura.** O guia veio de duas conversas, então olhe a virada da §18 para a §19: numeração seguida, mesmo padrão de título, mesmos nomes de coluna. Se a segunda metade veio com outra cara, é sinal de que você esqueceu de anexar o notebook da etapa 1.

E **corte e acrescente seções.** A lista que vai nos prompts é o meu índice, montado pela minha cabeça e pelo jeito que eu erro. Se você travou em `explode` a semana inteira e isso não está lá, vira seção. Se você nunca vai usar PCA, sai. Um guia que é cópia do índice de outra pessoa é exatamente o PDF inútil contra o qual este tutorial foi escrito.

---

## 7. Confira antes de confiar

O Claude erra, e erra com confiança. Em particular ele às vezes sugere um comando mais novo ou mais elegante do que o que foi ensinado, e isso não ajuda numa prova corrigida por quem ensinou de outro jeito. É para isso que serve a marca "(não caiu nas aulas)": onde ela aparecer, pense duas vezes antes de manter.

**Desconfie de número.** Se o guia citar um resultado ("a mediana dá 1,15"), confira rodando. Número que você não viu na sua tela não entra na sua resposta. Vale para o que a IA te disser e vale para o que eu escrevi na resolução.

---

## 8. O combinado

Isto é preparação, não execução. **A prova é sem IA**, é individual, e vocês vão escrever tudo do zero lá dentro. Gerar o guia serve para você chegar tendo lido, testado e entendido os comandos, com um índice que você mesmo organizou e sabe navegar.

Se você gerar o seu e quiser que eu olhe, me manda. Comparar a sua organização com a minha costuma ser a parte mais útil de tudo isso.

**Erik Rolin**
Monitor de Extração e Análise de Dados
WhatsApp: (21) 99202 5739
