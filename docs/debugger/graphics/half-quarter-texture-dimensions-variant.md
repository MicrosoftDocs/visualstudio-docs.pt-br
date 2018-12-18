---
title: Variante de dimensões de textura de metade / um quarto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 282e9bbb-51aa-4cd0-8e5c-0901268c29e5
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 94820b2930bbe689c37b90443ac007b137f162d6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49870192"
---
# <a name="halfquarter-texture-dimensions-variant"></a>Variante de metade/um quarto nas dimensões de textura
Reduz as dimensões de textura nas texturas que não são destinos de renderização.  
  
## <a name="interpretation"></a>Interpretação  
 Texturas menores ocupam menos memória e, portanto, consomem menos largura de banda de memória e reduzem a pressão no cache de textura de GPU. No entanto, a quantidade inferior de detalhes pode reduzir a qualidade das imagens, especialmente quando são vistas de perto em uma cena 3D ou ampliadas.  
  
 Se essa variante mostrar um grande ganho de desempenho, ela pode indicar que seu aplicativo consome muita largura de banda de memória, utiliza o cache de textura de maneira ineficiente, ou ambos. Também pode indicar que suas texturas ocupam mais memória de GPU do que o disponível, o que faz com que as texturas sejam paginadas para a memória do sistema.  
  
 Se seu aplicativo consumir muita largura de banda de memória ou usar o cache de textura de maneira ineficiente, pense em reduzir o tamanho das texturas, mas somente após considerar habilitar mapas de mip para texturas adequadas. Assim como texturas menores, texturas mapeadas de mip consumem menos largura de banda de memória (embora ocupem mais memória de GPU) e aumentam a utilização do cache, mas não reduzem os detalhes da textura. Recomendamos mapas de mip sempre que o aumento do uso da memória não faça com que as texturas sejam paginadas na memória do sistema.  
  
 Se as texturas ocuparem mais memória GPU do que o disponível, pense em reduzir o tamanho das texturas, mas somente após considerar comprimir texturas adequadas. Assim como as texturas menores, as texturas comprimidas ocupam menos memória e reduzem a necessidade de paginar na memória do sistema, mas sua fidelidade de cor é reduzida. Dependendo do seu conteúdo, a compactação não é adequada para todas as texturas, por exemplo, aquelas que possuem uma variação significativa de cores em uma pequena área. Porém, para muitas texturas, a compactação pode manter a qualidade de imagem geral melhor do que reduzir seu tamanho.  
  
## <a name="remarks"></a>Comentários  
 As dimensões da textura são reduzidas em cada chamada a `ID3D11Device::CreateTexture2D`, que cria uma textura de origem. As dimensões da textura são reduzidas especificamente quando o objeto D3D11_TEXTURE2D_DESC transferido em `pDesc` descreve uma textura usada na renderização; ou seja:  
  
- O membro BindFlags tem apenas o sinalizador D3D11_BIND_SHADER_RESOURCE definido.  
  
- O membro MiscFlags não possui o sinalizador D3D11_RESOURCE_MISC_TILE_POOL ou o conjunto de sinalizadores D3D11_RESOURCE_MISC_TILED (recursos lado a lado não são redimensionados).  
  
- O formato de textura tem suporte como destino de renderização, como determinado por D3D11_FORMAT_SUPPORT_RENDER_TARGET, que é necessário para reduzir o tamanho da textura. Os formatos BC1, BC2 e BC3 também têm suporte, embora não como destinos de renderização.  
  
  Se forem fornecidos dados iniciais pelo aplicativo, essa variante escala os dados da textura para o tamanho adequado antes de criar a textura. Se forem fornecidos dados iniciais em um formato compactado de bloco, somo BC1, BC2 ou BC3, eles são decodificados, escalados e codificados novamente antes de serem usados para criar a textura menor. (A natureza da compactação baseada em blocos significa que o processo de decodificação, escala e codificação extra quase sempre resulta em qualidade inferior da imagem do que quando uma textura compactada em bloco é gerada de uma versão escalada da textura, que não havia sido codificada anteriormente.)  
  
  Se mapas de mip forem habilitados para a textura, a variante reduz o número de nível de mip de maneira equivalente; um a menos ao redimensionar para a metade ou dois a menos ao redimensionar para um quarto.  
  
## <a name="example"></a>Exemplo  
 Essa variante redimensiona as texturas no tempo de execução antes da chamada para `CreateTexture2D`. Não recomendamos essa abordagem para códigos de produção, pois as texturas em tamanho integral consomem mais espaço em disco e a etapa adicional pode aumentar o tempo de carregamento no aplicativo, especialmente no caso de texturas compactadas, que requerem recursos computacionais significativos para codificação. Ao invés disso, recomendamos que você redimensione as texturas offline usando um editor de imagens ou um processador de imagem que faça parte do seu pipeline de compilação. Essas abordagens reduzem os requisitos de espaço em disco e eliminam a sobrecarga do tempo de execução no aplicativo, além de oferecer mais tempo de processamento para que seja possível manter a melhor qualidade de imagem ao reduzir ou compactar as texturas.  
  
## <a name="see-also"></a>Consulte também  
 [Variante de geração de MIP-map](mip-map-generation-variant.md)   
 [Variante de compressão de textura BC](bc-texture-compression-variant.md)