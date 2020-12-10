---
title: MIP – variante de geração de mapa | Microsoft Docs
description: Se a geração de mapa MIP mostrar grandes ganhos de desempenho, isso indica que você está usando texturas sem habilitar os mapas MIP e não obter o máximo do cache de textura.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3b4b3583-0b01-4f5d-aacb-3f96d19111d9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d939fb537ac6aed75d9b0f7bda2970a85f9175ad
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994961"
---
# <a name="mip-map-generation-variant"></a>Variante de geração de Mip-map
Habilita mapas mip em texturas que não são destinos de renderização.

## <a name="interpretation"></a>Interpretação
Os mapas mip são usados principalmente para eliminar artefatos de suavização das texturas que estão passando por minificação. Isso é possível com o cálculo prévio de versões menores da textura. Embora essas texturas adicionais consumam cerca de 33% mais memória da GPU que a textura original, elas também são mais eficientes porque o cache da textura da GPU comporta uma área de superfície maior dessa textura, o que faz com que seu conteúdo seja mais utilizado.

Recomendamos usar mapas mip nas cenas 3D quando houver memória disponível para armazenar texturas adicionais porque eles aumentam o desempenho da renderização e a qualidade da imagem.

Se essa variante tiver um ganho de desempenho considerável, é sinal de que você está usando as texturas sem habilitar os mapas mip e, por isso, não está aproveitando ao máximo o cache da textura.

## <a name="remarks"></a>Comentários
A geração do mapa mip é forçada em cada chamada de `ID3D11Device::CreateTexture2D` que cria uma textura de origem. Especificamente, a geração de mapa MIP é forçada quando o objeto de D3D11_TEXTURE2D_DESC passado `pDesc` descreve um recurso de sombreador inalterável; isto é:

- O membro BindFlags tem apenas o sinalizador D3D11_BIND_SHADER_RESOURCE definido.

- O membro Uso está definido como D3D11_USAGE_DEFAULT ou D3D11_USAGE_IMMUTABLE.

- O membro CPUAccessFlags está definido como 0 (sem acesso à CPU).

- O membro SampleDesc tem seu membro Count definido como 1 (sem MSAA (suavização de amostra múltipla)).

- O membro MipLevels está definido como 1 (não há mapas mip).

  Quando o aplicativo fornece os dados iniciais, o formato da textura deve permitir a geração de mapas mip automaticamente — conforme determinado por D3D11_FORMAT_SUPPORT_MIP_AUTOGEN —, a menos que o formato usado seja BC1, BC2 ou BC3. Caso contrário, a textura não é modificada e o mapa mip não é gerado após o fornecimento dos dados iniciais.

  Quando há mapas mip gerados automaticamente para uma textura, as chamadas de `ID3D11Device::CreateShaderResourceView` são modificadas durante a reprodução para usar a cadeia de mip durante a amostragem da textura.

## <a name="example"></a>Exemplo
A variante **Geração de Mapa Mip** pode ser reproduzida pelo uso de um código como este:

```cpp
D3D11_TEXTURE2D_DESC texture_description;

// ...

texture_description.MipLevels = 0; // generate a full mipchain

std::vector<D3D11_SUBRESOURCE_DATA> initial_data(num_mips);

for (auto&& mip_level : initial_data)
{
    // fill mip_level with the application-supplied initial data
}

d3d_device->CreateTexture2D(&texture_description, initial_data.data(), &texture)
```

Para criar uma textura com cadeia de mip completa, defina `D3D11_TEXTURE2D_DESC::MipLevels` como 0. O número de níveis MIP em uma cadeia MIP completa é Floor (log2 (n) + 1), em que n é a maior dimensão da textura.

Lembre-se de que ao fornecer os dados iniciais para `CreateTexture2D`, você também deve fornecer um objeto D3D11_SUBRESOURCE_DATA para cada nível de mip.

> [!NOTE]
> Se quiser fornecer seu próprio conteúdo aos níveis de mip em vez de gerá-lo automaticamente, crie as texturas usando um editor de imagens compatível com texturas com mapas mip. Em seguida, carregue o arquivo e transmita os níveis de mip a `CreateTexture2D`.

## <a name="see-also"></a>Confira também
[Variante de dimensões de textura de semestre/trimestre](half-quarter-texture-dimensions-variant.md)
