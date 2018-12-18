---
title: Análise de quadros de gráficos | Microsoft Docs
ms.custom: ''
ms.date: 02/09/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.frameanalysis
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e0ae541830adab222b07d1f16ce99e4957e380e5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49838095"
---
# <a name="graphics-frame-analysis"></a>Análise de Quadros de Gráficos
Use análise de quadros de gráficos no analisador de gráficos do Visual Studio para analisar e otimizar o desempenho de renderização do Direct3D jogo ou aplicativo.  

## <a name="frame-analysis"></a>Análise de quadro  
 A análise de quadro usa as mesmas informações capturadas em um arquivo de log de elementos gráficos para fins de diagnóstico, mas as utiliza para resumir o desempenho de renderização. As informações de desempenho não são registradas no log durante a captura; ao invés disso, as informações de desempenho são geradas posteriormente, durante a análise de quadro, programando eventos e coletando estatísticas conforme o quadro é reproduzido. Essa abordagem possui diversas vantagens em relação a registrar informações de desempenho durante a captura:  
  
- A análise de quadro pode tirar uma média dos resultados de diversas reproduções do mesmo quadro para garantir que o resumo do desempenho seja estatisticamente sólido.  
  
- A análise de quadro pode gerar informações de desempenho para configurações de hardware e dispositivos diferentes daqueles em que as informações foram capturadas.  
  
- Análise de quadro pode gerar novos resumos de desempenho de informações capturadas anteriormente — por exemplo, quando os drivers de GPU são otimizados ou expõem recursos de depuração adicionais.  
  
  Além dessas vantagens, a análise de quadros também pode alterar o modo como o quadro é renderizado durante a reprodução para que ela possa apresentar informações sobre como essas mudanças podem afetar o desempenho de renderização de um aplicativo. Você pode usar essas informações para se decidir entre possíveis estratégias de otimização sem ter que implementar todas elas e, depois, capturar e comparar todos os resultados você mesmo.  
  
  Embora a análise de quadro seja primordialmente pensada para ajudá-lo a alcançar um desempenho de renderização mais rápido, ela também pode ajudá-lo a atingir uma qualidade visual aprimorada para um determinado destino de desempenho ou reduzir o consumo de energia de GPU.  
  
  Para ver uma demonstração do que a análise de quadros pode fazer para seu aplicativo, você pode assistir a [análise de quadros de gráficos do Visual Studio](https://channel9.msdn.com/Shows/C9-GoingNative/GoingNative-25-Offline-Analysis-Graphics-Tool) vídeo no Channel 9.  
  
## <a name="using-frame-analysis"></a>Usando a análise de quadro  
 Antes de usar a análise de quadro, você precisa capturar informações gráficas de seu aplicativo enquanto ele é executado, exatamente como você faria ao usar qualquer uma das ferramentas do analisador de gráficos. Em seguida, na janela de documento (. vsglog) do log de gráficos, escolha o **análise de quadros** guia.  
  
 ![Selecione a guia análise de quadro](media/pix_frame_analysis_select_tab.png "pix_frame_analysis_select_tab")  
  
 Os resultados são exibidos após a conclusão da análise. A parte superior da guia de análise de quadros exibe a linha do tempo e a tabela de resumo. A parte inferior exibe as tabelas de detalhes. Se erros ou avisos forem gerados durante a reprodução, eles são resumidos acima da linha do tempo; a partir daí, é possível seguir os links para saber mais sobre os erros e os avisos.  
  
### <a name="interpreting-results"></a>Interpretando os resultados  
 Ao interpretar os resultados de cada variante, você pode inferir informações úteis sobre o desempenho de renderização e o comportamento do aplicativo. Para obter mais informações sobre as variantes de renderização, consulte [variantes](#Variants) mais adiante neste artigo.  
  
 Alguns resultados indicam diretamente como a variante afeta o desempenho de renderização:  
  
- Se a variante Filtragem de Textura Bilinear tiver mostrado ganhos de desempenho, usar a filtragem de textura bilinear no aplicativo mostrará ganhos de desempenho semelhantes.  
  
- Se a variante do Visor 1 x 1 mostrar ganhos de desempenho, reduzir o tamanho dos destinos de renderização no aplicativo aprimorará o desempenho de renderização.  
  
- Se a variante Compactação de Textura BC tiver mostrado ganhos de desempenho, usar a compactação de textura BC no aplicativo mostrará ganhos de desempenho semelhantes.  
  
- Se a variante 2xMSAA tiver quase o mesmo desempenho que a variante 0xMSAA, você poderá habilitar 2xMSAA no aplicativo para aprimorar a qualidade de renderização sem prejudicar o desempenho.  
  
  Outros resultados podem sugerir implicações mais profundas e sutis no desempenho do aplicativo:  
  
- Se a variante do Visor 1 x 1 mostrar ganhos de desempenho muito grandes, seu aplicativo provavelmente está consumindo mais taxa de enchimento do que a disponível. Se essa variante não mostrar ganhos de desempenho, o aplicativo provavelmente está processando muitas vértices.  
  
- Se a variante de Formato de Destino de Renderização de 16 bpp mostrar ganhos de desempenho significativos, seu aplicativo provavelmente está consumindo muita largura de banda de memória.  
  
- Se a variante de Dimensões de Textura de Metade/Quarto mostrar ganhos de desempenho significativos, suas texturas provavelmente ocupam muita memória, consomem muita largura de banda ou usam o cache de textura de maneira ineficiente. Se essa variante não mostrar uma alteração no desempenho, provavelmente, você poderá usar texturas maiores e mais detalhadas sem prejudicar o desempenho.  
  
  Quando contadores de hardware estão disponíveis, é possível usá-los para coletar informações bastante detalhadas sobre o motivo pelo qual o desempenho de renderização do aplicativo pode estar sendo impactado. Todos os dispositivos em nível de recurso 9.2 e superior dão suporte a consultas de oclusão de profundidade (**pixels obstruídos** contador) e carimbos de hora. Outros contadores de hardware podem estar disponíveis, dependendo se o fabricante de GPU implementou contadores de hardware e os expôs no driver. Você pode usar esses contadores para confirmar a causa precisa dos resultados mostrados na tabela de resumo; por exemplo, é possível determinar se o desenho excessivo é um fator relevante, examinando a porcentagem de pixels que foram obstruídos pelo teste de profundidade.  
  
### <a name="timeline-and-summary-table"></a>Linha do tempo e tabela de resumo  
 Por padrão, a Linha do Tempo e a Tabela de Resumo são exibidas e as outras seções são recolhidas.  
  
#### <a name="timeline"></a>Linha do tempo  
 A linha do tempo mostra uma visão geral dos horários de chamadas de desenho em relação umas às outras. Como barras maiores correspondem a horários de desenho maiores, você pode usá-las para localizar rapidamente as chamadas de desenho mais custosas no quadro. Quando o quadro capturado contiver um número muito grande de chamadas de desenho, diversas chamadas de desenho são combinadas em uma única barra, cujo comprimento é a soma dessas chamadas de desenho.  
  
 ![A linha do tempo mostra o desenho&#45;chamar os custos. ](media/pix_frame_analysis_timeline.png "pix_frame_analysis_timeline")  
  
 Você pode deixar o ponteiro sobre uma barra para ver a qual evento de chamada de desenho a barra corresponde. Escolher a barra faz com que a lista de eventos seja sincronizada com esse evento.  
  
#### <a name="table"></a>Tabela  
 A tabela de números abaixo da linha do tempo mostra o desempenho relativo de cada variante de renderização para cada chamada de desenho em relação à renderização padrão do seu aplicativo. Cada coluna exibe uma variante de renderização diferente e cada linha representa uma chamada de desenho diferente identificada na coluna mais à esquerda; a partir daí, é possível seguir um link até o evento na janela Lista de Eventos de Gráficos.  
  
 ![A tabela de resumo mostra as variantes diferentes. ](media/pix_frame_analysis_summary.png "pix_frame_analysis_summary")  
  
 A segunda coluna mais à esquerda na Tabela de Resumo exibe o horário de renderização de linha de base de seu aplicativo, ou seja, a quantidade de tempo necessária para que a renderização padrão do seu aplicativo conclua a chamada de desenho. As colunas restantes mostram o desempenho relativo de cada variante de renderização como uma porcentagem da linha de base de forma que facilite ver se o desempenho foi aprimorado. Porcentagens superiores a 100% levam mais tempo do que a linha de base, ou seja, o desempenho foi reduzido; porcentagens inferiores a 100% levam menos tempo, indicando que o desempenho foi aumentado.  
  
 Os valores do horário absoluto da linha de base e o horário relativo das variantes de renderização são, na verdade, médias de várias execuções; 5 por padrão. Essa média ajuda a assegurar que os dados de horário são confiáveis e consistentes. Você pode deixar o ponteiro em cada célula da tabela para examinar os valores de horário mínimo, máximo, médio e mediano que foram observados quando os resultados dessa chamada de desenho e variante de renderização foram gerados. O horário de linha de base também é exibido.  
  
#### <a name="hot-draw-calls"></a>Chamadas de desenho "ativas"  
 Para chamar atenção para chamadas de desenho que consomem uma proporção maior do tempo de renderização geral ou que podem ser incomumente mais lentas por motivos que podem ser evitados, a linha que contém essas chamadas de desenho "ativas" é exibida em vermelho quando seu horário de linha de base tem mais de um desvio padrão em relação ao horário de linha de base médio de todas as chamadas de desenho no quadro.  
  
 ![Essa chamada DrawIndexed tem variantes quentes e frios. ](media/pix_frame_analysis_hot_calls.png "pix_frame_analysis_hot_calls")  
  
#### <a name="statistical-significance"></a>Significância estatística  
 Para chamar atenção para as variações de renderização que possuem maior relevância, a Análise de Quadro determina a significância estatística de cada variante de renderização e exibe aquelas de são significativas em negrito. Aquelas que aprimoram o desempenho são exibidas em verde, e as que reduzem o desempenho, em vermelho. Os resultados que não são estatisticamente significativos são exibidos em fonte normal.  
  
 ![A estatística relevence da variante chamada draw](media/pix_frame_analysis_summary_stats.png "pix_frame_analysis_summary_stats")  
  
 Para determinar a relevância estatística, análise de quadro usa o [teste t de Student](http://www.wikipedia.org/wiki/Student%27s_t-test).  
  
### <a name="details-table"></a>Tabela de detalhes  
 Abaixo da tabelo de Resumo está a tabela de Detalhes, que fica recolhida por padrão. O conteúdo da tabela de Detalhes depende da plataforma de hardware do computador de reprodução. Para obter informações sobre as plataformas de hardware com suporte, consulte [suporte de Hardware](#HardwareSupport).  
  
#### <a name="platforms-that-do-not-support-hardware-counters"></a>Plataformas que não oferecem suporte a contadores de hardware  
 A maioria das plataformas não oferece suporte completo a contadores de GPU de hardware; isso inclui todas as GPUs oferecidas atualmente pela Intel, AMD e nVidia. Quando não há contadores de hardware para coleta, somente uma tabela de Detalhes é exibida, e ela contém o horário absoluto médio de todas as variantes.  
  
 ![A tabela de detalhes e algumas variantes de reprodução. ](media/pix_frame_analysis_details.png "pix_frame_analysis_details")  
  
#### <a name="platforms-that-support-hardware-counters"></a>Plataformas que oferecem suporte a contadores de hardware  
 No caso de plataformas que oferecem suporte a contadores de GPU de hardware, por exemplo, SOC da nVidia T40 e todos os SOCs da Qualcomm, diversas tabelas de Detalhes são exibidas, uma para cada variante. Cada contador de hardware disponível é coletado para cada variante de renderização e exibido em sua própria tabela de Detalhes.  
  
 ![Contadores de hardware são exibidos quando houver suporte. ](media/pix_frame.png "pix_frame")  
  
 As informações do contador de hardware oferecem uma visão bastante detalhada de comportamentos específicos da plataforma de hardware para cada chamada de desempenho, o que pode ajudar a identificar a causa de gargalos de desempenho de maneira bastante precisa.  
  
> [!NOTE]
>  Diferentes plataformas de hardware oferecem suporte a diferentes contadores; não há um padrão. Os contadores e aquilo que eles representam são determinados exclusivamente para cada fabricante de GPU.  
  
### <a name="marker-regions-and-events"></a>Regiões e eventos do marcador  
 A Análise de Quadro oferece suporte a marcadores de evento e grupos de evento definidos pelo usuário. Eles são exibidos na tabela de Resumo nas tabelas de Detalhes.  
  
 Você pode usar as APIs ID3DUserDefinedAnnotation ou a família legada de APIs D3DPERF_ para criar marcadores e grupos. Ao usar a família de APIs D3DPERF_, você pode atribuir uma cor a cada marcador e grupo exibidos pela Análise de Quadro como uma faixa colorida nas linhas que contêm os marcadores de início/término do marcador de evento ou do grupo de evento e seus conteúdos. Esse recurso pode ajudar a identificar rapidamente eventos ou grupos de eventos de renderização importantes.  
  
### <a name="warnings-and-errors"></a>Avisos e erros  
 Ocasionalmente, a Análise de Quadros é concluída com avisos ou erros, que são resumidos acima da Linha do Tempo e detalhados na parte inferior da guia Análise de Quadros.  
  
 Em geral, avisos e erros são apenas para fins informativos e não exigem intervenção.  
  
 Avisos geralmente indicam que o suporte ao hardware está ausente, mas que há uma solução alternativa, que contadores de hardware não podem ser coletados ou que determinados dados de desempenho podem não ser confiáveis, por exemplo, quando uma solução alternativa os afeta de maneira adversa.  
  
 Erros geralmente indicam que a implementação da análise de quadros possui bugs, que um driver possui bugs, que o suporte de hardware está ausente e não há uma solução alternativa ou que o aplicativo está tentando algo não suportado pela reprodução.  
  
### <a name="retries"></a>Novas tentativas  
 Se a GPU passar por uma transição de estado de energia durante a análise de quadros, a análise deve ser executada novamente, pois a velocidade de clock da GPU foi alterada o que, portanto, invalidou os resultados relativos do horário.  
  
 A Análise de Quadro limita o número de novas tentativas a 10. Se sua plataforma tiver um gerenciamento de energia ou clock-gating agressivo, isso pode fazer com que a Análise de Quadro falhe e relate um erro por ter excedido o limite de novas tentativas. Se a plataforma permitir, você pode atenuar esse problema redefinindo o gerenciamento de energia e a aceleração da velocidade de clock de sua plataforma para que sejam menos agressivos.  
  
##  <a name="HardwareSupport"></a> Suporte de hardware  
  
### <a name="timestamps-and-occlusion-queries"></a>Consultas de carimbos de data/hora e oclusão  
 Carimbos de data/hora têm suporte em todas as plataformas compatíveis com Análise de Quadro. Consultas de oclusão de profundidade, necessárias para o contador de Pixels Obstruídos, são suportadas em plataformas com nível de recurso de suporte 9.2 ou superior.  
  
> [!NOTE]
>  Embora carimbos de data e hora sejam suportados em todas as plataformas que dão suporte à Análise de Quadros, a precisão e a consistência dos carimbos varia de uma plataforma para outra.  
  
### <a name="gpu-counters"></a>Contadores de GPU  
 O suporte a contadores de hardware de GPU dependem do hardware.  
  
 Como nenhuma GPU de computador atualmente oferecida pela Intel, AMD ou nVidia tem suporte confiável a contadores de hardware de GPU, a Análise de Quadro não coleta contadores delas. No entanto, a análise de quadro coleta contadores de hardware a seguir GPU, que forma confiável dá suporte a eles:  
  
- nVidia T40 (Tegra4)
  
  Nenhuma outra plataforma com suporte à Análise de Quadro coleta contadores de hardware de GPU.  
  
> [!NOTE]
>  Como os contadores de hardware de GPU são recursos de hardware, pode levar vários passos para coletar o conjunto completo de contadores de hardware para cada variante de renderização. Como resultado, a ordem na qual os contadores de GPU são coletados não é especificada.  
  
## <a name="unsupported-scenarios"></a>Cenários sem suporte  
 Determinadas maneiras de usar a análise de quadro não possui suporte ou simplesmente não valem a pena.  
  
### <a name="playback-of-high-feature-level-captures-on-down-level-devices"></a>Reprodução de capturas de alto nível de recursos em dispositivos de baixo nível  
 No analisador de gráficos, ao reproduzir um arquivo de log de gráficos que usa um nível mais alto de recurso que dá suporte ao computador de reprodução, ele recorre automaticamente ao WARP. Na Análise de Quadro, ele não recorre explicitamente ao WARP e gera um erro; o WARP é útil para examinar a precisão do aplicativo Direct3D, mas não para examinar seu desempenho.  
  
> [!NOTE]
>  Embora seja importante manter os problemas de nível de recurso em mente, você pode capturar e reproduzir arquivos de log de elementos gráficos em diferentes configurações de hardware e dispositivos. O log de gráficos pode ser executado novamente desde que o arquivo de log não contenha APIs nem utilize níveis de recurso que não têm suporte no computador de reprodução.  
  
### <a name="direct3d-10-and-lower"></a>Direct3D 10 e versão anterior  
 Se seu aplicativo chama a API do Direct3D 10, a análise de quadro não reconhece ou criar o perfil mesmo que ela seja reconhecida e usadas por outras ferramentas do analisador de gráficos.
  
> [!NOTE]
>  Isso se aplica somente às chamadas à API do Direct3D que você estiver utilizando, e não aos níveis de recurso.

### <a name="warp"></a>WARP  
 A análise de quadro deve ser usada para analisar e aprimorar o desempenho de renderização em hardwares reais. Executar análise de quadro em dispositivos WARP não será impedida, mas ela geralmente não é vantajoso porque WARP em execução em uma CPU de alto nível é mais lento do que até mesmo as GPUs modernas com menor capacidade e desempenho de WARP pode variar bastante dependendo da CPU específica ele está em execução.  
  
##  <a name="Variants"></a> Variantes  
 Cada alteração que a análise de quadro realiza na maneira que um quadro é renderizado durante a reprodução é conhecida como uma *variante*. As variantes examinadas pela Análise de Quadro correspondem a alterações comuns e relativamente fáceis que podem ser feitas para aprimorar o desempenho de renderização ou a qualidade visual do aplicativo; por exemplo, reduzir o tamanho das texturas, usar a compactação de texturas ou habilitar diferentes tipos de suavização. As variantes substituem o contexto de renderização e os parâmetros comuns do seu aplicativo. Segue um resumo:  
  
|Variante|Descrição|  
|-------------|-----------------|  
|**Tamanho do visor 1 x 1**|Reduz as dimensões do visor em todos os destinos de renderização para 1 x 1 pixels.<br /><br /> Para obter mais informações, consulte [variante de tamanho do visor 1 x 1](1x1-viewport-size-variant.md)|  
|**0x MSAA**|Desativa a MSAA (suavização de múltipla amostra) em todos os destinos de renderização.<br /><br /> Para obter mais informações, consulte [0x / 2 x / 4 variantes de MSAA](0x-2x-4x-msaa-variants.md)|  
|**2x MSAA**|Ativa a MSAA de 2x em todos os destinos de renderização.<br /><br /> Para obter mais informações, consulte [0x / 2 x / 4 variantes de MSAA](0x-2x-4x-msaa-variants.md)|  
|**4x MSAA**|Ativa a MSAA de 4x em todos os destinos de renderização.<br /><br /> Para obter mais informações, consulte [0x / 2 x / 4 variantes de MSAA](0x-2x-4x-msaa-variants.md)|  
|**Filtragem de textura de ponto**|Define o modo de filtragem como `DXD11_FILTER_MIN_MAG_MIP_POINT` (filtragem de textura de ponto) para todas as amostras de textura adequadas.<br /><br /> Para obter mais informações, consulte [ponto, Bilinear, Trilinear e variantes de filtragem de textura Anisotrópica](point-bilinear-trilinear-and-anisotropic-texture-filtering-variants.md).|  
|**Filtragem de textura bilinear**|Define o modo de filtragem como `DXD11_FILTER_MIN_MAG_LINEAR_MIP_POINT` (filtragem de textura bilinear) para todas as amostras de textura adequadas.<br /><br /> Para obter mais informações, consulte [ponto, Bilinear, Trilinear e variantes de filtragem de textura Anisotrópica](point-bilinear-trilinear-and-anisotropic-texture-filtering-variants.md).|  
|**Filtragem de textura trilinear**|Define o modo de filtragem como `DXD11_FILTER_MIN_MAG_MIP_LINEAR` (filtragem de textura trilinear) para todas as amostras de textura adequadas.<br /><br /> Para obter mais informações, consulte [ponto, Bilinear, Trilinear e variantes de filtragem de textura Anisotrópica](point-bilinear-trilinear-and-anisotropic-texture-filtering-variants.md).|  
|**Filtragem de textura anisotrópica**|Define o modo de filtragem para `DXD11_FILTER_ANISOTROPIC` e `MaxAnisotropy` para `16` (16 x filtragem de textura anisotrópica) para todas as amostras de textura adequadas.<br /><br /> Para obter mais informações, consulte [ponto, Bilinear, Trilinear e variantes de filtragem de textura Anisotrópica](point-bilinear-trilinear-and-anisotropic-texture-filtering-variants.md).|  
|**Formato de destino de renderização de 16 bpp**|Define o formato de pixels como `DXGI_FORMAT_B5G6R5_UNORM` (16 bpp, formato 565) para todos os destinos de renderização e buffers de fundo.<br /><br /> Para obter mais informações, consulte [formato destino 16 bpp renderizar Variant](16bpp-render-target-format-variant.md)|  
|**Geração de mapas MIP**|Ativa mapas mip em todas as texturas que não são destinos de renderização.<br /><br /> Para obter mais informações, consulte [variante de geração de Mip-map](mip-map-generation-variant.md).|  
|**Dimensões de textura pela metade**|Reduz as dimensões de textura em todas as texturas que não são destinos de renderização pela metade de seu tamanho original em cada dimensão. Por exemplo, uma textura de 256 x 128 é reduzida para 128 x 64 texels.<br /><br /> Para obter mais informações, consulte [variantes de dimensões de textura de metade/quarto](half-quarter-texture-dimensions-variant.md).|  
|**Dimensões de textura de um quarto**|Reduz as dimensões de textura em todas as texturas que não são destinos de renderização a um quarto de seu tamanho original em cada dimensão. Por exemplo, uma textura de 256 x 128 é reduzida para 64 x 32 texels.<br /><br /> Para obter mais informações, consulte [variantes de dimensões de textura de metade/quarto](half-quarter-texture-dimensions-variant.md).|  
|**Compactação de textura BC**|Habilita a compactação de bloco em todas as texturas que possuem uma variante de formato de pixel de B8G8R8X8, B8G8R8A8 ou R8G8B8A8. As variantes de formato B8G8R8X8 são compactados com BC1; as variantes de formato B8G8R8A8 e R8G8B8A8 são compactadas com BC3.<br /><br /> Para obter mais informações, consulte [variante de compressão de textura BC](bc-texture-compression-variant.md).|  
  
 O resultado para a maioria das variantes é descrito como: "Reduzir o tamanho da textura pela metade é 25% mais rápido" ou "Ativar MSAA de 2x é apenas 2% mais lento". Outras variantes podem exigir mais interpretação; por exemplo, se a variante que alterar as dimensões do visor para 1 x 1 mostrar um ganho de desempenho grande, isso pode indicar que a renderização é afunilada por uma taxa de enchimento baixa; alternativamente, se não houver uma alteração significativa no desempenho, isso pode indicar que a renderização é afunilada pelo processamento de vértice.