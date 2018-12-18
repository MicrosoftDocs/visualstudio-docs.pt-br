---
title: Variante de compressão de textura BC | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 2d0f5305-585b-4b01-bc9a-7a32d6e991da
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 919191ec29ad45a8385d32b82de99d44fcdaa2ea
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49922439"
---
# <a name="bc-texture-compression-variant"></a>Variante de compressão de textura BC
Habilita a compactação do bloco em texturas cujo formato de pixel é uma variação de B8G8R8X8, B8G8R8A8 ou R8G8B8A8.  
  
## <a name="interpretation"></a>Interpretação  
 Os formatos de compactação em bloco, como BC1, BC2 e BC3, ocupam menos espaço na memória do que os formatos de imagem não compactados e, por isso, consomem menos largura de banda de memória. Quando compactado, o formato BC1 (anteriormente conhecido como DXT1) fica oito vezes menor que os formatos não compactados que usam 32 bits por pixel. Já o formato BC3 (anteriormente conhecido como DXT5) fica quatro vezes menor. A diferença entre os formatos BC1 e BC3 é que o BC3 é compatível com canal alfa com compactação em bloco e o BC1, não. Apesar da alta proporção de compactação, a redução da qualidade de imagem das texturas comuns é mínima. No entanto, a compactação do bloco de alguns tipos de textura — por exemplo, as texturas que têm variações de cor consideráveis em uma pequena área — pode apresentar resultados inaceitáveis.  
  
 Se as texturas forem adequadas para a compactação em bloco e não for necessário manter a fidelidade exata com as cores, você pode usar um formato compactado em bloco para reduzir o uso da memória e consumir menos largura de banda.  
  
## <a name="remarks"></a>Comentários  
 Para compactar texturas, use um formato de compactação em bloco em cada chamada de `ID3DDevice::CreateTexture2D`, que cria uma textura de origem. As texturas são compactadas quando:  
  
- O objeto `D3D11_TEXTURE2D_DESC` apresentado a `pDesc` descreve um recurso do sombreador inalterável, ou seja:  
  
  -   O membro BindFlags tem apenas o sinalizador D3D11_BIND_SHADER_RESOURCE definido.  
  
  -   O membro Uso está definido como D3D11_USAGE_DEFAULT ou D3D11_USAGE_IMMUTABLE.  
  
  -   O membro CPUAccessFlags está definido como 0 (sem acesso à CPU).  
  
  -   O membro SamplerDesc tem seu membro Count definido como 1 (sem MSAA (suavização de amostra múltipla)).  
  
- Os dados iniciais são fornecidos para a chamada de `CreateTexture2D`.  
  
  Estes são os formatos de origem compatíveis e seus respectivos formatos compactados em blocos:  
  
|Formato original (de)|Formato compactado (para)|  
|------------------------------|------------------------------|  
|`DXGI_FORMAT_B8G8R8X8_UNORM`|BC1 (antigo DXT1)|  
|`DXGI_FORMAT_B8G8R8X8_UNORM_SRGB`|BC1|  
|`DXGI_FORMAT_B8G8R8X8_TYPELESS`|BC1|  
|`DXGI_FORMAT_B8G8R8A8_UNORM`|BC3 (antigo DXT5)|  
|`DXGI_FORMAT_B8G8R8A8_UNORM_SRGB`|BC3|  
|`DXGI_FORMAT_B8G8R8A8_TYPELESS`|BC3|  
|`DXGI_FORMAT_R8G8B8A8_UNORM`|BC3|  
|`DXGI_FORMAT_R8G8B8A8_UNORM_SRGB`|BC3|  
|`DXGI_FORMAT_R8G8B8A8_TYPELESS`|BC3|  
  
 Se o formato da sua textura não consta nessa tabela, a textura não foi modificada.  
  
## <a name="restrictions-and-limitations"></a>Restrições e limitações  
 No momento, algumas texturas criadas com formatos de imagens que são variações de B8G8R8A8 ou R8G8B8A8 não usam o canal alfa, mas a variante não tem como obter essa informação. Para manter a exatidão caso o canal alfa seja usado, a variante sempre codifica esses formatos em um formato BC3 menos eficiente. Você pode ajudar a Análise de quadros de gráficos a compreender melhor o potencial de desempenho de renderização de seu aplicativo com essa variante. Para isso, use uma variação do formato de imagem B8G8R8X8 quando não estiver usando o canal alfa para que a variante possa usar o formato BC1, que é mais eficiente.  
  
## <a name="example"></a>Exemplo  
 Essa variante compacta as texturas em blocos no tempo de execução, antes da chamada de `CreateTexture2D`. Essa abordagem não é recomendada para códigos de produção porque as texturas não compactadas consomem mais espaço em disco. Além disso, a etapa adicional necessária pode aumentar consideravelmente o tempo de carregamento no aplicativo porque a compactação em blocos requer muitos recursos computacionais para realizar a codificação. Em vez disso, recomendamos que você faça a compactação das texturas quando não estiver conectado, usando um editor ou processador de imagens que faça parte do pipeline da sua compilação. Essas abordagens diminuem o espaço necessário em disco, eliminam a sobrecarga do tempo de execução no aplicativo e proporcionam mais tempo de processamento para que as imagens tenham a melhor qualidade possível.  
  
## <a name="see-also"></a>Consulte também  
 [Variante de metade/um quarto nas dimensões de textura](half-quarter-texture-dimensions-variant.md)