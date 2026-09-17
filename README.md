# Monitoria de Extração e Análise de Dados

Bem-vindos! Este repositório é o ponto de apoio da monitoria de Extração e Análise de Dados da FGV Comunicação.

*Atualizado em 17/09/2026.*

## Quem sou eu

Me chamo **Erik Rolin**, sou aluno de Comunicação Digital na FGV e monitor da disciplina de Extração e Análise de Dados. A ideia aqui é simples: juntar em um só lugar tudo que possa facilitar a vida de vocês na matéria, desde o básico até as partes que costumam travar todo mundo.

## O que já está no ar

| Arquivo | O que é |
|---|---|
| `resolucao_simulado.ipynb` | Resolução comentada das 8 questões do simulado do Festival ViraBairro, com o código, as saídas reais e a resposta escrita de cada questão. **Roda inteiro na sua máquina.** |
| `dados/` | As duas bases do simulado: `publicacoes_brutas.csv` (36 linhas) e `publicacoes_analise.csv` (120 linhas) |
| `exercicios/Exercicios_Extras.ipynb` | 10 exercícios de treino no mesmo caso, com célula em branco para você resolver e gabarito recolhido |
| `exercicios/dados/` | Os dois CSVs que os exercícios usam. **Não são os mesmos de `dados/`**, e a próxima seção explica a diferença |

## Comece por aqui

A ordem que eu recomendo é essa, e ela importa:

1. **Leia a resolução do simulado** (`resolucao_simulado.ipynb`). Em cada questão, pare no bloco *O que a questão pede* e tente escrever o código antes de olhar a célula de baixo. Depois compare.
2. **Rode a resolução.** As bases estão no repositório, então dá para executar célula por célula e ver o número aparecer. Aproveite para **quebrar o código de propósito**: tire o `format="ISO8601"` da questão 2, troque o `subset` do `drop_duplicates`, use `stratify` na questão 7. As conferências que eu deixei nas células existem justamente para mostrar o estrago, e ver o estrago acontecer ensina mais do que ler sobre ele.
3. **Faça os exercícios extras** (`exercicios/Exercicios_Extras.ipynb`), com o gabarito fechado. Eles não são a mesma prova de novo: mudei fórmula, mudei o corte, mudei o trio de modelos, e em vários casos o resultado é o **oposto** do simulado. Isso é de propósito. Se você decorou "a logística sempre ganha", o exercício 8 vai te pegar.
4. **Refaça o exercício 10 cronometrado**, com o caderno fechado. Saber fazer e saber fazer em 35 minutos são coisas diferentes.

E escreva os campos de interpretação **sempre**, mesmo quando o código não sair. Metade da nota está no texto em Markdown, e é justamente a metade que quase ninguém treina.

## Sobre os dados

São **dois** conjuntos de CSVs neste repositório, e confundir os dois gera número diferente do meu:

* **`dados/`** são as bases verdadeiras do simulado, as mesmas que rodam na plataforma do professor. É o que a resolução usa. Os números que você vê gravados no notebook saíram delas, e eu confirmei um por um contra a execução na plataforma: as mesmas medianas, os mesmos 56 dias, as mesmas cinco importâncias da árvore, a mesma matriz de confusão.
* **`exercicios/dados/`** são bases que eu construí a partir do dicionário do caso. Têm os mesmos nomes de coluna, as mesmas unidades e a mesma escala, mas os dados são outros: o período é julho, as grafias sujas são diferentes e a contagem de descartes não bate com a do simulado. Servem para os exercícios, não para conferir os números da resolução.

## Como rodar a resolução

Os notebooks abrem no Jupyter, no VS Code ou no Google Colab.

**Rode as células em ordem, da primeira à última.** A questão 1 é quem faz os `import` de pandas, numpy e matplotlib, e a questão 6 é quem importa o scikit-learn e define a lista `CARACTERISTICAS` que as questões 7 e 8 reaproveitam. Pular direto para o meio dá `NameError`.

**Sobre versões.** A plataforma roda Python 3.13 com pandas 2.3.1, e foi com pandas 2.3.1 que eu gravei as saídas. Uma ressalva que vale conhecer: o Random Forest da questão 8 **muda de resultado** no scikit-learn 1.9, a ponto de trocar o primeiro lugar em F1. Testei na 1.5.2, que dá igual à plataforma, e na 1.9.1, que dá diferente. As outras sete questões dão o mesmo número em qualquer versão recente. A célula da questão 6 imprime as suas versões instaladas, e a nota dentro da questão 8 explica por que isso acontece e o que fazer com essa informação na prova.

Para clonar:

```bash
git clone https://github.com/ErikRolinFGV/Monitoria_ExtracaoAnaliseDados.git
```

Se preferir, dá para baixar o zip direto pelo botão verde **Code** aqui em cima. Se for pelo Colab, lembre de subir também as pastas `dados/` e `exercicios/dados/`, senão o `read_csv` não acha os arquivos.

Uma observação sobre a prova: vocês podem levar um repositório próprio para consulta. Vale a pena clonar este e ir anotando as suas próprias coisas nele ao longo das semanas, porque material que você mesmo organizou você acha em dez segundos, e material que você baixou na véspera você não acha nunca.

## O que a prova cobra, em uma tabela

O simulado **não é uma prova de scikit-learn**. Só 3 das 8 questões usam modelo. As outras 5 são pandas e matplotlib das aulas 5, 6 e 10.

| Questão | O que ela cobra | Aula |
|---|---|---|
| 1 | Inspeção inicial da base | 5 e 10 |
| 2 | Limpeza e pipeline | 10 |
| 3 | Agrupamento e gráfico de barras | 5 e 6 |
| 4 | Série temporal, filtro e ranking | 5, 6 e 10 |
| 5 | Agrupamento por duas variáveis | 5 e 6 |
| 6 | Árvore de classificação e importâncias | 12 |
| 7 | Regressão e comparação de modelos | 11 |
| 8 | Classificação, métricas e threshold | 12 |

Clusterização (aula 13) não aparece em nenhuma questão do simulado.

## Os seis erros que mais custam ponto

1. Esquecer `pd.get_dummies` nas questões 6, 7 e 8. É o comando cobrado que não tem célula de exemplo nos notebooks das aulas, então é o que menos gente já rodou.
2. Usar `stratify` na regressão. Ele só vale para classificação.
3. Usar `drop_duplicates()` sem `subset="id_publicacao"` quando o enunciado pede a duplicidade por id.
4. Converter data sem dizer o formato. São dois estragos silenciosos num comando só: sem `format`, o pandas adivinha o formato pela primeira linha e mata como `NaT` toda data que não encaixa; e com `dayfirst=True` na coluna inteira, as datas em padrão ISO têm dia e mês trocados. Na base do simulado isso daria 16 datas erradas e 18 destruídas, sem uma única mensagem de erro. Confira `.min()` e `.max()` depois de toda conversão de data.
5. Gráfico sem título, sem nome de eixo ou sem a fonte. São itens explícitos do enunciado, e cada um é ponto.
6. Responder o campo de Markdown em uma frase genérica, ou deixar em branco.

## O sétimo erro, que é o mais difícil de enxergar

**Descrever um tratamento que você não fez.** É tentador escrever "descartei as linhas sem tema, com alcance zero e com contagem negativa" porque soa completo. Só que na base do simulado nenhum desses três filtros derruba uma linha sequer, e o professor tem o arquivo na mão.

O antídoto é imprimir o efeito de cada decisão em vez de só o total: quantas linhas cada filtro derrubou, qual era o `dtype` antes de converter, quantas grafias o `value_counts` mostrou. A resolução faz isso em todas as etapas da questão 2, e é de lá que sai a resposta escrita. Você só pode afirmar o que o seu print mostrou.

## A parte que separa a nota boa da nota mediana

A base é pequena, e quase toda diferença entre categorias está dentro do ruído. Antes de recomendar qualquer coisa a partir de um número, faça duas perguntas a ele:

**Quantos casos tem por trás desse número?** Uma mediana calculada sobre 8 publicações não é uma medida, é uma curiosidade.

**Qual é a distância para o segundo colocado?** Se for menor do que o deslocamento que uma única publicação atípica causaria, você não tem um vencedor, tem um empate.

A resposta preguiçosa aponta a barra mais alta. A resposta que ganha nota percebe o empate, diz isso com todas as letras, e mesmo assim entrega uma decisão utilizável. O enunciado repete em quase toda questão as palavras "limitação", "não afirme causalidade", "sem afirmar tendência". Ele está pedindo ceticismo, não ranking.

E se você quiser uma prova de que isso não é conversa de monitor: na questão 8, trocar a versão do scikit-learn é suficiente para inverter qual modelo fica em primeiro lugar. A distância entre eles valia duas ou três publicações num teste com 7 positivos. Ranking frágil é ranking frágil.

## O que vem por aí

* Revisões e resumos organizados por aula
* Mais exercícios conforme a matéria avançar
* Materiais de apoio que eu achar úteis ao longo do semestre

Volte aqui com frequência: o repositório cresce semana a semana.

## Dúvidas e contato

Se travar em algo, se achar um erro no material ou se quiser sugerir um tema para eu cobrir, é só chamar:

**Erik Rolin**
Monitor de Extração e Análise de Dados
WhatsApp: (21) 99202 5739

Monitoria existe para ser usada. Não fique com a dúvida guardada até a véspera da prova.

**NINGUÉM VAI REPROVAR NO MEU PLANTÃO!**
