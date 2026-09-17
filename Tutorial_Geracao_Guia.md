# Como montar o seu próprio guia de consulta

*Material de monitoria | Extração e Análise de Dados | FGV Comunicação*

Eu tenho um guia de consulta que uso para a prova: um notebook com trinta seções, uma para cada coisa que a prova cobra, cada uma com o trecho de código pronto para copiar e uma linha de palavras-chave para achar por `Ctrl+F`. Mostrei ele na monitoria.

Não vou distribuir o arquivo, e o motivo não é mesquinhez: **montar a cola é metade do estudo.** Quando você decide o que entra, escreve a linha de busca com as palavras que o enunciado usa e descobre que não sabe explicar um trecho, você aprende. Quando você baixa a cola pronta de outra pessoa, você tem um PDF que não vai achar nada dentro na hora do desespero.

O que eu posso fazer, e é o que este documento faz, é te contar exatamente como eu gerei o meu. Siga isso e em uma tarde você tem um guia igual ou melhor, com as suas palavras e do jeito que a sua cabeça procura as coisas.

---

## 1. O que você precisa ter em mãos antes de começar

**A resolução comentada do simulado.** Está neste repositório, em `resolucao_simulado.ipynb`. Ela roda, então abra e execute antes: o guia que você vai gerar sai muito melhor se você já tiver visto o código funcionando.

**Os notebooks das aulas do professor.** Baixe do repositório da disciplina. Não precisa de todos: **as aulas 5, 6, 10, 11, 12 e 13** cobrem tudo que a prova pede. A aula 5 e a 10 são pandas, a 6 é gráfico, a 11 é regressão, a 12 é classificação e a 13 é clusterização.

> Repositório do professor: preencha aqui o link que eu passo na monitoria.

**O enunciado do simulado.** Se você tiver o texto das oito questões, melhor ainda: é dele que saem as palavras que você vai usar na linha de busca de cada seção.

Junte tudo numa pasta. Você vai anexar esses arquivos na conversa.

---

## 2. Onde fazer, com qual modelo e com qual esforço

Use o **Claude**, em [claude.ai](https://claude.ai). A conta gratuita dá conta deste trabalho.

**Modelo.** Pegue o melhor que o seu plano oferecer no seletor de modelos. O **Sonnet** é suficiente para esta tarefa e costuma ser o que o plano gratuito oferece. Se aparecer **Opus**, use Opus: ele erra menos em código.

**Esforço e raciocínio.** No seletor, junto do modelo, existe um ajuste de **esforço** com as opções Low, Medium, High, Extra high e Max, e um botão de **raciocínio estendido** (thinking). Para este trabalho:

* coloque o esforço em **High** (que costuma ser o padrão) ou **Max**, se o seu plano deixar;
* **ligue o raciocínio estendido** se o botão aparecer. Em alguns modelos ele já vem sempre ligado e não dá para desligar.

Esforço baixo serve para pergunta rápida. Aqui você está pedindo um documento longo, com código que precisa estar certo, então vale gastar.

**Uma dica sobre o limite do plano gratuito.** O limite é por quantidade de mensagens, não por tamanho. Então **prefira poucas mensagens grandes a muitas pequenas**: anexe tudo de uma vez, mande o prompt inteiro de uma vez, e guarde as mensagens restantes para os ajustes.

---

## 3. O prompt

Anexe os arquivos e cole o texto abaixo. Ele é longo de propósito: cada parágrafo ali está evitando um jeito específico de o resultado sair ruim.

```
Você vai me ajudar a montar um guia de consulta rápida para uma prova prática
de análise de dados.

CONTEXTO
Sou aluno de Comunicação Digital na FGV, na disciplina de Extração e Análise
de Dados. A prova é prática, feita em sala, num ambiente Python no navegador,
individual e sem IA. Posso consultar material próprio, então este guia é para
eu abrir durante a prova e procurar coisas com Ctrl+F.
Estou anexando: a resolução comentada de um simulado e os notebooks das aulas
que a prova cobre.

O QUE EU QUERO
Um notebook .ipynb chamado Guia_Rapido_Consulta, organizado em seções
numeradas (§01, §02, ...), uma seção por tarefa que a prova pode pedir.

REGRAS DE CONTEÚDO
1. Extraia os comandos DOS MATERIAIS ANEXADOS. Se você incluir algum comando
   que não aparece em nenhum deles, escreva ao lado: "não apareceu nas aulas".
   Eu preciso saber o que é apoio e o que é chute.
2. Use os nomes de coluna reais das bases anexadas nos exemplos, não nomes
   genéricos tipo "coluna_x". Quero copiar e colar trocando o mínimo.
3. Marque com o comentário # TROQUE: exatamente a linha que eu preciso editar
   ao adaptar o trecho.
4. Cada seção começa com uma linha "Ctrl+F:" listando as palavras que o
   enunciado da prova usaria para pedir aquilo, incluindo sinônimos. Essa linha
   é o que faz o guia funcionar: capriche nela.
5. Nas seções de limpeza de dados, me dê NÍVEIS: um Nível 1 simples, que
   resolve o caso normal, e um Nível 2 mais completo, para quando a base vier
   mais suja. Não misture os dois no mesmo bloco. Eu prefiro escrever pouco
   código e entender tudo a escrever muito e não saber explicar.
6. Para cada armadilha, explique o MOTIVO em uma ou duas frases, não só o
   conserto. Preciso reconhecer o problema na prova, não decorar a linha.
7. Inclua uma seção final de mensagens de erro: o que a mensagem diz, o que
   ela significa e qual seção resolve. Inclua também os erros que NÃO aparecem
   em vermelho, aqueles em que o código roda e entrega número errado.
8. Inclua uma seção de frases prontas para os campos de resposta em Markdown,
   com lacunas para eu preencher com os números da minha tela.

O QUE NÃO FAZER
Não resolva o simulado por mim. Não invente número nem resultado. Se um trecho
depender de algo que não está nos anexos, diga isso em vez de preencher.

COMO COMEÇAR
Antes de escrever o guia, liste para mim as seções que você pretende criar, em
uma linha cada. Eu confirmo ou ajusto, e só então você escreve o notebook.
```

O último parágrafo é o mais importante do prompt inteiro. Ele faz o Claude te mostrar o esqueleto antes de gastar uma resposta longa escrevendo a coisa errada. Olhe a lista com atenção: se faltar alguma questão do simulado ali, peça para acrescentar **antes** de mandar ele escrever.

---

## 4. Depois da primeira versão

Não pare na primeira resposta. Três pedidos que melhoram muito o resultado:

**"Rode cada trecho de código contra as bases que eu anexei e me diga qual deu erro."** Ele consegue executar. Trecho de guia que não roda é armadilha, não apoio.

**"Na seção X, a linha `Ctrl+F` está fraca. Acrescente as palavras que o enunciado da questão N usa."** Compare cada seção com o enunciado real. Essa é a parte que só você pode fazer bem, porque é a sua cabeça que vai procurar.

**"Explique o trecho da seção X como se eu nunca tivesse visto."** Faça isso em todo bloco que você não saberia explicar em voz alta. E aí vem a regra mais importante deste documento inteiro:

> **Se você não entende um trecho, tire ele do guia.** Código que você não entende não te salva na prova: você cola, dá erro, e você não sabe nem por onde começar a consertar. Um guia de vinte seções que você domina vale mais que um de quarenta que você decorou.

---

## 5. Confira antes de confiar

O Claude erra, e erra com confiança. Em particular ele às vezes sugere um comando mais novo ou mais elegante do que o que foi ensinado, e isso não te ajuda numa prova corrigida por quem ensinou de outro jeito.

Três conferências que valem o tempo:

**Rode tudo.** Abra o guia gerado, aponte para as bases e execute. O que não rodar, conserte ou corte.

**Compare com a aula.** Se um comando não aparece em nenhum notebook do professor, pense duas vezes antes de deixar no guia. Não está proibido, mas o caminho que a aula ensinou é o que você vai lembrar sob pressão.

**Desconfie de número.** Se o guia citar um resultado ("a mediana dá 1,15"), confira rodando. Número que você não viu na sua tela não entra na sua resposta. Vale para o que a IA te disser e vale para o que eu escrevi na resolução.

---

## 6. O combinado

Isto é preparação, não execução. **A prova é sem IA**, é individual, e vocês vão escrever tudo do zero lá dentro. Gerar o guia serve para você chegar tendo lido, testado e entendido os comandos, com um índice que você mesmo organizou e sabe navegar.

Se você gerar o seu e quiser que eu olhe, me manda. Comparar a sua organização com a minha costuma ser a parte mais útil de tudo isso.

**Erik Rolin**
Monitor de Extração e Análise de Dados
WhatsApp: (21) 99202 5739
