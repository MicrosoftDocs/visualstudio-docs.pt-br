---
title: Variante de formato de destino de renderização de 16 bpp | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 24b22ad9-5ad0-4161-809a-9b518eb924bf
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bf00bf536e5f1ee140a818ee59c66703906860f0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727635"
---
# <a name="16bpp-render-target-format-variant"></a>Variante de formato de destino de renderização 16bpp
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Define o formato de pixel como DXGI_FORMAT_B5G6R5_UNORM para todos os destinos de renderização e buffers de fundo.  
  
## <a name="interpretation"></a>Interpretação  
 O destino de renderização ou buffer de fundo geralmente usa um formato de 32 bpp (32 bits por pixel), como B8G8R8A8_UNORM. Os formatos de 32 bpp podem consumir muita largura de banda da memória. Como B5G6R5_UNORM é um formato de 16 bpp e tem metade do tamanho dos formatos de 32 bpp, ele pode aliviar a pressão sobre a largura de banda da memória, mas é menos fiel às cores.  
  
 Se essa variante tiver um ganho de desempenho considerável, é provável que o aplicativo consuma muita largura de banda da memória. Os ganhos de desempenho podem ser altos quando o quadro analisado tiver muitos excedentes ou muita combinação alfa.  
  
 Se os tipos de cenas renderizados por seu aplicativo não precisarem de reprodução de cores com alta fidelidade, o destino de renderização não precisar de um canal alfa e os gradientes suaves não forem muito comuns — que são suscetíveis aos artefatos de faixas menos fiéis às cores — você poderá usar o formato de destino de renderização de 16 bpp para diminuir o uso da largura de banda da memória.  
  
 Se as cenas renderizadas no seu aplicativo requerem reprodução de cores com alta fidelidade ou um canal alfa, ou se os gradientes suaves forem comuns, pense em outras estratégias para reduzir o uso de largura de banda da memória — por exemplo, reduza a quantidade de excedentes ou combinação alfa, reduza as dimensões do framebuffer ou modifique os recursos de textura para consumir menos largura de banda da memória ao habilitar a compactação ou reduzir as dimensões. Como sempre, você precisa levar em consideração as concessões em termos de qualidade de imagem que acompanham todas essas otimizações.  
  
 Se o buffer de fundo de 16 bpp for útil para o aplicativo, mas ele fizer parte da sua cadeia de swap, você deve executar outras etapas porque o formato DXGI_FORMAT_B5G6R5_UNORM não é compatível com cadeias de swap criadas com o uso de `D3D11CreateDeviceAndSwapChain` ou `IDXGIFactory::CreateSwapChain`. Como alternativa, você pode criar um destino de renderização no formato B5G6R5_UNORM usando `CreateTexture2D` e renderizar nesse formato. Antes de chamar Present na cadeia de swap, copie o destino de renderização para o buffer de fundo da cadeia de swap. Para isso, desenhe um quadrupleto de tela inteira com o destino de renderização como textura de origem. Embora essa etapa adicional consuma mais largura de banda da memória, a maior parte das operações de renderização vai consumir menos largura de banda porque afetam o destino de renderização de 16 bpp. Se isso economizar mais largura de banda do que a cópia do destino de renderização para o buffer de fundo da cadeia de swap, o desempenho da renderização melhorará.  
  
 As arquiteturas de GPU que usam técnicas de renderização lado a lado obtêm benefícios de desempenho importantes com o uso de um formato de framebuffer de 16 bpp, pois o cache do framebuffer local de cada bloco lado a lado comporta uma porção maior do framebuffer. As arquiteturas de renderização lado a lado podem ser encontradas em GPUs de dispositivos móveis e tablet. Elas raramente são encontradas em outros tipos de dispositivos.  
  
## <a name="remarks"></a>Comentários  
 O formato do destino de renderização é redefinido como DXGI_FORMAT_B5G6R5_UNORM em todas as chamadas de `ID3D11Device::CreateTexture2D` que criam um destino de renderização. O formato é substituído especificamente quando o objeto D3D11_TEXTURE2D_DESC apresentado a pDesc descreve um destino de renderização, ou seja:  
  
-   O membro BindFlags tem o sinalizador D3D11_BIND_REDNER_TARGET definido.  
  
-   O membro BindFlags tem o sinalizador D3D11_BIND_DEPTH_STENCIL desmarcado.  
  
-   O membro Uso está definido como D3D11_USAGE_DEFAULT.  
  
## <a name="restrictions-and-limitations"></a>Restrições e limitações  
 Como o formato B5G6R5 não tem um canal alfa, o conteúdo alfa não é preservado por essa variante. Se a renderização do aplicativo necessitar de um canal alfa no destino de renderização, você não poderá simplesmente alternar para o formato B5G6R5.  
  
## <a name="example"></a>Exemplo  
 O **formato de destino de renderização de 16 bpp** variante pode ser reproduzida para destinos de renderização criados usando `CreateTexture2D` usando código como este:  
  
```  
D3D11_TEXTURE2D_DESC target_description;  
  
target_description.BindFlags = D3D11_BIND_RENDER_TARGET;  
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;  
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);  
```



