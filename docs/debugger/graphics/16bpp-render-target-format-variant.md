---
title: Variante de formato de destino de renderização de 16 bpp | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 24b22ad9-5ad0-4161-809a-9b518eb924bf
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f9c72abaaf1a799316686c77b127952f1fe4f689
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49832882"
---
# <a name="16-bpp-render-target-format-variant"></a>Renderizar destino formato variantes de 16 bpp
Define o formato de pixel como DXGI_FORMAT_B5G6R5_UNORM para todos os destinos de renderização e buffers de fundo.  
  
## <a name="interpretation"></a>Interpretação  
 Destino de renderização ou buffer de fundo geralmente usa um formato de 32 bpp (32 bits por pixel), como B8G8R8A8_UNORM. formatos de 32 bpp podem consumir uma grande quantidade de largura de banda de memória. Como o formato B5G6R5_UNORM é um formato de 16 bpp é metade do tamanho dos formatos de 32 bpp, usá-lo pode aliviar a pressão de largura de banda de memória, mas fiel às cores.  
  
 Se essa variante tiver um ganho de desempenho considerável, é provável que o aplicativo consuma muita largura de banda da memória. Você pode obter melhorias significativas de desempenho, especialmente quando o quadro analisado tiver uma quantidade significativa de excedentes ou combinação alfa.

Um formato de destino de renderização de 16 bpp pode reduzir a banda de memória com o uso quando seu aplicativo tem as seguintes condições:
- Não exige a reprodução de cores de alta fidelidade.
- Não requer um canal alfa.
- Ofent não tem os gradientes suaves (que são suscetíveis aos artefatos de faixas em fidelidade de cor reduzida).

Outras estratégias para reduzir a largura de banda de memória incluem:
- Reduza a quantidade de excedentes ou combinação alfa.
- Reduza as dimensões do buffer de quadro.
- Reduza as dimensões de recursos de textura.
- Reduza compressões de recursos de textura.
 
Como sempre, você precisa levar em consideração as concessões em termos de qualidade de imagem que acompanham todas essas otimizações.  

Aplicativos que fazem parte de uma cadeia de troca tem um formato de buffer de fundo (DXGI_FORMAT_B5G6R5_UNORM) que não oferece suporte a 16 bpp. Essas cadeias de troca criadas usando `D3D11CreateDeviceAndSwapChain` ou `IDXGIFactory::CreateSwapChain`. Para contornar essa limitação, execute as seguintes etapas:
1. Criar um destino de renderização do formato B5G6R5_UNORM usando `CreateTexture2D` e renderizar a esse destino. 
2. Copie o destino de renderização para o buffer de fundo da cadeia de troca desenhando um quadrupleto de tela inteira com o destino de renderização como textura de origem.
3. Chame Present na cadeia de swap.

   Se essa estratégia economiza largura de banda mais do que é consumido, copiando o destino de renderização para o buffer de fundo da cadeia de troca, desempenho de renderização é aprimorado.

   Arquiteturas de GPU que usam técnicas de renderização lado a lado podem ver os benefícios significativos de desempenho usando um formato de buffer de quadro de 16 bpp. Essa melhoria é porque uma porção maior do que o buffer de quadro pode caber no cache de buffer de quadro de local de cada bloco. As arquiteturas de renderização lado a lado podem ser encontradas em GPUs de dispositivos móveis e tablet. Elas raramente são encontradas em outros tipos de dispositivos.  
  
## <a name="remarks"></a>Comentários  
 O formato do destino de renderização é redefinido como DXGI_FORMAT_B5G6R5_UNORM em todas as chamadas de `ID3D11Device::CreateTexture2D` que criam um destino de renderização. O formato é substituído especificamente quando o objeto D3D11_TEXTURE2D_DESC apresentado a pDesc descreve um destino de renderização, ou seja:  
  
-   O membro BindFlags tem o sinalizador D3D11_BIND_REDNER_TARGET definido.  
  
-   O membro BindFlags tem o sinalizador D3D11_BIND_DEPTH_STENCIL desmarcado.  
  
-   O membro Uso está definido como D3D11_USAGE_DEFAULT.  
  
## <a name="restrictions-and-limitations"></a>Restrições e limitações  
 Como o formato B5G6R5 não tem um canal alfa, o conteúdo alfa não é preservado por essa variante. Se a renderização do aplicativo necessitar de um canal alfa no destino de renderização, você não poderá simplesmente alternar para o formato B5G6R5.  
  
## <a name="example"></a>Exemplo  
 O **formato de destino de renderização de 16 bpp** variante pode ser reproduzida para destinos de renderização criados usando `CreateTexture2D` usando código como este:  
  
```cpp
D3D11_TEXTURE2D_DESC target_description;  
  
target_description.BindFlags = D3D11_BIND_RENDER_TARGET;  
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;  
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);  
```
