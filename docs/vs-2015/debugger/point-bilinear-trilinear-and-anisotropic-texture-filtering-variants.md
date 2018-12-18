---
title: Ponto, Bilinear, Trilinear e Anisotrópica textura variantes de filtragem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 57d14fc9-b5f7-45ee-9717-48086886742d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ef054b1773b1f0d07e21ec25cb326594a4d3b2d9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791222"
---
# <a name="point-bilinear-trilinear-and-anisotropic-texture-filtering-variants"></a>Variantes de filtragem de textura de ponto, bilinear, trilinear e anisotrópico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Substitui o modo de filtragem em amostras adequadas de textura.  
  
## <a name="interpretation"></a>Interpretação  
 Diferentes métodos de amostragem de textura possuem diferentes custos de desempenho e qualidade de imagem. Na ordem crescente de custo, e de qualidade visual, os modos de filtragem são:  
  
1. Filtragem de ponto (mais barata, pior qualidade visual)  
  
2. Filtragem bilinear  
  
3. Filtragem trilinear  
  
4. Filtragem anisotrópica (mais cara, melhor qualidade visual)  
  
   Se o custo de desempenho de cada variante for significativo ou aumentar com modos de filtragem mais intensos, você pode relacionar o custo à melhor qualidade de imagem. Com base em sua avaliação, você pode aceitar custos de desempenho adicionais para aumentar a qualidade visual ou aceitar uma qualidade visual menor para atingir uma taxa de quadro mais alta ou ganhar mais desempenho, que pode ser usado de outras maneiras.  
  
   Se você achar que o custo de desempenho é insignificante ou permanece estável independentemente do modo de filtragem, por exemplo, quando a GPU de destino possui muito rendimento de sombreador ou largura de banda de memória, considere usar a filtragem anisotrópica para alcançar a melhor qualidade de imagem em seu aplicativo.  
  
## <a name="remarks"></a>Comentários  
 Essas variantes substituem os estados de amostra em chamadas para `ID3D11DeviceContext::PSSetSamplers` nas quais o modo de filtragem fornecido pelo aplicativo é um dos seguintes:  
  
- `D3D11_FILTER_MIN_MAG_MIP_POINT`  
  
- `D3D11_FILTER_MIN_MAG_POINT_MIP_LINEAR`  
  
- `D3D11_FILTER_MIN_POINT_MAG_LINEAR_MIP_POINT`  
  
- `D3D11_FILTER_MIN_POINT_MAG_MIP_LINEAR`  
  
- `D3D11_FILTER_MIN_LINEAR_MAG_MIP_POINT`  
  
- `D3D11_FILTER_MIN_LINEAR_MAG_POINT_MIP_LINEAR`  
  
- `D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT`  
  
- `D3D11_FILTER_MIN_MAG_MIP_LINEAR`  
  
- `D3D11_FILTER_ANISOTROPIC`  
  
  No **filtragem de textura de ponto** variant, o modo de filtragem fornecido pelo aplicativo é substituído por `D3D11_FILTER_MIN_MAG_MIP_POINT`; na **filtragem de textura Bilinear** variant, ele será substituído pelo `D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT`; e, na **filtragem de textura Trilinear** variant, ele será substituído pelo `D3D11_FILTER_MIN_MAG_MIP_LINEAR`.  
  
  No **filtragem de textura Anisotrópica** variant, o modo de filtragem fornecido pelo aplicativo é substituído por `D3D11_FILTER_ANISOTROPIC`, e a Anisotropy máxima é definida como 16.  
  
## <a name="restrictions-and-limitations"></a>Restrições e limitações  
 No Direct3D, o nível de recurso 9.1 especifica uma anisotropia máxima de 2x. Porque o **filtragem de textura Anisotrópica** variante tenta usar a anisotropia de 16x exclusivamente, a reprodução falha quando a análise de quadro é executada em um dispositivo de nível de recurso 9.1. Dispositivos contemporâneos que são afetados por essa limitação incluem os tablets Windows Surface RT e Surface 2 baseados em ARM. GPUs mais antigas que ainda podem ser encontradas em alguns computadores também podem ser afetadas, mas elas são consideradas bastante obsoletas e cada vez mais incomuns.  
  
## <a name="example"></a>Exemplo  
 O **filtragem de textura de ponto** variante pode ser reproduzida usando códigos da seguinte forma:  
  
```  
D3D11_SAMPLER_DESC sampler_description;  
  
// ... other sampler description setup ...  
  
sampler_description.Filter = D3D11_FILTER_MIN_MAG_MIP_POINT;  
  
d3d_device->CreateSamplerState(&sampler_desc, &sampler);  
d3d_context->PSSetSamplers(0, 1, &sampler  
```  
  
## <a name="example"></a>Exemplo  
 O **filtragem de textura Bilinear** variante pode ser reproduzida usando códigos da seguinte forma:  
  
```  
D3D11_SAMPLER_DESC sampler_description;   
  
// ... other sampler description setup ...  
  
sampler_description.Filter = D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT;  
  
d3d_device->CreateSamplerState(&sampler_desc, &sampler);  
d3d_context->PSSetSamplers(0, 1, &sampler  
```  
  
## <a name="example"></a>Exemplo  
 O **filtragem de textura Trilinear** variante pode ser reproduzida usando códigos da seguinte forma:  
  
```  
D3D11_SAMPLER_DESC sampler_description;   
  
// ... other sampler description setup ...  
  
sampler_description.Filter = D3D11_FILTER_MIN_MAG_MIP_LINEAR;  
  
d3d_device->CreateSamplerState(&sampler_desc, &sampler);  
d3d_context->PSSetSamplers(0, 1, &sampler  
```  
  
## <a name="example"></a>Exemplo  
 O **filtragem de textura Anisotrópica** variante pode ser reproduzida usando códigos da seguinte forma:  
  
```  
D3D11_SAMPLER_DESC sampler_description;   
  
// ... other sampler description setup ...  
  
sampler_description.Filter = D3D11_FILTER_ANISOTROPIC;  
sampler_description.MaxAnisotropy = 16;  
  
d3d_device->CreateSamplerState(&sampler_desc, &sampler);  
d3d_context->PSSetSamplers(0, 1, &sampler  
```



