# O básico: rumo a uma árvore pronta para publicação

Esta vinheta percorre os principais passos para editar uma árvore no tree2go, desde abrir um conjunto de árvores até exportar a figura final. Ela cobre a maioria das opções básicas para personalizar uma árvore e transformá-la em uma figura pronta para publicação. Funções mais específicas são tratadas em outras vinhetas.

Estes tutoriais curtos não pretendem explicar cada menu em detalhe, mas sim dar uma visão rápida das opções disponíveis. Para informações mais detalhadas, consulte o [guia de referência das opções](https://vr-daniel.github.io/tree2go/#reference).

Como exemplo, usamos um conjunto de dados simulado que inclui tudo o que é necessário para mostrar a maior parte do que o tree2go pode fazer. Ele tem 31 espécies de vertebrados: 24 vivas e 7 fósseis. Embora o exemplo use nomes de espécies reais, e seus valores tenham sido escolhidos para parecer razoáveis do ponto de vista biológico, todos os dados são fictícios. **Qualquer padrão ou conclusão obtidos a partir destes dados não tem significado biológico.**

## 1. Os arquivos de que precisamos

Árvores e redes filogenéticas vêm de muitos programas e métodos diferentes, e em muitas variantes. Para este tutorial, preparamos um conjunto de arquivos prontos para usar, agrupados em pastas que seguem as seções do painel esquerdo do tree2go. Eles cobrem muitos dos tipos e formatos de arquivo que você pode encontrar em análises filogenéticas, então também podem servir de referência mais adiante, quando você importar seus próprios dados. Os arquivos podem ser baixados [neste link](https://github.com/VR-Daniel/tree2go/tree/main/content/examples), e são os seguintes:

```text
vertebrates/
├── Tree/
│   ├── vertebrates_ml.nwk                    Árvore de máxima verossimilhança (Newick), comprimentos de ramo em substituições por sítio
│   ├── vertebrates_mcc.tre                   Árvore MCC (NEXUS), comprimentos de ramo em tempo, com uma taxa morfológica fictícia
│   └── vertebrates_posterior.trees           10.001 árvores calibradas no tempo (NEXUS) de uma análise bayesiana
├── Clades/
│   └── clade_groups.txt                      Clados para destacar (um por linha), como Clade={sp1, sp2, …}
├── Phylogenetic networks/
│   └── heliconius_network.nwk                Rede de borboletas Heliconius (eNewick), com uma espécie híbrida e uma introgressão
├── Ancestral reconstructions/
│   └── vertebrates_habitat.simmap            100 mapas estocásticos de caracteres para o hábitat (formato SIMMAP, como escrito pelo phytools)
├── Attachments/
│   ├── regions.csv                           Presença (1) ou ausência (0) de cada espécie em diferentes regiões geográficas
│   ├── traits.csv                            Caracteres categóricos e contínuos de cada espécie
│   ├── vertebrates_traits_heatmap.csv        Cinco caracteres contínuos de cada espécie
│   └── vertebrates_alignment.fasta           Alinhamento de DNA de 100 pb das espécies vivas (FASTA)
├── Geography/
│   └── fossil_records.csv                    Registros de ocorrência dos locais de amostragem das espécies fósseis
└── Tanglegram/
    └── vertebrates_alternative.nwk           A mesma árvore com uma topologia alternativa (Newick)
```

## 2. Abrir uma árvore ou um conjunto de árvores

Clique em `Open tree` na seção **Tree** do painel esquerdo. O tree2go lê arquivos nos formatos NEXUS e Newick, qualquer que seja a extensão. Um arquivo com uma única árvore é desenhado imediatamente. Um arquivo com muitas árvores, como a amostra posterior de uma análise bayesiana, é lido como um **conjunto de árvores**.

Se o arquivo tiver mais de 10.000 árvores, uma janela se abre antes de lê-las (Fig. 1A), onde você pode escolher:

- *Burn-in*: a porcentagem das primeiras árvores a descartar.
- *Keep*: quantas árvores manter depois do burn-in, como número ou como porcentagem.
- *Which trees*: se as árvores mantidas são espaçadas uniformemente ou escolhidas ao acaso (com uma semente, para que a mesma amostra possa ser obtida de novo).

A mesma janela se abre quando você escolhe vários arquivos de árvores de uma vez, como os arquivos `.t` das corridas de uma análise do MrBayes. Nesse caso, o tree2go os lê como um único conjunto de árvores, o burn-in é aplicado a cada corrida, o mesmo número de árvores é mantido de cada uma, e as árvores mantidas são combinadas. Depois, na seção **Tree**, você pode escolher quais corridas usar (*Runs used*) e ver o quanto elas concordam (ASDSF).

O tree2go também verifica a estrutura das anotações das árvores ao ler um arquivo. Quando chaves ou colchetes não estão pareados, o que pode acontecer quando um arquivo passa por vários programas, o app detecta isso na maioria dos casos e oferece repará-lo (Fig. 1B). É um problema real que costuma passar despercebido, já que o arquivo abre mesmo assim, mas que prejudica silenciosamente os cálculos e gráficos que dependem dessas anotações. O tree2go repara apenas a estrutura das anotações, ele não pode recuperar valores que outros programas perderam ou alteraram.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig01-window.png" alt="A janela exibida antes de ler um arquivo com mais de 10.000 árvores, com campos para o burn-in, o número de árvores a manter e como escolhê-las"><figcaption><b>Figura 1A.</b> A janela exibida antes de ler um arquivo com mais de 10.000 árvores, com um burn-in e o número de árvores a manter.</figcaption></figure>
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig01-repair.png" alt="A janela que avisa sobre anotações cujas chaves não estão pareadas, mostra onde, e oferece carregar o arquivo com o reparo"><figcaption><b>Figura 1B.</b> A janela exibida ao abrir um arquivo cujas anotações têm chaves sem par.</figcaption></figure>
  </div>
</figure>

Para este tutorial, vamos abrir `vertebrates_posterior.trees`, que contém 10.001 árvores. Na janela, definimos um burn-in de `10`% e mantemos as 9.001 árvores que restam depois dele (Fig. 1A).

> **Nota.** Quanto mais árvores um arquivo tem, mais memória ele precisa. O tree2go não tem um limite próprio além da memória que o navegador dá a cada aba, mas amostras muito grandes deixam o app mais lento, dependendo do número de terminais e das anotações de cada árvore. Como regra geral, uma amostra de 10.000 árvores é mais do que suficiente para árvores-resumo.

## 3. Resumir as árvores

Depois que as árvores são lidas, a seção **Tree** mostra quantas foram mantidas (Fig. 2). A partir dali, você pode mostrar qualquer árvore do conjunto, ou construir uma árvore-resumo: um consenso (estrito, de maioria ou de máxima compatibilidade), uma árvore de máxima credibilidade de clados (MCC) ou uma árvore de máximo a posteriori (MAP). A árvore MAP também precisa do arquivo `.p` do MrBayes ou do arquivo `.log` do BEAST2, anexados em **Attachments**.

Aqui construímos uma árvore MCC, que deve ser quase idêntica à de `vertebrates_mcc.tre`. Como já descartamos 10% das árvores ao ler o arquivo, deixamos o *Burn-in* desta seção em `0`. E como as árvores são calibradas no tempo, definimos *Node ages* como `Median`, para que cada nó receba a mediana de suas idades na amostra. Depois clicamos em `Build summary tree`.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig02-panel.png" alt="A seção Tree com um conjunto de árvores carregado, Maximum clade credibility escolhida como árvore-resumo e Median como idades dos nós">
  <figcaption><b>Figura 2.</b> A seção Tree, construindo uma árvore MCC com as idades medianas dos nós a partir da amostra de árvores.</figcaption>
</figure>

A seção **Tree** também tem uma subseção **Reading properties**, com duas opções que tornam mais leve o trabalho com arquivos grandes. Ambas se aplicam ao próximo arquivo que você abrir:

- *Significant digits of branch lengths* (de 1 a 10): menos dígitos usam menos memória, mas podem arredondar ramos muito curtos.
- *Keep the trees in a compact binary form*: mantém na memória uma cópia mais leve de cada árvore. Quando está desativada, as árvores são mantidas como texto, o que deixa o app mais lento com arquivos muito grandes.

## 4. Organizar a árvore

A seção **Layout** muda a forma da árvore e seu tamanho. Como regra geral, cada opção do painel esquerdo muda a árvore inteira de uma vez, enquanto um `Right-click` em qualquer elemento da tela muda apenas esse elemento (ou os elementos selecionados).

Aqui definimos **Layout** > *Order nodes* como `Decreasing`, para que os clados maiores fiquem embaixo, e damos à raiz um ramo curto de `25` px com **Layout** > *Root branch*, que marca onde a árvore começa (Fig. 3A–B). Ambas são escolhas puramente estéticas. Fique à vontade para experimentar as outras formas e opções. Todos os elementos da tela se adaptam a essas mudanças.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig03-panel.png" alt="A seção Layout, com Order nodes em Decreasing e um ramo de raiz de 25 px"><figcaption><b>Figura 3A.</b> Opções de Layout.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig03-canvas.png" alt="A árvore com seus clados ordenados por tamanho e um ramo de raiz curto"><figcaption><b>Figura 3B.</b> A árvore MCC, com seus clados ordenados por tamanho e um ramo de raiz curto.</figcaption></figure>
  </div>
</figure>

Embora não a usemos na figura final, a seção **Tree cloud** desenha todas as árvores do conjunto sobrepostas, como faz o DensiTree (Fig. 4), para mostrar a incerteza na topologia e nas idades. Ela está disponível apenas para conjuntos de árvores.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig04-cloud.png" alt="As árvores da amostra desenhadas umas sobre as outras atrás da árvore MCC">
  <figcaption><b>Figura 4.</b> As árvores da amostra desenhadas como uma nuvem de árvores.</figcaption>
</figure>

> **Nota.** Você pode personalizar a aparência da nuvem de árvores: espessura da linha, cor, opacidade, quantas árvores são desenhadas e como são escolhidas. Como desenhar muitas árvores pode deixar o app mais lento, recomendamos desativar **Tree cloud** > *Show the trees of the sample* enquanto você continua editando, e reativá-la antes de exportar. O tree2go lembra suas escolhas nesta seção.

## 5. Ramos

A seção **Branches** define a aparência de todos os ramos. Em árvores com espécies vivas e extintas, os ramos dos terminais extintos são tracejados por padrão, e seus nomes levam uma adaga (†). Para mudar isso apenas em alguns ramos, selecione-os com `Shift` + clique e mude sua aparência pelo menu de `Right-click`. Em árvores apenas de espécies extintas, ou em árvores não calibradas no tempo, todos os ramos são contínuos por padrão.

As subseções **Color by data** e **Width by data** colorem os ramos, ou mudam sua espessura, de acordo com qualquer valor da árvore (Fig. 5A), suas próprias anotações ou uma tabela anexada na seção **Attachments**. As cores podem ser escolhidas uma a uma (`Custom colors`) ou tiradas de uma paleta, várias das quais são seguras para daltonismo.

No nosso exemplo, definimos **Branches** > *Line width* como `1.5` px e, em **Color by data**, colorimos os ramos por `rate_median`, que aqui representa uma taxa de evolução morfológica de uma análise bayesiana, com a paleta `Magma` (Fig. 5B).

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig05-panel.png" alt="A subseção Color by data, colorindo os ramos por rate_median com a paleta Magma"><figcaption><b>Figura 5A.</b> Opções de Color by data.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig05-canvas.png" alt="A árvore com seus ramos coloridos do escuro ao claro de acordo com sua taxa evolutiva"><figcaption><b>Figura 5B.</b> Ramos coloridos de acordo com sua taxa evolutiva com uma paleta segura para daltonismo.</figcaption></figure>
  </div>
</figure>

> **Nota.** A paleta de toda a sessão é definida em `Page settings`, no cabeçalho. Ela muda as cores oferecidas a partir de então, mas não as que já foram dadas aos elementos. O mesmo menu tem `Page settings` > *Color blind preview*, que mostra a figura como seria vista com diferentes deficiências na visão de cores. Ela muda apenas o que você vê na tela, a figura mantém suas cores quando você volta à visão normal ou a exporta.

## 6. Valores, nós e sua incerteza

A seção **Branch values** escreve em cada ramo qualquer valor da árvore ou de uma tabela anexada, e define sua aparência: posição, alinhamento, tamanho, cor e número de casas decimais.

A seção **Nodes** adiciona símbolos aos nós internos e aos terminais, com a mesma aparência para todos ou com uma aparência definida por um valor da árvore ou de uma tabela anexada.

A seção **Node values** reúne os valores que costumam ser mostrados nos nós:

- **Support values**: como números ou como símbolos, cuja cor ou tamanho muda com o valor. Para manter a figura limpa, você pode mostrar apenas os valores dentro de um intervalo que escolher.
- **Other node labels**: qualquer outro valor da árvore ou de uma tabela anexada, com várias formas de alinhá-lo.
- **Node bars**: em árvores calibradas no tempo com incerteza nas idades, como a nossa árvore MCC, a incerteza de cada nó pode ser desenhada como uma barra HPD ou como um violino (*Show the ages as*). Sua aparência, tamanho e cor podem ser mudados como os de qualquer outro elemento.

No nosso exemplo, primeiro mostramos os **Support values** como números, deixando todas as outras opções como estão. Depois, em **Other node labels**, mostramos (*Show*) `Age, median of the trees` como número, e definimos *Stack with the support values* como `Below the branch` (Fig. 6A). Fique à vontade para explorar outras opções que se ajustem ao objetivo visual que você quer alcançar.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig06-panel.png" alt="A seção Node values, com os valores de suporte como números e as idades medianas dos nós empilhadas abaixo do ramo"><figcaption><b>Figura 6A.</b> Valores de suporte e idades dos nós na seção Node values.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig06-canvas.png" alt="A árvore com o valor de suporte acima de cada nó e sua idade mediana abaixo do ramo, com um círculo vermelho ao redor de valores que se sobrepõem"><figcaption><b>Figura 6B.</b> A idade de cada nó mostrada como um segundo valor, abaixo do seu suporte.</figcaption></figure>
  </div>
</figure>

Em muitos casos, especialmente em clados grandes com ramos curtos, alguns valores acabam uns sobre os outros (círculo vermelho na Fig. 6B). Há várias maneiras de contornar isso. Uma é mover separadamente cada rótulo sobreposto, mudando seu deslocamento pelo menu de `Right-click`. Outra, que seguimos aqui, é substituir os números por símbolos cujo tamanho e cor deem uma pista visual do seu valor.

Para isso, ocultamos novamente as idades dos nós e mudamos os valores de suporte de `Number` para `Circles`. Depois, em *Which values*, escolhemos `By categories`, com três intervalos: preto para suportes abaixo de 80, azul de 80 a 95, e vermelho acima de 95. Também mantemos um tamanho de círculo diferente para cada intervalo (Fig. 7A–B).

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig07-panel.png" alt="A subseção Support values, mostrando os suportes como círculos em três intervalos, cada um com sua cor e tamanho"><figcaption><b>Figura 7A.</b> Valores de suporte mostrados como símbolos, por categorias.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig07-canvas.png" alt="A árvore com um círculo preto, azul ou vermelho em cada nó de acordo com seu suporte"><figcaption><b>Figura 7B.</b> A árvore com seus valores de suporte mostrados como símbolos.</figcaption></figure>
  </div>
</figure>

Em seguida, como nossa árvore vem de uma amostra de árvores, podemos mostrar a incerteza nas idades dos nós. Alguns programas a escrevem nas anotações de uma única árvore, como um intervalo HPD de 95%, que pode ser desenhado como uma barra. Como temos a amostra inteira, podemos ir um passo além e mostrar como as idades se distribuem dentro desse intervalo, como gráficos de violino, pela subseção **Node bars** (Fig. 8A–B). Como qualquer outro elemento do app, os gráficos de violino podem ser totalmente personalizados em tamanho e cor, e também podem mostrar outros valores, como a média e a mediana.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig08-panel.png" alt="A subseção Node bars, com as idades mostradas como violinos"><figcaption><b>Figura 8A.</b> A subseção Node bars, onde as idades podem ser mostradas como uma barra HPD ou como densidades.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig08-canvas.png" alt="A árvore com um gráfico de violino em cada nó mostrando a distribuição de sua idade"><figcaption><b>Figura 8B.</b> A árvore com gráficos de violino em seus nós, mostrando a incerteza das idades na amostra.</figcaption></figure>
  </div>
</figure>

> **Nota.** Em árvores datadas, a mediana das barras HPD e dos gráficos de violino deve ficar sobre os nós. O tree2go reconhece, a partir das próprias árvores, se seus comprimentos de ramo estão em tempo. Em algumas árvores, porém, a estrutura é ambígua, e árvores datadas podem ser lidas como não datadas, o que deixa as medianas das distribuições fora de seus nós. Se isso acontecer, indique ao app que as árvores são datadas com **Tree** > *Trees in time*.

## 7. Nomes dos terminais

A seção **Tip labels** define a aparência e a posição dos nomes dos terminais. Aqui ativamos *Align labels to the right*, para que todos os nomes terminem em uma mesma coluna (Fig. 9A–B). Isso é especialmente útil em árvores cujos terminais não chegam todos ao presente, como árvores com fósseis, ou em árvores com comprimentos de ramo em substituições por sítio.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig08-canvas.png" alt="A árvore com os nomes de seus terminais fósseis junto ao fim de seus ramos"><figcaption><b>Figura 9A.</b> Nomes dos terminais sem alinhar.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig09-canvas.png" alt="A árvore com todos os nomes dos terminais alinhados em uma coluna, com os terminais fósseis destacados em amarelo"><figcaption><b>Figura 9B.</b> Nomes dos terminais alinhados em uma coluna, com os terminais fósseis destacados em amarelo para que a mudança seja mais fácil de ver.</figcaption></figure>
  </div>
</figure>

Como mencionado antes, o tree2go reconhece automaticamente o tipo de árvore, e com ele os ramos que pertencem a fósseis. Mas, olhando com mais atenção o nosso exemplo, vemos que *Mammuthus primigenius* (mamute-lanoso) e *Smilodon fatalis* (tigre-dente-de-sabre) não têm nem o ramo tracejado nem a adaga que os marca como fósseis. Isso não é um erro, mas uma questão da escala da árvore.

Para distinguir fósseis de espécies vivas, o tree2go admite uma pequena tolerância, terminais que acabam a menos de 0,5% da altura da árvore em relação ao presente ainda contam como vivos, para que o arredondamento dos comprimentos de ramo não transforme espécies vivas em fósseis. Em uma árvore que abrange mais de 450 milhões de anos, como a nossa, esses 0,5% equivalem a mais de dois milhões de anos, e ambas as espécies se extinguiram há apenas cerca de 12.000 anos. A solução é simples, reduzimos **Fossils** > *Tolerance (% of the tree height)* a um valor muito pequeno, como `0.001` (Fig. 10A–B).

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig10-panel.png" alt="A seção Fossils, com a tolerância reduzida a 0.001%"><figcaption><b>Figura 10A.</b> A seção Fossils e suas opções.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig10-canvas.png" alt="Os terminais do mamute-lanoso e do tigre-dente-de-sabre desenhados como fósseis, com ramos tracejados e uma adaga"><figcaption><b>Figura 10B.</b> Os terminais fósseis depois de reduzir a tolerância.</figcaption></figure>
  </div>
</figure>

> **Nota.** Como qualquer outro elemento, os nomes dos terminais podem ser editados um a um pelo menu de `Right-click`, ou vários de uma vez depois de selecioná-los com `Shift` + clique. Renomear um terminal muda apenas o nome exibido. O nome original continua por baixo, então o terminal mantém seu vínculo com os dados anexados. Quando alguns terminais foram renomeados e a árvore é exportada como NEXUS ou Newick, o tree2go pergunta se deve escrever os nomes novos, como aparecem na figura, ou os originais.

## 8. Clados

A seção **Clades** destaca e nomeia clados, e define a aparência de seus destaques e de suas barras de nome. Os clados podem ser escolhidos diretamente na tela, usando `Select mode` no cabeçalho:

- `Element` seleciona um nó ou um ramo.
- `Clade` seleciona um nó com todos os seus descendentes.

Destaques e nomes se aplicam à seleção, e podem cobrir o clado inteiro, apenas suas linhagens vivas (coroa) ou apenas as extintas (tronco). Um destaque pode ser um bloco de cor sólida ou um degradê, da esquerda para a direita ou da direita para a esquerda.

Se você já sabe quais terminais pertencem a cada grupo, também pode escrever um arquivo de texto simples, como `clade_groups.txt`, com um clado por linha no formato `Clade={sp1, sp2, …}`. Cada clado precisa de pelo menos dois terminais, escritos como aparecem na árvore. Com `Highlight clades from a file…` ou `Name clades from a file…`, o tree2go encontra o ancestral comum mais recente dos terminais de cada clado, e destaca ou nomeia esse clado para você (Fig. 11A).

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig11-canvas.png" alt="A árvore retangular com vários clados principais destacados e nomeados a partir de um arquivo"><figcaption><b>Figura 11A.</b> A árvore com alguns de seus clados principais destacados a partir de um arquivo.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig11-canvas_fan.png" alt="A mesma árvore desenhada em leque, com os mesmos clados destacados e nomeados"><figcaption><b>Figura 11B.</b> A mesma árvore, com seus clados destacados, em forma de leque.</figcaption></figure>
  </div>
</figure>

Todas as mudanças são mantidas quando a forma da árvore muda (retangular, circular, em leque ou sem raiz), a menos que não possam ser desenhadas na nova forma, como um alinhamento de sequências em uma árvore circular. Além disso, embora o app tenha sido pensado para se adaptar a todas as formas, alguns elementos que podem passar de uma forma para outra não são práticos em todas. Por exemplo, gráficos de violino em uma árvore circular ou em leque se sobrepõem em direção à raiz (Fig. 11B).

## 9. Legendas e posicionamento de elementos

À medida que adicionamos elementos com cores, símbolos ou tamanhos, o tree2go adiciona suas legendas no canto inferior esquerdo da figura. Cada legenda pode ser movida, mudar de estilo e ser ocultada pelo seu menu de `Right-click` ou pela seção **Legends**. Por padrão, as legendas ficam fixas no lugar, como indica o cadeado azul no canto superior direito. Um clique no cadeado o deixa amarelo e libera a legenda, que então pode ser arrastada para qualquer lugar da tela, como imagens e gráficos.

Enquanto um elemento é movido, guias pontilhadas mostram os outros elementos ao seu redor, cada um com sua distância (Fig. 12). Clique na bolha azul de uma distância para digitar um valor exato, e o elemento se move para lá.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig12-canvas.png" alt="Uma legenda sendo movida, com guias pontilhadas e bolhas azuis com as distâncias até os elementos ao seu redor">
  <figcaption><b>Figura 12.</b> Movendo uma legenda livremente, com as guias e as distâncias até os elementos ao seu redor.</figcaption>
</figure>

## 10. Eixo do tempo e escala geológica

Em árvores calibradas no tempo, `Show time axis` na seção **Time axis** adiciona um eixo de idades abaixo da árvore, ou acima dela com *Position*. Suas subseções definem o eixo:

- **Ages**: entre outras opções, um deslocamento para árvores apenas de fósseis, nas quais nenhuma espécie chega ao presente. Quando esse valor muda, todos os rótulos que mostram uma idade são atualizados automaticamente.
- **Ticks** e **Axis look**: onde ficam as marcas e qual a aparência do eixo.
- **Geologic time scale**: caixas com os intervalos geológicos, nas cores da Geological Society of America (GSA Geologic Time Scale v. 6.0), e fundos que sombreiam esses intervalos, ou intervalos próprios, atrás da árvore (Fig. 13).

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig13-canvas.png" alt="A árvore com um eixo do tempo e as caixas da escala geológica abaixo dela">
  <figcaption><b>Figura 13.</b> Um eixo do tempo com a escala geológica abaixo da árvore.</figcaption>
</figure>

> **Nota.** Como nos outros elementos da figura, quase toda a aparência do eixo do tempo e da escala geológica pode ser personalizada. A única exceção são as cores das caixas geológicas, que seguem uma convenção internacional. Você também pode adicionar um segundo eixo do tempo com uma escala diferente (**Time axis** > *Show a second axis*), e sombrear intervalos atrás da árvore, sejam intervalos geológicos padrão ou intervalos que você definir. O eixo do tempo também funciona em árvores circulares e em leque, como anéis concêntricos, mas as caixas geológicas não são desenhadas ali, porque não se encaixam em uma forma radial.

## 11. Dividir uma árvore longa em páginas

Uma árvore alta demais para uma página impressa pode ser dividida pela seção **Split into pages**. O tree2go encontra os clados que vão em cada página, para o número de páginas que você escolher, e mostra os limites de cada página na tela como caixas tracejadas (Fig. 14). Para mover um limite, arraste-o.

Cada página tem a mesma largura, e pode ter seu próprio eixo do tempo ou escala geológica. Uma miniatura da árvore inteira (o mapa da árvore) mostra, em cada página, onde seus clados estão na árvore. Sua posição, cores e destaque são definidos pelo seu menu de `Right-click`. Ao exportar, você pode salvar a árvore inteira em um arquivo, ou cada página como um arquivo próprio.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig14-canvas.png" alt="Uma árvore dividida em páginas, cada página com uma miniatura da árvore inteira">
  <figcaption><b>Figura 14.</b> Uma árvore dividida em páginas, cada uma com uma miniatura da árvore inteira.</figcaption>
</figure>

> **Nota.** Quando uma figura com um eixo do tempo ou uma escala geológica é dividida em páginas, você pode repetir o eixo abaixo de cada página ou mostrá-lo apenas na última, com **Split into pages** > *Repeat the time axis under each page*, na sua subseção **Look**. A mudança não aparece na tela, apenas nos arquivos exportados.

## 12. Gráficos de pizza nos nós

Às vezes temos, para cada nó, uma estimativa feita de proporções, como as probabilidades dos estados em uma reconstrução de estados ancestrais. O tree2go pode desenhá-las como gráficos de pizza nos nós, para um ou vários caracteres, e colorir os ramos de acordo com seus estados mais prováveis.

Para manter nossa árvore estilizada como está, primeiro a copiamos para uma nova aba e começamos a cópia com a aparência padrão. Faça `Right-click` na raiz da árvore e escolha `Copy tree to a new tab` (Fig. 15). Uma janela pergunta então se a cópia mantém a mesma aparência ou começa com a aparência padrão, e aqui escolhemos `Default look`. Para reiniciar, em vez disso, a aparência da aba atual, use `Reset styles` em `Page settings`. Se você fizer `Right-click` em qualquer outro nó em vez da raiz, `Extract clade` abre apenas esse clado em uma nova aba.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig15-panel.png" alt="O menu de clique direito da raiz com Copy tree to a new tab, e a janela que pergunta se a cópia mantém a mesma aparência ou começa com a aparência padrão">
  <figcaption><b>Figura 15.</b> Copiando a árvore para uma nova aba.</figcaption>
</figure>

Para renomear a nova aba, clique duas vezes no seu nome. Depois, na seção **Attachments**, clique em `Add file` e escolha `vertebrates_habitat.simmap`. Os nós da árvore se transformam imediatamente em gráficos de pizza. Sua aparência é definida na seção **Ancestral reconstructions** (Fig. 16A), onde os ramos também podem ser coloridos por estado com **Ancestral reconstructions** > *Color the branches*, pelo estado de máximo a posteriori, pelos estados mais prováveis acima de um limiar, ou como um degradê de probabilidade. Como as pizzas ocupam o lugar dos pontos dos nós, seu tamanho e sua borda são definidos na seção **Nodes**, como os de qualquer outro ponto.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig16-panel.png" alt="A seção Ancestral reconstructions, com pizzas nos nós e os ramos coloridos de acordo com seus estados mais prováveis"><figcaption><b>Figura 16A.</b> A seção Ancestral reconstructions.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig16-canvas.png" alt="A árvore copiada com um gráfico de pizza do hábitat em cada nó e seus ramos coloridos por estado, com um trecho incerto desenhado tracejado dentro de um círculo vermelho"><figcaption><b>Figura 16B.</b> Gráficos de pizza do hábitat nos nós, e ramos coloridos de acordo com seus estados mais prováveis.</figcaption></figure>
  </div>
</figure>

Para este exemplo, definimos **Nodes** > *Node dot size* como `9` px e **Branches** > *Line width* como `3` px, demos às pizzas uma borda preta, movemos a legenda e renomeamos seus estados pelo seu menu de `Right-click`. Também colorimos os ramos com `Most probable states (threshold-based)`. Essa opção define o quanto um estado precisa ser dominante para colorir um trecho de ramo, de modo que os trechos em que o estado é incerto se destacam como uma linha tracejada (círculo vermelho na Fig. 16B).

> **Nota.** Os gráficos de pizza também podem vir de um arquivo, com `Pie charts from a file…` na subseção **Pie charts** de **Node values**. O arquivo pode ser uma tabela com os nomes na primeira coluna e uma coluna por categoria, com a proporção de cada uma, ou um arquivo de texto simples com uma linha por terminal ou nó, como `Name | {A:0.3, B:0.7}`, a notação dos arquivos SIMMAP. Os nós internos são associados pelos seus nomes, então a árvore precisa ter nomes nos nós internos, escritos como no arquivo.

## 13. Gráficos laterais

Uma das funções mais úteis do tree2go é desenhar gráficos ao lado dos terminais: gráficos de barras, matrizes de categorias (como presença e ausência), mapas de calor de valores contínuos, e até alinhamentos de DNA.

Primeiro, na seção **Attachments**, clique em `Add file` e escolha `regions.csv`, `traits.csv`, `vertebrates_traits_heatmap.csv` e `vertebrates_alignment.fasta`, que podem ser escolhidos juntos (Fig. 17A). Como descrito no começo deste tutorial, esses arquivos contêm a distribuição geográfica das espécies, alguns de seus caracteres, e sequências de DNA das espécies vivas. As tabelas são simples: uma coluna com os nomes dos terminais, e uma coluna para cada valor. Você pode criá-las em qualquer programa de planilhas, como o Excel, e salvá-las como `.csv`. O tree2go encontra sozinho a coluna com os nomes dos terminais, e você pode escolher outra na sua lista *Names in* em **Attachments**, se precisar.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig17-attachments.png" alt="A seção Attachments com o SIMMAP, o alinhamento e três tabelas carregadas, cada uma com o número de terminais com que coincide"><figcaption><b>Figura 17A.</b> Os arquivos anexados, cada um com o número de terminais da árvore com que coincide.</figcaption></figure>
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig17-sideplots.png" alt="A lista no topo da seção Side plots, com os gráficos na sua ordem dos terminais para fora e um ícone de olho para cada um"><figcaption><b>Figura 17B.</b> A seção Side plots, com os gráficos na sua ordem dos terminais para fora.</figcaption></figure>
  </div>
</figure>

Cada arquivo anexado aparece na seção **Attachments**, com o número de terminais da árvore com que coincide. Aqui, a distribuição geográfica (`regions.csv`) e os caracteres (`traits.csv` e `vertebrates_traits_heatmap.csv`) coincidem com 31 dos 31 terminais, enquanto o alinhamento coincide com apenas 24, o que faz sentido, já que os 7 fósseis não têm DNA.

Os gráficos laterais podem ser empilhados. Vários podem ser mostrados ao mesmo tempo, e sua ordem, dos terminais para fora, é mudada arrastando-os na lista no topo da seção **Side plots**, onde o ícone de olho mostra ou oculta cada um (Fig. 17B). A aparência de cada gráfico é definida na sua subseção de **Side plots**, e alguns elementos também podem ser mudados um a um pelo menu de `Right-click`. Alguns gráficos também podem seguir a aparência da árvore, por exemplo colorindo as barras de acordo com o clado nomeado a que cada terminal pertence (**Side plots** > *Color the bars by named clade*).

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig18-canvas.png" alt="A árvore com barras de massa cerebral em escala logarítmica ao lado das espécies vivas, e um mapa de calor de cinco caracteres contínuos">
  <figcaption><b>Figura 18.</b> Barras de massa cerebral em escala logarítmica, e um mapa de calor de cinco caracteres contínuos.</figcaption>
</figure>

Neste exemplo, desenhamos barras de massa cerebral (`brain_g`, de `traits.csv`), coloridas de acordo com o clado nomeado de cada terminal, e em escala logarítmica (**Side plots** > *Logarithmic scale (log₁₀)*), já que a massa cerebral vai de uma fração de grama a vários quilos. Ao lado delas, desenhamos um mapa de calor de cinco caracteres contínuos (`vertebrates_traits_heatmap.csv`): massa corporal, longevidade máxima, tamanho do genoma, temperatura corporal e descendentes por ano. Observe que os gráficos laterais deixam um terminal vazio quando ele não tem valor. Aqui, os fósseis não têm barra, já que sua massa cerebral é desconhecida, e no mapa de calor mostram apenas sua massa corporal (Fig. 18).

Os gráficos laterais também podem mostrar sequências de DNA ou de proteínas, direto de um arquivo `.fasta`. Aqui usamos `vertebrates_alignment.fasta`. O tree2go dá a cada base sua própria cor, e as cores podem ser mudadas na subseção **Alignment** de **Side plots**.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig19-bases.png" alt="Os sítios 15 a 30 do alinhamento ao lado dos terminais, um quadrado colorido por base, com as letras dentro"><figcaption><b>Figura 19A.</b> Os sítios 15 a 30 do alinhamento, como um quadrado por base.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig19-barcode.png" alt="O alinhamento inteiro ao lado dos terminais como um código de barras, com cada sítio marcado onde difere da sua base mais comum"><figcaption><b>Figura 19B.</b> O alinhamento inteiro, como um código de barras.</figcaption></figure>
  </div>
</figure>

A forma como o alinhamento é desenhado depende de quantos sítios são mostrados. Quando cabem na largura do gráfico (**Side plots** > *Width*, em **Alignment**), cada base é desenhada como um quadrado colorido, com sua letra dentro quando há espaço (Fig. 19A). Quando não cabem, o alinhamento é desenhado como um código de barras, que marca em cada sítio, em duas cores contrastantes, as bases que diferem da mais comum (Fig. 19B). O tree2go calcula quantos sítios cabem, e a dica sob *Width* informa isso. Você também pode escolher quais sítios mostrar com *From site* e *To site*.

## 14. Presença e ausência em uma árvore circular

Deixamos os dados binários para o final porque, além de desenhá-los como os outros gráficos, vamos combiná-los com uma forma de árvore diferente. Para este exemplo, ocultamos as barras, o mapa de calor e o alinhamento com seus ícones de olho na lista de **Side plots**, e deixamos apenas **Categories**, com `regions.csv`. Como os outros gráficos, ele desenha uma grade de quadrados, coloridos onde uma espécie está presente e em cinza onde está ausente, e ambas as cores podem ser mudadas. Depois, em **Layout**, escolhemos a forma `Circular` e viramos a árvore do avesso com **Layout** > *Turn circular and fan trees inside out*. Para deixar a figura mais leve, também removemos os gráficos de violino e as idades dos nós, transformamos a árvore em um cladograma desmarcando **Layout** > *Use branch lengths*, e ampliamos o centro com **Layout** > *Inner radius (center gap)*. Por fim, com **Side plots** > *Squares follow the circle*, em **Categories**, os quadrados se transformam em cunhas que acompanham o círculo, e *Width of the bands* define sua largura (Fig. 20).

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig20-canvas.png" alt="Um cladograma circular virado do avesso, com a presença e a ausência de cada espécie em sete regiões desenhadas como anéis de cunhas coloridas dentro do círculo, e um espaço vazio no centro">
  <figcaption><b>Figura 20.</b> A árvore virada do avesso, com sua matriz de presença e ausência dentro do círculo.</figcaption>
</figure>

O resultado é uma vista especialmente útil em biogeografia, já que mostra de relance tanto as relações entre as espécies quanto sua presença e ausência em cada região. E o espaço que abrimos no centro vai levar nossa figura um passo além na próxima seção.

## 15. Geografia

Outra função marcante do tree2go é desenhar mapas com registros de ocorrência diretamente no app, sem precisar de um programa de SIG. Isso é feito na seção **Geography** do painel esquerdo (Fig. 21). Você pode carregar seus próprios mapas como shapefiles (`.shp`, ou compactados em um `.zip`), ou baixar contornos básicos do [Natural Earth](https://www.naturalearthdata.com) para mapas atuais, ou do [GPlates](https://www.gplates.org) para reconstruções paleogeográficas. Baixá-los requer conexão com a internet.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig21-panel.png" alt="A seção Geography, com suas subseções Map, Points e Lines to the tips">
  <figcaption><b>Figura 21.</b> A seção Geography.</figcaption>
</figure>

Para este exemplo, usamos `fossil_records.csv`, com os locais de amostragem dos sete fósseis da nossa árvore. O arquivo precisa, no mínimo, de uma coluna com os nomes dos terminais, que podem se repetir quando uma espécie tem vários registros, e de uma coluna para a longitude e outra para a latitude. Quando os registros são muitos, o tree2go pode agrupar os mais próximos. Como nossos fósseis abrangem um longo período de tempo, mostramos os registros como locais de amostragem atuais. Com o GPlates, as coordenadas podem, em vez disso, ser colocadas sobre uma reconstrução paleogeográfica, a partir de vários modelos, o que também requer conexão com a internet. Isso é mais útil quando os fósseis têm idades semelhantes e queremos mostrar como era sua distribuição naquele momento.

Primeiro, na subseção **Map**, baixamos os contornos `Land` do Natural Earth em `1:110 million`, e definimos **Geography** > *Projection (maps in degrees)* como `Mollweide (ESRI:54009)`, que dá ao mapa uma forma oval. A melhor projeção depende dos seus dados e do que você quer mostrar. Depois movemos o mapa para o centro do círculo, o espaço que abrimos na seção anterior. Como os outros elementos, o mapa tem seu próprio menu de `Right-click`, que muda não só sua aparência, mas também sua extensão e seu zoom. Diretamente no mapa, `Ctrl` + arrastar move a vista dentro do seu quadro, e `Ctrl` + rolagem aproxima e afasta, como em um SIG.

Em seguida, com `fossil_records.csv` anexado em **Attachments**, nós o escolhemos em **Geography** > *Table*, na subseção **Points**, e os registros aparecem no mapa. Com *Size* em `By the number of records`, cada ponto cresce com o número de registros do seu local. O tamanho e a cor dos pontos também podem seguir um valor da árvore ou de uma tabela anexada, e a cor pode seguir os clados nomeados ou, como aqui, o destaque de cada clado (`As the highlight of its clade`). As Figuras 22A e 22B mostram duas formas de incorporar dados geográficos a uma árvore.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig22-canvas.png" alt="A árvore circular virada do avesso com um mapa-múndi no centro, os registros fósseis como pontos coloridos de acordo com o destaque do seu clado, e os anéis de regiões entre o mapa e a árvore"><figcaption><b>Figura 22A.</b> A árvore com um mapa dos registros fósseis no centro. Os anéis internos mostram as regiões onde cada espécie vive ou foi encontrada, e os pontos do mapa estão coloridos de acordo com o destaque do seu clado.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig22-canvas_alternative.png" alt="Uma árvore com um mapa ao lado, mostrando os registros de ocorrência agrupados por proximidade geográfica e coloridos de acordo com os clados da árvore"><figcaption><b>Figura 22B.</b> Uma vista alternativa de um mapa dentro de uma filogenia. O mapa mostra os registros de ocorrência agrupados por proximidade geográfica e coloridos de acordo com os clados da árvore.</figcaption></figure>
  </div>
</figure>

> **Nota.** A subseção **Lines to the tips** liga cada terminal aos seus pontos (**Geography** > *Join each tip to its points*). Isso ajuda a mostrar de onde vêm as amostras ou as espécies, especialmente quando cada espécie tem um ou poucos registros próximos. Caso contrário, uma linha é desenhada do terminal até cada ponto.

## 16. Imagens e elementos visuais

A seção **Images and visual elements** adiciona seus próprios elementos à figura:

- `Add image`: uma imagem, como uma silhueta ou uma foto, em PNG ou JPEG.
- `Add label`: um texto livre, que pode ser alinhado com a árvore.
- `Draw arrow`: uma seta, que pode ser ancorada a nós e imagens, de modo que os acompanha quando a árvore muda.
- `Add density plot`: a distribuição de um valor da árvore, como as taxas.
- `Add LTT plot`: um gráfico de linhagens ao longo do tempo, para a árvore inteira ou para clados nomeados.

Como as legendas, eles podem ser movidos para qualquer lugar, com guias e distâncias até os elementos ao seu redor, e mudar de estilo pelo seu menu de `Right-click`.

## 17. Tanglegrama

Os tanglegramas são outra figura comum em filogenética comparada, duas árvores frente a frente, geralmente com topologias alternativas, com linhas que ligam seus terminais correspondentes. Na seção **Tanglegram**, a segunda árvore pode ser qualquer árvore do conjunto (`Open a tree of the set`) ou uma árvore de um arquivo (`Load a tree file in a new tab`). Aqui carregamos `vertebrates_alternative.nwk` (Fig. 23).

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig23-canvas.png" alt="A árvore principal e a árvore alternativa frente a frente, com linhas que ligam as mesmas espécies">
  <figcaption><b>Figura 23.</b> Um tanglegrama da árvore principal e de uma árvore com uma topologia alternativa.</figcaption>
</figure>

A segunda árvore se abre em uma aba própria, e é desenhada com a aparência dessa aba, o alinhamento dos nomes, as cores dos ramos e os destaques são definidos ali, como em qualquer outra árvore. Da árvore principal ela recebe apenas o tamanho, seus terminais se distribuem na mesma altura, e sua largura é a mesma, a menos que se defina outra em **Tanglegram** > *Width (0 as this tree)*. Com **Tanglegram** > *Join the highlights of the same clade*, os destaques de um clado nas duas árvores são ligados entre si. A ordem dos seus ramos é própria, e para que as linhas se cruzem o mínimo possível, a árvore principal oferece `Untangle (turn the second tree)`, que gira apenas os nós da segunda árvore, e `Untangle both`, que gira os nós das duas árvores.

## 18. Salvar e exportar

O tree2go guarda o seu trabalho de duas formas. Primeiro, enquanto os dados do navegador não forem apagados, o app lembra a sua sessão mesmo depois de fechado: na próxima vez que você abrir o tree2go, suas árvores, abas, aparência e arquivos anexados estarão lá, exatamente como você os deixou. `Clear session`, no cabeçalho, apaga tudo para começar de novo. Uma sessão, porém, existe apenas naquele navegador, então recomendamos salvar o seu trabalho como projeto de tempos em tempos.

Em `Save`, no cabeçalho, você pode salvar:

- `Project`: as árvores e tudo o que as acompanha, incluindo abas, aparência, tabelas, alinhamentos, mapas, imagens e, se você escolher, todas as árvores de um conjunto. Ele pode ser aberto de novo depois, em qualquer computador, em `Import` > `Project`. Ao salvá-lo, uma janela permite deixar de fora os arquivos anexados ou as árvores do conjunto, e comprimir o arquivo, o que o torna muito mais leve.
- `Style`: apenas a aparência da figura, sem a árvore nem os dados. Um estilo pode ser aplicado a outra árvore em `Import` > `Style`, o que é prático para dar a mesma aparência a todas as figuras de um artigo.

Por fim, exporte a figura em `Export`, como SVG ou PDF, arquivos vetoriais que continuam nítidos em qualquer tamanho, ou como PNG ou TIFF, na resolução e no tamanho que você escolher. O mesmo menu salva a árvore como está agora, com seus nomes, enraizamento e ordem, em Newick ou NEXUS, e, no caso de um conjunto de árvores, as árvores da amostra.

## 19. Redes filogenéticas

Embora não faça parte do nosso exemplo de vertebrados, falta uma seção para explorar: **Phylogenetic networks**. A história de um grupo nem sempre é uma árvore: quando as linhagens trocam genes, por hibridização ou introgressão, ela é melhor representada como uma rede. O tree2go lê redes em Newick estendido (eNewick), como as escritas pelo PhyloNet ou pelo SNaQ, em que cada reticulação é marcada com um rótulo como `#H1`.

Como exemplo, usamos `heliconius_network.nwk`, uma pequena rede de borboletas *Heliconius* inspirada em dois casos bem conhecidos, com valores fictícios: *H. heurippa*, uma espécie de origem híbrida entre *H. cydno* e *H. melpomene*, e *H. timareta*, que recebeu genes de *H. melpomene* por introgressão. Ela abre com `Open tree`, como qualquer árvore.

O tree2go reconhece as reticulações, e o tipo de cada uma, a partir do seu rótulo no arquivo: `#H` para hibridização, `#LGT` para transferência lateral de genes e `#R` para recombinação, cada uma com sua própria cor em **Phylogenetic networks**. Os dois eventos do nosso exemplo são hibridizações (`#H`). O que distingue uma espécie híbrida de uma introgressão é gama (γ), a proporção do genoma herdada de cada progenitor, um valor que pode ser mostrado como qualquer outra anotação da árvore.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig24-major.png" alt="A rede de Heliconius desenhada como sua árvore principal, com duas setas tracejadas do ramo de H. melpomene para H. heurippa e H. timareta, rotuladas com seus valores de gama"><figcaption><b>Figura 24A.</b> A rede desenhada como sua árvore principal, com cada reticulação como uma seta do doador para a linhagem híbrida.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig24-full.png" alt="A mesma rede desenhada por completo, em que cada nó híbrido une suas duas arestas parentais, com espessuras que seguem gama"><figcaption><b>Figura 24B.</b> A mesma rede desenhada por completo, com as duas arestas parentais de cada nó híbrido.</figcaption></figure>
  </div>
</figure>

As reticulações são desenhadas como linhas tracejadas da linhagem doadora até o nó híbrido. Por padrão, uma seta aponta do doador para o receptor (*Arrows* > `To hybrid`), mas também pode apontar no sentido contrário, nos dois sentidos ou não aparecer. Com *Show a value on each line*, cada linha mostra seu γ, e com *Width from γ*, sua espessura o acompanha. *Where on the branches* define onde cada linha começa e termina, `Centered` as coloca no meio dos ramos, enquanto `Lengths` usa as idades escritas no arquivo. Como qualquer outro elemento, cada linha pode ser selecionada com um clique e mudada separadamente pelo seu menu de `Right-click`.

Por fim, *Style* alterna entre duas vistas da mesma rede. `Major tree` desenha a árvore das arestas principais, as que levam a maior parte do genoma, com cada aresta secundária como uma linha a partir do seu doador (Fig. 24A), enquanto `Full network` dá a cada nó híbrido um ponto próprio, onde suas duas arestas parentais se encontram (Fig. 24B).
