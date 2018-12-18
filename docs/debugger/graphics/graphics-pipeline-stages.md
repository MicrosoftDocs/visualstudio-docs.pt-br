---
title: Estágios de Pipeline gráficos | Microsoft Docs
ms.custom: ''
ms.date: 02/09/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.pipeline
ms.assetid: 2bf5c12e-2a00-401c-8163-4e373d08ad3f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: da74af0f77586e518365fa669c84309e7751b319
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941537"
---
# <a name="graphics-pipeline-stages"></a>Estágios de Pipeline Gráficos
A janela estágios de Pipeline gráficos ajuda a entender como uma chamada de desenho individuais é transformada por cada estágio do pipeline de gráficos do Direct3D.  
  
 Esta é a janela de estágios de Pipeline:  
  
 ![Um objeto 3D percorre os estágios de pipeline.](media/gfx_diag_demo_pipeline_stages_orientation.png)
  
## <a name="understanding-the-graphics-pipeline-stages-window"></a>Noções básicas sobre a janela Estágios de Pipeline Gráficos  
 A janela estágios de Pipeline visualiza o resultado de cada estágio de pipeline gráficos separadamente, para cada chamada de desenho. Normalmente, os resultados dos estágios no meio do pipeline estiverem ocultas, tornando difícil determinar onde um problema de renderização é iniciado. Visualizando separadamente cada estágio, a janela estágios de Pipeline torna mais fácil ver onde o problema começa — por exemplo, você pode ver facilmente quando o estágio de sombreador de vértice inesperadamente faz com que um objeto a ser desenhado fora da tela.  
  
 Depois de identificar o estágio em que o problema ocorre, você pode usar outras ferramentas do analisador de gráficos para examinar como os dados foram interpretados ou transformados. Problemas de renderização que aparecem nos estágios de pipeline geralmente são descritores de formato de vértice relacionados a incorreto, programas de sombreador com bugs ou estado configurado incorretamente.  
  
### <a name="links-to-related-graphics-objects"></a>Links para os objetos gráficos relacionados  
 Contexto adicional, às vezes, é necessário para determinar por que uma chamada de desenho interage de uma maneira específica com o pipeline de gráficos. Para facilitar a localização deste contexto adicional, os links de janela estágios de Pipeline gráficos a um ou mais objetos que fornecem contexto adicional relacionado ao que está acontecendo no pipeline gráfica.  
  
- No Direct3D 12 esse objeto é geralmente uma lista de comandos.  
  
- No Direct3D 11 esse objeto é geralmente um contexto de dispositivo de gráficos.  
  
  Esses links são parte da assinatura do evento atual do elementos gráficos que está localizada no canto superior esquerdo da janela estágios de Pipeline gráficos. Depois de qualquer um desses links para examinar os detalhes adicionais sobre o objeto.  
  
### <a name="viewing-and-debugging-shader-code"></a>Exibição e depuração do código do sombreador  
 Você pode examinar e depurar o código para o vértice, hull, domínio, geometria e pixel shaders usando os controles na parte inferior de seus respectivos estágios na janela estágios de Pipeline.  
  
#### <a name="to-view-a-shaders-source-code"></a>Para exibir o código-fonte do sombreador  
  
-   No **estágios de Pipeline gráficos** janela, localize o estágio de sombreador que corresponde ao sombreador que deseja examinar. Em seguida, abaixo da imagem de visualização, siga o link de título do estágio de sombreador — por exemplo, siga o link **obj:30 do sombreador de vértices** para exibir o código de origem do sombreador de vértice.  
  
    > [!TIP]
    >  O número de objeto **obj:30**, identifica esse sombreador em toda a interface de analisador de gráficos como a janela de histórico de pixel e de tabela do objeto.  
  
#### <a name="to-debug-a-shader"></a>Para depurar um sombreador  
  
-   No **estágios de Pipeline gráficos** janela, localize o estágio de sombreador que corresponde ao sombreador que deseja depurar. Em seguida, abaixo da imagem de visualização, escolha **iniciar depuração**. Esse ponto de entrada para os padrões de depurador HLSL para a primeira invocação do sombreador para o estágio correspondente — ou seja, o primeiro pixel, vértice ou primitivo que é processado pelo sombreador durante esta chamada de desenho. Invocações deste sombreador para um vértice ou pixel específico podem ser acessadas por meio de **histórico de Pixel de gráficos**.  
  
### <a name="the-pipeline-stages"></a>Os estágios de pipeline  
 A janela estágios de Pipeline visualiza apenas os estágios do pipeline que estavam ativos durante a chamada de desenho. Cada estágio do pipeline gráfica transforma uma entrada de estágio anterior e passa o resultado para o próximo estágio. O primeiro estágio, o Assembler de entrada — extrai dados de índice e vértice de seu aplicativo como sua entrada; o último estágio — a fusão de saída — combina recentemente renderizado pixels junto com o conteúdo atual do framebuffer ou destino de renderização como sua saída para produzir a imagem final, você vê na tela.  
  
> [!NOTE]
>  Sombreadores de cálculo não dá suporte a **estágios de Pipeline gráficos** janela.  
  
 **Assembler de entrada**  
 O Assembler de entrada lê os dados de índice e vértice especificados pelo seu aplicativo e monta no hardware de gráficos.  
  
 Na janela estágios de Pipeline, a saída do Assembler de entrada é visualizada como um modelo de wireframe. Para tirar a examinar mais detalhadamente os resultados, selecione **Assembler de entrada** na **estágios de Pipeline gráficos** janela para exibir os vértices montados em 3D completo usando o Editor de modelo.  
  
> [!NOTE]
>  Se o `POSITION` semântica não está presente na saída do assembler de entrada e, em seguida, nada é exibido na **Assembler de entrada** estágio.  
  
 **Sombreador de vértice**  
 O estágio de sombreador de vértice processa vértices, normalmente executando operações como a transformação, colocação de capa e iluminação. Sombreadores de vértices produzem o mesmo número de vértices que eles utiliza como entrada.  
  
 Na janela estágios de Pipeline, a saída do sombreador de vértice é visualizada como uma imagem de varredura de wireframe. Para tirar a examinar mais detalhadamente os resultados, selecione **sombreador de vértice** na **estágios de Pipeline gráficos** windows para exibir os vértices processados no Editor de imagens.  
  
> [!NOTE]
>  Se o `POSITION` ou `SV_POSITION` semântica não estiver presente na saída do sombreador de vértice, nada é exibido na **sombreador de vértices** estágio.  
  
 **Convexos sombreador** (Direct3D 11 e Direct3D 12 somente)  
 Os processos de estágio de sombreador hull controlam pontos que definem uma superfície de ordem inferior, como uma linha, triângulo ou quad. Como saída, ele produz um patch de geometria de ordem superior e constantes do patch que são passados para o estágio de mosaico de função fixa.  
  
 O estágio de sombreador hull não é visualizado na janela estágios de Pipeline.  
  
 **Estágio de tessellator** (Direct3D 11 e Direct3D 12 somente)  
 O estágio de tessellator é uma unidade de hardware de função fixa (não programável) que pré-processa o domínio representado pela saída do sombreador hull. Como saída, ele cria um padrão de amostragem do domínio e um conjunto de primitivos menores — pontos, linhas ou triângulos — que se conectam a esses exemplos.  
  
 O estágio de tessellator não é visualizado na janela estágios de Pipeline.  
  
 **Sombreador de domínio** (Direct3D 11 e Direct3D 12 somente)  
 O estágio de sombreador de domínio processa os patches de geometria de ordem superior do sombreador Hull, fatores de subdivisão juntos do estágio de mosaico. O mosaico fatores podem ser incluem os fatores de entrada tessellator, bem como fatores de saída. Como saída, ele calcula a posição de vértice de um ponto em que o patch de saída de acordo com os fatores de tessellator.  
  
 O estágio de sombreador de domínio não é visualizado na janela estágios de Pipeline.  
  
 **Sombreador de geometria**  
 O estágio de sombreador de geometria processa primitivos inteiros — triângulos, linhas ou pontos — junto com os dados de vértice opcionais para primitivos adjacentes de borda. Ao contrário de sombreadores de vértices, sombreadores de geometria podem produzir mais ou menos primitivos que eles usam como de entrada.  
  
 Na janela estágios de Pipeline, a saída do sombreador de geometria é visualizada como uma imagem de varredura de wireframe. Para tirar a examinar mais detalhadamente os resultados, selecione **sombreador de geometria** na **estágios de Pipeline gráficos** janela para exibir os primitivos processados no Editor de imagens.  
  
 **Estágio de Output Stream**  
 O estágio de output stream pode interceptar primitivos transformados antes da rasterização e gravá-las em memória. a partir daí, os dados podem ser recirculated como entrada para anteriores estágios de pipeline gráficos ou ser lidos novamente pela CPU.  
  
 O estágio de output stream não é visualizado na janela estágios de Pipeline.  
  
 **Rasterizer Stage**  
 O estágio de rasterizador é uma unidade de hardware (não programável) de função fixa que converte os primitivos de vetor — pontos, linhas ou triângulos — em uma imagem de varredura, executando a conversão de linha de varredura. Durante a rasterização vértices são transformados no espaço do clipe homogêneo e recortados. Como saída, sombreadores de pixel são mapeados e os atributos por vértice são interpolados entre o primitivo e preparados para o sombreador de pixel.  
  
 Rasterizer stage não é visualizado na janela estágios de Pipeline.  
  
 **Sombreador de pixel**  
 Os valores de pixel shader estágio processos rasterizado primitivos de junto com os dados de vértice interpolados para gerar por pixel, como cor e a profundidade.  
  
 Na janela estágios de Pipeline, a saída do sombreador de pixel é visualizada como uma imagem de varredura de quatro cores. Para tirar a examinar mais detalhadamente os resultados, selecione **sombreador de Pixel** na **estágios de Pipeline gráficos** janela para exibir os primitivos processados no Editor de imagens.  
  
 **Fusão de saída**  
 O estágio de fusão de saída combina o efeito de pixels renderizados recentemente junto com o conteúdo existente de seus buffers correspondentes — cor, profundidade e estêncil — para produzir novos valores nesses buffers.  
  
 Na janela estágios de Pipeline, a saída de fusão de saída é visualizada como uma imagem de varredura de quatro cores. Para aproveitar a examinar mais detalhadamente os resultados, selecione **fusão de saída** na **estágios de Pipeline gráficos** janela para exibir o framebuffer mesclada.  
  
### <a name="vertex-and-geometry-shader-preview"></a>Vértices e visualização do sombreador de geometria  
 Quando você seleciona o estágio de sombreador de geometria ou de vértice na **estágios de Pipeline** janela, você pode exibir as entradas e saídas de sombreador no painel abaixo.  Aqui, você encontrará detalhes sobre a lista de vértices fornecido para os sombreadores depois que eles foram reunidos pelo estágio do assembler de entrada.  

 ![O Visualizador de buffer de entrada do estágio de sombreador de vértice](media/gfx_diag_vertex_shader_inbuffers.png)  
  
 Para exibir o resultado do estágio de sombreador de vértice, escolha a miniatura do estágio de sombreador de vértice para exibir um wireframe de varredura em tamanho normal, da malha após seu foram transformados pelo sombreador de vértice.  
  
 ![A visualização de resultado de estágio de sombreador de vértice](media/gfx_diag_vertex_shader_preview.png)  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Objetos ausentes devido ao sombreamento de vértice](walkthrough-missing-objects-due-to-vertex-shading.md)   
 [Passo a passo: depurando erros de renderização devido ao sombreamento](walkthrough-debugging-rendering-errors-due-to-shading.md)