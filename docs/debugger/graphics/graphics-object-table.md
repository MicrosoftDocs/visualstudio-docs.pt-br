---
title: Tabela do objeto de gráfico | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.datavisualizer
- vs.graphics.objecttable
- vs.graphics.bufferviewer
ms.assetid: f48f62d9-16ff-4a2e-8c01-5cbe99513788
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d58c219069efcc98fccaa52dff5bd156212ea64d
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31477759"
---
# <a name="graphics-object-table"></a>Tabela de objetos de gráfico
A tabela de objeto de gráficos na análise de gráficos do Visual Studio ajuda você a entender os objetos de Direct3D que dão suporte a um quadro de seu aplicativo ou um jogo.  
  
 Essa é a tabela de objeto:  
  
 ![Objetos de Direct3D que foram criados por um aplicativo.](media/gfx_diag_demo_object_table_orientation.png "gfx_diag_demo_object_table_orientation")  
  
## <a name="understanding-the-graphics-object-table"></a>Noções básicas sobre a Tabela de Objetos Gráficos  
 Usando o objeto de tabela, você pode analisar os objetos de Direct3D que dão suporte a renderização de um quadro específico. Você pode identificar um problema de renderização para um objeto específico ao examinar suas propriedades e os dados (usando outras ferramentas de diagnóstico de gráficos anteriormente no seu diagnóstico, você pode restringir a lista de objetos que podem não ser que você esperava.) Quando você localizar o objeto incorreto, você pode usar uma visualização que é específica ao seu tipo para examiná-lo — por exemplo, você pode usar o Editor de imagem para exibir texturas, ou o *Visualizador de Buffer* para exibir o conteúdo do buffer.  
  
 A tabela de objeto oferece suporte a copiar e colar para que você pode usar outra ferramenta — por exemplo, o Microsoft Excel — para examinar seu conteúdo.

 Além disso, você pode usar o **tipo** suspenso da parte superior esquerda para alternar a exibição de objetos do tipo **Buffers**, **sombreadores** ou **texturas**, ou todos esses itens de uma só vez.  Além disso, você pode usar a caixa de pesquisa no canto superior direito para localizar linhas específicas em todos os dados que são apresentados.  Por exemplo, você pode procurar *D32_FLOAT* para localizar todas as instâncias de objetos de formato na lista.
  
### <a name="graphics-object-table-format"></a>Formato da Tabela de Objetos Gráficos  
 A tabela de objeto exibe os objetos de Direct3D e recursos que dão suporte a moldura que está associado ao evento selecionado — por exemplo, estado de objetos, buffers, sombreadores, texturas e outros recursos. Objetos que foram criados em um quadro anterior, mas não são usados durante o quadro capturado, são omitidos da tabela de objetos. Objetos que tenham sido destruídos pelo eventos anteriores durante o quadro capturado são omitidos nos eventos subsequentes. Objetos que não são definidos no D3D10Device ou D3D11DeviceContext são exibidos como texto cinza. Os objetos são exibidos em um formato de tabela.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**Identificador**|O ID do objeto.|  
|**Nome**|Informações específicas do aplicativo que foi definido no objeto usando a função Direct3D `SetPrivateData`, normalmente para fornecer informações adicionais de identificação sobre um objeto.|  
|**Tipo**|O tipo de objeto.|  
|**Ativo**|Exibe "*" para um objeto que foi definido no D3D10Device ou D3D11DeviceContext durante o quadro capturado.<br /><br /> Isso corresponde aos objetos que são exibidos como texto cinza, mas fornece uma entrada de coluna que você pode usar para classificar a tabela de objetos.|  
|**Size**|O tamanho do objeto em bytes.|  
|**Formatar**|O formato do objeto. Por exemplo, o formato de um objeto de textura ou o modelo de sombreador de um objeto sombreador.|  
|**Largura**|A largura de um objeto de textura. Não se aplica a outros tipos de objeto.|  
|**Altura**|A altura de um objeto de textura. Não se aplica a outros tipos de objeto.|  
|**Profundidade**|A profundidade de um objeto de textura 3D. Se uma textura não for 3D, o valor é 0. Não se aplica a outros tipos de objeto.|  
|**MIPS**|O número de níveis de MIP que um objeto de textura possui. Não se aplica a outros tipos de objeto.|  
|**ArraySize**|O número de texturas em uma matriz de textura. O intervalo é de 1 a um limite superior definido pelo nível de recurso atual. Para um mapa de cubo, esse valor é 6 vezes o número de mapas de cubo na matriz.|  
|**Amostras**|O número de multisamples por pixel.|  
  
## <a name="graphics-object-viewers"></a>Visualizadores de objeto gráfico  
 Para exibir detalhes sobre um objeto, abra-o clicando em seu nome na tabela de objetos. Detalhes do objeto são exibidos em formatos diferentes, dependendo do tipo do objeto. Por exemplo, texturas são exibidas usando o Visualizador de textura e estado do dispositivo como o contexto de dispositivo D3D11 é exibido como uma lista formatada. Versões diferentes do Direct3D usar objetos diferentes, e geralmente são visualizadores específicos para os objetos mais importantes de cada versão.  
  
 Aqui está o Visualizador de textura, mostrando o conteúdo do estágio do pipeline de fusão de saída.  
  
 ![A visualização de textura exibindo a fusão de saída](media/gfx_diag_texture_preview.png "gfx_diag_texture_preview")  
  
### <a name="d3d12-command-list"></a>Lista de comandos D3D12  
 Direct3D 12 uma lista de comando é um objeto que grava os comandos em um alocador de comando para que eles possam ser enviados para a GPU como uma única solicitação. Listas de comando geralmente executam uma série de configuração de estado, desenhar, limpam e copiar os comandos. Eles são particularmente importantes porque eles são o método preferencial de renderização Direct3D 12 e podem ser usados novamente entre os quadros para ajudar a aumentar o desempenho. Detalhes do comando da lista são exibidos em uma nova janela de documento, com informações relacionadas a cada estágio do pipeline apresentado em sua própria guia.  
  
### <a name="d3d12-pipeline-state-object-pso"></a>Objeto de estado de Pipeline de D3D12 (PSO)  
 Um objeto de estado do pipeline Direct3D 12 representa uma parte significativa do estado GPU, incluindo todas as conjunto sombreadores e determinados objetos de estado da função fixa. Depois de criado, um objeto de estado de pipeline é imutável — um aplicativo só pode alterar a configuração do pipeline pela associação a um objeto de estado do pipeline diferentes. Detalhes PSO são exibidos em uma nova janela de documento, com detalhes da configuração de pipeline dispostos hierarquicamente.  
  
### <a name="d3d12-root-signature"></a>Assinatura de raiz D3D12  
 No Direct3D 12, a assinatura raiz define todos os recursos que estão associados a um pipeline gráficos ou de computação e vincula a listas de comando para os recursos que os sombreadores requer. Normalmente há uma assinatura de raiz para gráficos e outra para a computação em um aplicativo. Detalhes de assinatura de raiz são exibidos em uma nova janela de documento, com detalhes da assinatura de raiz dispostos hierarquicamente.  
  
### <a name="d3d12-resources"></a>Recursos de D3D12  
 Recursos Direct3D 12, são captura todos os objetos que fornecem dados para o pipeline de renderização; Isso é diferente de Direct3D11 que muitos objetos específicos para tipos diferentes e dimensões de recursos definidos. Um recurso de Direct3D 12 pode conter dados de textura, dados de vértice, os dados do sombreador e muito mais — podem representar até mesmo os destinos de renderização, como o buffer de profundidade. Detalhes de um recurso de Direct3D 12 são exibidos em uma nova janela de documento. Análise de gráficos usará o visualizador apropriado para o conteúdo do objeto de recurso se ele é capaz de determinar o tipo de. Por exemplo, um objeto de recurso que contém dados de textura é exibido usando o Visualizador de textura, assim como um objeto de D3D11 Texture2D é.  
  
### <a name="device-context-object"></a>Objeto de contexto de dispositivo  
 No Direct3D 11 e 10 Direct3D, o contexto de dispositivo (**o contexto de dispositivo D3D11** ou **dispositivo D3D10**) objeto é particularmente importante porque ele contém as informações de estado mais importantes e vincula a outras objetos de estado que são definidos no momento. Detalhes do contexto de dispositivo são exibidos em uma nova janela de documentos e cada categoria de informações é apresentada em sua própria guia. As alterações de contexto de dispositivo quando um novo evento é selecionado para refletir o estado atual do dispositivo.  
  
### <a name="buffer-object"></a>Objeto de buffer  
 Detalhes do objeto de buffer (Buffer D3D11 ou D3D10) são exibidos em uma nova janela de documento que apresenta o conteúdo de buffer em uma tabela e fornece uma interface para alterar como o conteúdo de buffer é exibido. O **buffer dados** dá suporte à cópia da tabela e colar para que você pode usar outra ferramenta — por exemplo, o Microsoft Excel — para examinar seu conteúdo. O conteúdo do buffer é interpretado de acordo com o valor da **formato** caixa de combinação, que está localizada acima do **de buffer de dados** tabela. Na caixa, você pode inserir um formato de dados compostos que consiste em tipos de dados listados na tabela a seguir. Por exemplo, "float int" exibe uma lista de estruturas que contêm um valor de ponto flutuante de 32 bits seguido por um valor inteiro com sinal de 32 bits. Formatos de dados compostos que você especificou são adicionados à caixa de combinação para uso posterior.  
  
 Você também pode alternar o **Mostrar desloca** caixa de seleção para ocultar ou exibir o deslocamento de cada elemento no buffer.  
  
|Tipo|Descrição|  
|----------|-----------------|  
|**float**|Um valor de ponto flutuante de 32 bits.|  
|**float2**|Um vetor que contém dois valores de ponto flutuante de 32 bits.|  
|**float3**|Um vetor que contém três valores de ponto flutuante de 32 bits.|  
|**FLOAT4**|Um vetor que contém quatro valores de ponto flutuante de 32 bits.|  
|**byte**|Um valor inteiro com sinal de 8 bits.|  
|**2 bytes**|Um valor inteiro com sinal de 16 bits.|  
|**4 bytes**|Um valor inteiro com sinal de 32 bits. Mesmo que **int**.|  
|**8 bytes**|Um valor inteiro com sinal de 64 bits. Mesmo que **int64**.|  
|**xbyte**|Um valor hexadecimal de 8 bits.|  
|**x2byte**|Um valor hexadecimal de 16 bits.|  
|**x4byte**|Um valor hexadecimal de 32 bits. Mesmo que **xint**.|  
|**x8byte**|Um valor hexadecimal de 64 bits. Mesmo que **xint64**.|  
|**ubyte**|Um valor inteiro sem sinal de 8 bits.|  
|**u2byte**|Um valor inteiro sem sinal de 16 bits.|  
|**u4byte**|Um valor inteiro sem sinal de 32 bits. Mesmo que **uint**.|  
|**u8byte**|Um valor inteiro sem sinal de 64 bits. Mesmo que **uint64**.|  
|**metade**|Um valor de ponto flutuante de 16 bits.|  
|**Semestre 2**|Um vetor que contém dois valores de ponto flutuante de 16 bits.|  
|**half3**|Um vetor que contém três valores de ponto flutuante de 16 bits.|  
|**half4**|Um vetor que contém quatro valores de ponto flutuante de 16 bits.|  
|**double**|Um valor de ponto flutuante de 64 bits.|  
|**int**|Um valor inteiro com sinal de 32 bits. Mesmo que **4 bytes**.|  
|**int64**|Um valor inteiro com sinal de 64 bits. Mesmo que **8 bytes**.|  
|**xint**|Um valor hexadecimal de 32 bits. Mesmo que **x4byte**.|  
|**xint64**|Um valor hexadecimal de 64 bits. Mesmo que **x8byte**.|  
|**uint**|Um valor inteiro sem sinal de 32 bits. Mesmo que **u4byte**.|  
|**uint64**|Um valor inteiro sem sinal de 64 bits. Mesmo que **u8byte**.|  
|**bool**|Um valor booleano (`true` ou `false`). Cada valor booleano é representado por um valor de 32 bits.|  
  
## <a name="see-also"></a>Consulte também  
 [Diagnóstico de gráficos (depuração DirectX Graphics)](visual-studio-graphics-diagnostics.md)   
 [Passo a passo: objetos ausentes devido ao estado do dispositivo](walkthrough-missing-objects-due-to-device-state.md)