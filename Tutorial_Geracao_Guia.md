# Como montar o seu próprio guia de consulta

*Material de monitoria | Extração e Análise de Dados | FGV Comunicação*

Eu tenho um guia de consulta que uso para a prova: um notebook com trinta seções, uma para cada coisa que a prova cobra, cada uma com o trecho de código pronto para copiar e uma linha de palavras-chave para achar por `Ctrl+F`. Mostrei ele na monitoria.

Não vou distribuir o arquivo, e o motivo não é mesquinhez: **montar a cola é metade do estudo.** Quando você escreve a linha de busca com as palavras que o enunciado usa, testa cada trecho e descobre que não sabe explicar um deles, você aprende. Quando você baixa a cola pronta de outra pessoa, você tem um PDF que não vai achar nada dentro na hora do desespero.

O que eu posso fazer, e é o que este documento faz, é te contar exatamente como eu gerei o meu. Siga isso e em uma tarde você tem um guia igual ou melhor, com as suas palavras e do jeito que a sua cabeça procura as coisas.

---

## 1. O que você precisa ter em mãos antes de começar

Está tudo na pasta `documentos_guia/` deste repositório. Baixe o repositório (botão verde **Code**, ou `git clone`), abra a pasta e você tem:

* **os notebooks das aulas 5, 6, 10, 11, 12 e 13**, que são as que a prova cobre. É de onde o Claude tira os comandos;
* **os `comandos_05.md` a `comandos_13.md`**, um resumo por aula de cada comando e do efeito dele;
* **o `Simulado.ipynb` em branco**, de onde saem as palavras que você vai usar nas linhas de busca;
* **a `resolucao_simulado.ipynb`**, a mesma da raiz do repositório.

Os notebooks das aulas são cópia do repositório do professor, tirada em 15/09/2026. Se ele corrigir alguma célula depois disso, a versão viva é a dele: https://github.com/mateuspestana/extracao_analise_2026

**Antes de gerar, abra e rode a resolução do simulado.** O guia sai muito melhor se você já tiver visto o código funcionando, porque aí você reconhece o que o modelo te entrega em vez de aceitar no escuro.

---

## 2. Onde fazer, com qual modelo e com qual esforço

Use o **Claude**, em [claude.ai](https://claude.ai). A conta gratuita dá conta deste trabalho, mas o orçamento é apertado, e a seção 3 foi reescrita justamente para caber nele.

**Modelo.** Pegue o melhor que o seu plano oferecer. O **Sonnet** é suficiente e costuma ser o que o plano gratuito dá. Se aparecer **Opus**, use Opus: erra menos em código.

**Esforço e raciocínio.** No seletor, junto do modelo, tem um ajuste de **esforço** (Low, Medium, High, Extra high, Max) e um botão de **raciocínio estendido**. Coloque o esforço em **High** ou **Max**, e ligue o raciocínio estendido se o botão aparecer. Em alguns modelos ele já vem ligado e não dá para desligar.

**O limite é por quantidade de mensagens, não por tamanho.** Essa é a única regra de orçamento que importa. Anexe tudo de uma vez, mande o prompt inteiro de uma vez, e não gaste mensagem com "ok", "pode seguir" ou "obrigado". Do jeito que o prompt abaixo está montado, o guia inteiro sai em **quatro mensagens suas**: o prompt e três vezes a palavra `CONTINUAR`. O que sobrar do seu limite é para a seção 4, que é onde o guia fica bom.

---

## 3. O prompt

Anexe os arquivos de `documentos_guia/` e cole o texto abaixo, inteiro, na mesma mensagem.

Ele é longo de propósito. A versão anterior deste tutorial pedia que o modelo listasse as seções e esperasse você confirmar, e isso soava prudente, mas na prática queimava duas ou três mensagens antes de existir uma linha de guia, e ainda vinha com quarenta e sete seções propostas. Agora a lista de seções já vai dentro do prompt, e o modelo escreve direto. A seção 4 explica o que você faz com isso.

```
Você vai montar um guia de consulta rápida para uma prova prática de análise
de dados. Comece a escrever o guia já nesta primeira resposta, sem preâmbulo,
sem me pedir confirmação de nada e sem repetir a lista de seções antes.

CONTEXTO
Sou aluno de Comunicação Digital na FGV, na disciplina de Extração e Análise
de Dados. A prova é prática, em sala, num ambiente Python no navegador,
individual e sem IA. Posso consultar material próprio, e este guia é o que eu
vou abrir durante a prova para procurar coisas com Ctrl+F.
Anexei os notebooks das aulas, um resumo de comandos por aula, o enunciado de
um simulado e a resolução comentada dele.

QUAL É A BASE DOS EXEMPLOS
Os exemplos devem usar os nomes de coluna do caso Festival ViraBairro, que é o
caso do simulado e do dicionário de dados: id_publicacao, tema, formato,
data_publicacao, alcance, taxa_engajamento_pct e as demais que aparecerem nos
anexos. Não use nomes genéricos tipo coluna_x, e não use as colunas das bases
das aulas (exportacao.csv, livros, clientes): as aulas entram como fonte de
COMANDO, o ViraBairro entra como fonte de NOME DE COLUNA.
Da resolução do simulado você pode tirar nomes de coluna, armadilhas e o
formato das decisões de limpeza. O que você não pode tirar dela é número,
resultado ou resposta pronta das questões.

FORMATO DE CADA SEÇÃO
Uma célula Markdown com o título, seguida de uma célula de código. A Markdown
tem, nesta ordem:
1. o título no formato "# §NN · Nome curto da tarefa";
2. uma linha "`Ctrl+F:` " com as palavras que o enunciado usaria para pedir
   aquilo, incluindo sinônimos. Essa linha é o que faz o guia funcionar:
   capriche, use as palavras que aparecem no enunciado do simulado anexado;
3. duas ou três frases, no máximo, com a armadilha da seção e o MOTIVO dela.
   O motivo importa mais que o conserto: eu preciso reconhecer o problema na
   prova, não decorar a linha.
A célula de código vem comentada, com "# TROQUE:" marcando exatamente a linha
que eu edito ao adaptar o trecho.

Exemplo do padrão que eu quero, para você seguir o tom e o tamanho:

    # §04 · Duplicatas

    `Ctrl+F:` duplicidade, duplicata, registro repetido, drop_duplicates,
    remover duplicidade por id, keep, cópias

    **Cuidado.** `drop_duplicates()` sem argumento só apaga linhas idênticas
    em **todas** as colunas. Se o enunciado disser "duplicidade por
    id_publicacao", use `subset`.

    # TROQUE: a coluna de identificador
    print("duplicadas por id:", bruto.duplicated(subset="id_publicacao").sum())
    limpo = bruto.drop_duplicates(subset="id_publicacao", keep="first").copy()

REGRAS DE CONTEÚDO
1. Extraia os comandos DOS MATERIAIS ANEXADOS. Se incluir algum comando que não
   aparece em nenhum deles, escreva ao lado: "não apareceu nas aulas". Eu
   preciso saber o que é apoio e o que é chute.
2. Nas seções §04 a §08, e só nelas, dê NÍVEIS: Nível 1 simples, que resolve o
   caso normal, e Nível 2 mais completo, para quando a base vier suja ou o
   enunciado pedir justificativa da decisão. Blocos separados, nunca misturados.
   Nas outras seções, um trecho só.
3. Peso por assunto: cinco das oito questões do simulado são pandas e
   matplotlib, e só três usam modelo. Clusterização não cai em nenhuma. Então
   as seções de limpeza, tabela e gráfico vêm completas, e clusterização ganha
   uma seção só.
4. Nada de seção com mais de uns 25 linhas de código. Se não couber, corte o
   caso raro, não o comentário.

O QUE NÃO FAZER
Não resolva o simulado por mim. Não invente número nem resultado. Se um trecho
depender de algo que não está nos anexos, diga isso em vez de preencher.

AS SEÇÕES, NESTA ORDEM
§00 Imports
§01 Carregar o CSV
§02 Olhar a base antes de mexer (head, shape, dtypes)
§03 Valores ausentes, mostrando só as colunas que têm ausência
§04 Duplicatas (linha inteira e por coluna-chave)
§05 Padronizar texto e categoria (grafias diferentes da mesma coisa)
§06 Converter data (formato fixo, formatos mistos, o estrago silencioso)
§07 Coluna numérica que veio como texto
§08 Ausências e valores inválidos (descartar, preencher ou manter)
§09 Criar coluna calculada (taxa, percentual)
§10 Tabela resumo por UMA coluna (groupby, agg, reset_index, sort_values)
§11 Tabela resumo por DUAS colunas
§12 Os N maiores, ordenar, ranking
§13 Filtrar linhas (uma e várias condições)
§14 Trabalhar com data: dia, hora, dia da semana
§15 Gráfico de barras vertical
§16 Gráfico de barras horizontal
§17 Gráfico de linhas ao longo do tempo
§18 Dispersão com linha de referência
§19 Regressão, classificação ou clusterização? (como decidir)
§20 Montar X e y, get_dummies e vazamento
§21 Treino e teste (com e sem stratify, e por que)
§22 Regressão: estimar um número (MAE, R², modelo bobo)
§23 Criar o rótulo por percentil
§24 Classificação: treinar e comparar vários modelos
§25 Métricas e matriz de confusão
§26 Ajustar o corte (threshold)
§27 Importâncias e coeficientes
§28 Clusterização com KMeans
§29 Deu erro: o que a mensagem diz, o que significa, qual seção resolve.
    Inclua os erros que NÃO aparecem em vermelho, aqueles em que o código roda
    e entrega número errado.
§30 Frases prontas para os campos de resposta em Markdown, com lacunas para eu
    preencher com os números da minha tela. Cubra pelo menos: mediana, MAE, R²,
    causalidade, tamanho da amostra, empate entre categorias, justificar uma
    decisão de limpeza, e limitação de generalização.

ANTES DO §00, um cabeçalho com uma tabela "Mapa rápido: da questão para a
seção", com duas colunas: "Se a questão pede" e "Vá para". Uma linha por tipo
de pedido, escrita com as palavras do enunciado, apontando para o § certo. Essa
tabela é o que eu leio primeiro na prova, então faça umas 30 linhas nela.

COMO ENTREGAR
Em quatro mensagens, e eu escrevo CONTINUAR entre elas. Não peça permissão para
seguir, não resuma o que fez, não repita o que vem depois. Só escreva o bloco e
pare.
Bloco 1: cabeçalho, Mapa rápido, e §00 a §09.
Bloco 2: §10 a §19.
Bloco 3: §20 a §28.
Bloco 4: §29 e §30.
No fim do bloco 4, e só ali, me diga em até cinco linhas quais comandos você
marcou como "não apareceu nas aulas" e o que ficou de fora por não estar nos
anexos.
Entregue tudo como células de notebook, para eu colar num .ipynb chamado
Guia_Rapido_Consulta.
```

---

## 4. Depois dos quatro blocos, que é onde o guia fica bom

O que você tem agora é um rascunho bem organizado, não um guia. As mensagens que sobraram valem mais que as quatro que você gastou. Em ordem de retorno:

**"Rode cada trecho contra as bases que eu anexei e me diga quais deram erro."** Ele consegue executar. Trecho de guia que não roda é armadilha, não apoio.

**"Na §NN a linha `Ctrl+F` está fraca. Acrescente as palavras que a questão N do simulado usa."** Abra o simulado do lado e compare seção por seção. Essa parte só você pode fazer bem, porque é a sua cabeça que vai procurar. Se você sempre pensa "tabelinha por tema" e o guia só diz "agrupamento", você não vai achar.

**"Explique o trecho da §NN como se eu nunca tivesse visto."** Faça isso em todo bloco que você não saberia explicar em voz alta. E aí vem a regra mais importante deste documento inteiro:

> **Se você não entende um trecho, tire ele do guia.** Código que você não entende não te salva na prova: você cola, dá erro, e não sabe nem por onde começar a consertar. Um guia de vinte seções que você domina vale mais que um de quarenta que você decorou.

Essa regra vale em dobro agora que a lista de seções vem pronta no prompt. Ela é o meu índice, montado pela minha cabeça e pelo jeito que eu erro. **Corte o que não é seu e acrescente o que falta.** Se você travou em `explode` a semana inteira e isso não está na lista, vira seção. Se você nunca vai usar PCA, sai. Um guia que é uma cópia do índice de outra pessoa é exatamente o PDF inútil contra o qual este tutorial inteiro foi escrito.

---

## 5. Confira antes de confiar

O Claude erra, e erra com confiança. Em particular ele às vezes sugere um comando mais novo ou mais elegante do que o que foi ensinado, e isso não te ajuda numa prova corrigida por quem ensinou de outro jeito.

Três conferências que valem o tempo:

**Rode tudo.** Abra o guia gerado, aponte para as bases e execute. O que não rodar, conserte ou corte.

**Compare com a aula.** Se um comando não aparece em nenhum notebook do professor, pense duas vezes antes de deixar no guia. Não está proibido, mas o caminho que a aula ensinou é o que você vai lembrar sob pressão. É para isso que serve a lista do fim do bloco 4.

**Desconfie de número.** Se o guia citar um resultado ("a mediana dá 1,15"), confira rodando. Número que você não viu na sua tela não entra na sua resposta. Vale para o que a IA te disser e vale para o que eu escrevi na resolução.

---

## 6. O combinado

Isto é preparação, não execução. **A prova é sem IA**, é individual, e vocês vão escrever tudo do zero lá dentro. Gerar o guia serve para você chegar tendo lido, testado e entendido os comandos, com um índice que você mesmo organizou e sabe navegar.

Se você gerar o seu e quiser que eu olhe, me manda. Comparar a sua organização com a minha costuma ser a parte mais útil de tudo isso.

**Erik Rolin**
Monitor de Extração e Análise de Dados
WhatsApp: (21) 99202 5739
