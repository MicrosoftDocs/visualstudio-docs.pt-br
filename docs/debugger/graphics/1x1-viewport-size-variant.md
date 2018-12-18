---
title: Tamanho do visor 1x1 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 3dbc3247-00f5-4644-8ff9-72e9febcf09a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 168b358bf58dcb2c91814f5460b203873255e275
ms.sourcegitcommit: 80f9daba96ff76ad7e228eb8716df3abfd115bc3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37433225"
---
# <a name="1x1-viewport-size-variant"></a>Variação de tamanho do visor 1x1
Reduz as dimensões do visor em todos os destinos de renderização para 1 x 1 pixels.  
  
## <a name="interpretation"></a>Interpretação  
 Um visor menor reduz o número de pixels que têm como sombreamento. Mas, um visor menor não reduz o número de vértices que você precise processo. Ao definir as dimensões do visor para 1 × 1, você elimina o sombreamento dos pixels de seu aplicativo.  
  
 Se essa variante mostrar um ganho de desempenho grande, isso pode indicar que seu aplicativo consome muita taxa de preenchimento. Além disso, a resolução pode ser muito alta para a plataforma de destino ou o aplicativo poderia gastar um tempo significativo para sombrear pixels que são substituídos posteriormente, também conhecidos como *exceda*. Um buffer de quadro menor ou reduzir a quantidade de excedentes melhorará o desempenho do aplicativo.  
  
## <a name="remarks"></a>Comentários  
 As dimensões do visor são redefinidas para 1 × 1 pixel após cada chamada de `ID3D11DeviceContext::OMSetRenderTargets` ou `ID3D11DeviceContext::RSSetViewports`.  
  
## <a name="example"></a>Exemplo  
 Essa variante pode ser reproduzido com o código a seguir:  
  
```cpp
D3D11_VIEWPORT viewport;  
viewport.TopLeftX = 0;  
viewport.TopLeftY = 0;  
viewport.Width = 1;  
viewport.Height = 1;  
d3d_context->RSSetViewports(1, &viewport);  
```
