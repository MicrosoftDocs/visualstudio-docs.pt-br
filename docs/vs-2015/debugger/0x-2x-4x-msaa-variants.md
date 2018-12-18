---
title: Variantes de MSAA x-4 x-2 0 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 668a6603-5082-4c78-98e6-f3dc871aa55b
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8e661823a07945c22679832dc716ad2f25f4f6aa
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793770"
---
# <a name="0x2x4x-msaa-variants"></a>Variantes MSAA 0x/2x/4x
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Substitui a MSAA (suavização de múltipla amostra) em todos os destinos de renderização e cadeias de troca.  
  
## <a name="interpretation"></a>Interpretação  
 A suavização de múltipla amostra aumenta a qualidade visual colhendo amostras em vários locais e cada pixel; níveis mais altos de MSAA colhem mais amostras, e sem MSAA, somente uma amostra é colhida do centro do pixel. Habilitar MSAA em seu aplicativo geralmente afeta de maneira modesta, porém notável, o desempenho de renderização; mas em determinadas cargas de trabalho ou em determinadas GPUs, ele quase não oferece impacto.  
  
 Se seu aplicativo já tem MSAA habilitado, então as variantes de MSAA mais inferiores indicam o custo sobre o desempenho relativo incorrido pelo MSAA existente de mais alto nível. Em particular, a variante MSAA de 0x indica o desempenho relativo de seu aplicativo sem MSAA.  
  
 Se seu aplicativo ainda não tem MSAA habilitado, então as variantes de MSAA de 2x e 4x indicam o custo sobre o desempenho relativo de habilitá-las em seu aplicativo. Quando o custo for aceitavelmente baixo, considere habilitar MSAA para aprimorar a qualidade de imagem do seu aplicativo.  
  
> [!NOTE]
>  Seu hardware pode não oferecer suporte completo a MSAA para todos os formatos. Se uma dessas variantes encontrar uma limitação de hardware que não tenha uma solução alternativa, sua coluna na tabela de resumo de desempenho estará em brando e uma mensagem de erro será produzida.  
  
## <a name="remarks"></a>Comentários  
 Essas variantes substituem a contagem de amostra e os argumentos de qualidade de amostra em chamadas para `ID3DDevice::CreateTexture2D` que criam destinos de renderização. Especificamente, esses parâmetros são substituídos quando:  
  
- O objeto `D3D11_TEXTURE2D_DESC` transmitido em `pDesc` descreve um destino de renderização; ou seja:  
  
  -   O membro BindFlags possui o sinalizador D3D11_BIND_TARGET ou D3D11_BIND_DEPTH_STENCIL definido.  
  
  -   O membro Uso está definido como D3D11_USAGE_DEFAULT.  
  
  -   O membro CPUAccessFlags é definido como 0.  
  
  -   O membro MipLevels é definido como 1.  
  
- O dispositivo oferece suporte à contagem de amostra solicitada (0, 2 ou 4) e à qualidade da amostra (0) para o formato do destino de renderização solicitado (membro D3D11_TEXTURE2D_DESC::Format), como determinado por `ID3D11Device::CheckMultisampleQualityLevels`.  
  
  Se o membro D3D11_TEXTURE2D_DESC::BindFlags tiver um sinalizador D3D_BIND_SHADER_RESOUCE ou D3D11_BIND_UNORDERED_ACCESS definido, então são criadas duas versões da textura; a primeira tem esses sinalizadores liberados para uso como o destino de renderização, e a outra é uma textura não MSAA, na qual esses sinalizadores são deixados intactos para agirem como um buffer de resolução para a primeira versão. Isso é necessário porque o uso de uma textura MSAA como um recurso de sombreador ou para acesso não ordenado provavelmente não será válido; por exemplo, um sombreador que agisse sobre ela geraria resultados incorretos, pois esperaria uma textura não MSAA. Se a variante tiver criado a textura não MSAA secundária, então sempre que o destino de renderização MSAA não for definido do contexto do dispositivo, seu conteúdo será resolvido na textura não MSAA. Da mesma forma, sempre que o destino de renderização MSAA for vinculado como um recurso do sombreador ou usado em uma exibição de acesso não ordenada, a textura não MSAA resolvida é vinculada em seu lugar.  
  
  Essas variantes também substituem as definições de MSAA em todas as cadeias de troca criadas usando `IDXGIFactory::CreateSwapChain`, `IDXGIFactory2::CreateSwapChainForHwnd`, `IDXGIFactory2::CreateSwapChainForCoreWindow`, `IDXGIFactory2::CreateSwapChainForComposition` e `ID3D11CreateDeviceAndSwapChain`.  
  
  O efeito real dessas alterações é que toda a renderização é realizada em um destino de renderização MSAA, mas se seu aplicativo usar um desses destinos de renderização ou buffers de cadeia de troca como uma exibição de recurso do sombreador ou uma exibição de acesso não ordenada, então os dados são amostrados a partir da cópia não MSAA resolvida do destino de renderização.  
  
## <a name="restrictions-and-limitations"></a>Restrições e limitações  
 No Direct3D11, as texturas MSAA são mais restritas do que texturas não MSAA. Por exemplo, você não pode chamar `ID3D11DeviceContext::UpdateSubresource` em uma textura MSAA, e chamar `ID3D11DeviceContext::CopySubresourceRegion` falhará se a contagem de amostra e a qualidade da amostra do recurso de origem e do recurso de destino não forem correspondentes, o que pode ocorrer quando essa variante substitui as definições de MSAA de um recurso, mas não de outro.  
  
 Quando a reprodução detecta esses tipos de conflitos, ela se esforça para replicar o comportamento pretendido, mas pode não ser possível reproduzir os resultados de maneira exata. Embora isso geralmente não afete o desempenho dessas variantes de maneira que seu impacto seja representado de forma inadequada, é possível que isso aconteça, por exemplo, quando o controle do fluxo em um sombreador de pixel é determinado de acordo com o conteúdo preciso de uma textura, pois a textura replicada pode não ter conteúdos idênticos.  
  
## <a name="example"></a>Exemplo  
 Essas variantes podem ser reproduzidas para destinos de renderização criados usando `ID3D11Device::CreateTexture2D` ao utilizar um código como esse:  
  
```  
D3D11_TEXTURE2D_DESC target_description;  
target_description.BindFlags = D3D11_BIND_RENDER_TARGET;  
target_description.SampleDesc.Count = 4; // 4x MSAA, can be 2 or 0 instead  
target_description.SampleDesc.Quality = 0;  
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);  
```  
  
## <a name="example"></a>Exemplo  
 Ou para cadeias de troca criadas usando IDXGISwapChain::CreateSwapChain ou D3D11CreateDeviceAndSwapChain ao utilizar um código como esse:  
  
```  
DXGI_SWAP_CHAIN_DESC chain_description;  
chain_description.SampleDesc.Count = 4; // 4x MSAA, can be 2 or 0 instead  
chain_description.SampleDesc.Quality = 0;  
  
// Call IDXGISwapChain::CreateSwapChain or D3D11CreateDeviceAndSwapChain, etc.  
```



