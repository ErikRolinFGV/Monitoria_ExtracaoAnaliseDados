# Monitoria de Extração e Análise de Dados

Bem-vindos! Este repositório é o ponto de apoio da monitoria de Extração e Análise de Dados da FGV Comunicação.

*Atualizado em 17/09/2026.*

## Quem sou eu

Me chamo **Erik Rolin**, sou aluno de Comunicação Digital na FGV e monitor da disciplina de Extração e Análise de Dados. A ideia aqui é simples: juntar em um só lugar tudo que possa facilitar a vida de vocês na matéria, desde o básico até as partes que costumam travar todo mundo.

## O que já está no ar

| Arquivo | O que é |
|---|---|
| `resolucao_simulado.ipynb` | Resolução comentada das 8 questões do simulado do Festival ViraBairro, com o código, as saídas reais e a resposta escrita de cada questão |
| `exercicios/Exercicios_Extras.ipynb` | 10 exercícios de treino no mesmo caso, com célula em branco para você resolver e gabarito recolhido |
| `exercicios/dados/` | Os dois CSVs que os exercícios usam |

## Comece por aqui

A ordem que eu recomendo é essa, e ela importa:

1. **Leia a resolução do simulado** (`resolucao_simulado.ipynb`). Em cada questão, pare no bloco *O que a questão pede* e tente escrever o código antes de olhar a célula de baixo. Depois compare.
2. **Faça os exercícios extras** (`exercicios/Exercicios_Extras.ipynb`), com o gabarito fechado. Eles não são a mesma prova de novo: mudei fórmula, mudei o corte, mudei o trio de modelos, e em vários casos o resultado é o **oposto** do simulado. Isso é de propósito. Se você decorou "a logística sempre ganha", o exercício 8 vai te pegar.
3. **Refaça o exercício 10 cronometrado**, com o caderno fechado. Saber fazer e saber fazer em 35 minutos são coisas diferentes.

E escreva os campos de interpretação **sempre**, mesmo quando o código não sair. Metade da nota está no texto em Markdown, e é justamente a metade que quase ninguém treina.

## Sobre os dados

Duas coisas para não gerar confusão:

* **A resolução do simulado é para ler, não para rodar.** O professor não distribui os CSVs do caso antes da prova, então eu rodei tudo na própria plataforma dele e deixei as saídas gravadas no notebook. Os números que você vê ali são os verdadeiros, direto da tela. Só não tem como reexecutar as células aqui fora.
* **Os exercícios extras rodam.** As bases em `exercicios/dados/` foram construídas por mim a partir do dicionário do caso. Não são os arquivos da prova, mas têm os mesmos nomes de coluna, as mesmas unidades e a mesma escala: 120 publicações na base de análise, 36 na bruta, quatro temas e três formatos.

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
4. Jogar `dayfirst=True` numa coluna com formatos de data misturados. Isso não dá erro, dá resposta errada em silêncio. Confira `.min()` e `.max()` depois de toda conversão de data.
5. Gráfico sem título, sem nome de eixo ou sem a fonte. São itens explícitos do enunciado, e cada um é ponto.
6. Responder o campo de Markdown em uma frase genérica, ou deixar em branco.

## A parte que separa a nota boa da nota mediana

A base é pequena, e quase toda diferença entre categorias está dentro do ruído. Antes de recomendar qualquer coisa a partir de um número, faça duas perguntas a ele:

**Quantos casos tem por trás desse número?** Uma mediana calculada sobre 8 publicações não é uma medida, é uma curiosidade.

**Qual é a distância para o segundo colocado?** Se for menor do que o deslocamento que uma única publicação atípica causaria, você não tem um vencedor, tem um empate.

A resposta preguiçosa aponta a barra mais alta. A resposta que ganha nota percebe o empate, diz isso com todas as letras, e mesmo assim entrega uma decisão utilizável. O enunciado repete em quase toda questão as palavras "limitação", "não afirme causalidade", "sem afirmar tendência". Ele está pedindo ceticismo, não ranking.

## Como usar os arquivos

Para clonar:

```bash
git clone <url-do-repositorio>
```

Se preferir, dá para baixar o zip direto pelo botão verde **Code** aqui em cima. Os notebooks abrem no Jupyter, no VS Code ou no Google Colab. Se for pelo Colab, lembre de subir também a pasta `exercicios/dados/`, senão o `read_csv` não acha os arquivos.

Uma observação sobre a prova: vocês podem levar um repositório próprio para consulta. Vale a pena clonar este e ir anotando as suas próprias coisas nele ao longo das semanas, porque material que você mesmo organizou você acha em dez segundos, e material que você baixou na véspera você não acha nunca.

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
