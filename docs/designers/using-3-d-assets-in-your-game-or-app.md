---
title: Usando ativos 3D em seu jogo ou aplicativo
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- VC.Project.ImageContentTask.ContentOutput
- VC.Project.MeshContentTask.ContentOutput
- VC.Project.ImageContentTask.GeneratePremultipliedAlpha
- VC.Project.ImageContentTask.Compress
- VC.Project.ShaderGraphContentTask.ContentOutput
- VC.Project.ImageContentTask.GenerateMips
ms.assetid: ea587909-e434-46a8-abf8-9b3e95a58b4f
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3821262a456f9e3e764555fce5fc883b42d4ae9e
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768650"
---
# <a name="how-to-use-3d-assets-in-your-game-or-app"></a>Como: Usar ativos 3D em seu jogo ou aplicativo

Este artigo descreve como é possível usar o Visual Studio para processar ativos 3D e incluí-los nos builds.

Depois de usar as ferramentas no Visual Studio para criar ativos 3D, a próxima etapa é usá-las no aplicativo. Mas antes de usá-las, os ativos precisam ser transformados em um formato que possa ser reconhecido pelo DirectX. Para ajudá-lo a transformar seus ativos, o Visual Studio fornece personalizações de build para cada tipo de ativo que pode ser produzido. Para incluir os ativos na sua compilação, tudo o que você precisa fazer é configurar o projeto para usar as personalizações de compilação, adicionar os ativos ao seu projeto e configurar os ativos para usar a personalização de compilação correta. Depois disso, você pode carregar os ativos no aplicativo e usá-los criando e preenchendo recursos do DirectX, assim como faria em qualquer outro aplicativo DirectX.

## <a name="configure-your-project"></a>Configurar seu projeto

Antes que seja possível implantar os ativos 3D como parte da criação, o Visual Studio precisa conhecer os tipos de ativos que você deseja implantar. O Visual Studio já conhece muitos tipos de arquivo comuns, mas como apenas certos tipos de aplicativos usam ativos 3D, o Visual Studio não presume que um projeto crie esses tipos de arquivos. Você pode dizer ao Visual Studio que seu aplicativo usa esses tipos de ativos usando as *personalizações de build* (arquivos que dizem ao Visual Studio como processar tipos diferentes de arquivos de maneira útil), que são fornecidas para cada tipo de ativo. Como essas personalizações são aplicadas por projeto, tudo o que você precisa fazer é adicionar as personalizações adequadas ao seu projeto.

### <a name="to-add-the-build-customizations-to-your-project"></a>Para adicionar as personalizações de compilação ao seu projeto

1. No **Gerenciador de Soluções**, abra o menu de atalho do projeto e, em seguida, escolha **Dependências de Build** > **Personalizações de Build**.

   A caixa de diálogo **Arquivos de Personalizações de Build do Visual C++** será exibida.

2. Em **Arquivos de Personalização de Build Disponíveis**, marque as caixas de seleção que correspondem aos tipos de ativo que você deseja usar no projeto, conforme descrito na seguinte tabela:

    |Tipo de ativo|Nome da personalização de compilação|
    |----------------| - |
    |Texturas e imagens|**ImageContentTask(.targets, .props)**|
    |Modelos 3D|**MeshContentTask(.targets, .props)**|
    |Sombreadores|**ShaderGraphContentTask(.targets, .props)**|

3. Clique no botão **OK**.

## <a name="include-assets-in-your-build"></a>Incluir ativos na criação

Agora que seu projeto conhece os diferentes tipos de ativos 3D que você deseja usar, a próxima etapa será dizer quais arquivos são ativos 3D e quais tipos de ativos eles são.

### <a name="to-add-an-asset-to-your-build"></a>Para adicionar um ativo à sua compilação

1. No **Gerenciador de Soluções**, no seu projeto, abra o menu de atalho do ativo e selecione **Propriedades**.

   A caixa de diálogo **Página de Propriedades** do ativo é exibida.

2. Verifique se as propriedades **Configuração** e **Plataforma** estão definidas com os valores aos quais você deseja aplicar as alterações.

3. Em **Propriedades da Configuração**, escolha **Geral** e, na grade de propriedades, em **Geral**, defina a propriedade **Tipo de Item** para o tipo de item do pipeline de conteúdo adequado. Por exemplo, no caso um arquivo de imagem ou de textura, escolha **Pipeline de Conteúdo da Imagem**.

    > [!IMPORTANT]
    > Por padrão, o Visual Studio presume que muitos tipos de arquivos de imagem devem ser classificados usando o tipo de item **Imagem**, integrado ao Visual Studio. Portanto, você precisa alterar a propriedade **Tipo de Item** de cada imagem que deseja que seja processada pelo pipeline de conteúdo da imagem. Outros tipos de arquivos de origem de pipeline de conteúdo para modelos 3D e gráficos de sombreador visual assumem como padrão o **Tipo de Item** correto.

4. Clique no botão **OK**.

Veja a seguir os três tipos de item de pipeline de conteúdo e seus tipos de arquivo de origem e de saída associados.

|Tipo de item|Tipos de arquivo de origem|Formato do arquivo de saída|
|---------------| - | - |
|**Pipeline de conteúdo da imagem**|Formato PNG (*.png*)<br /><br /> JPEG (*.jpg*, *.jpeg*, *.jpe*, *.jfif*)<br /><br /> Direct Draw Surface (*.dds*)<br /><br /> Graphics Interchange Format (*.gif*)<br /><br /> Bitmap (*.bmp*, *.dib*)<br /><br /> Formato TIFF (*.tif*, *.tiff*)<br /><br /> Formato TGA (*.tga*)|DirectDraw Surface (*.dds*)|
|**Pipeline de conteúdo da malha**|Arquivo de Intercâmbio AutoDesk FBX (*.fbx*)<br /><br /> Arquivo Collada DAE (*.dae*)<br /><br /> Arquivo Wavefront OBJ (*.obj*)|Arquivo de malha 3D (*.cmo*)|
|**Pipeline de conteúdo do sombreador**|Visual Shader Graph (*.dgsl*)|Saída do Sombreador Compilado (*.cso*)|

## <a name="configure-asset-content-pipeline-properties"></a>Configurar ativos do pipeline de conteúdo do ativo

É possível definir as propriedades do pipeline de cada arquivo de ativo de modo que eles sejam compilados de maneira específica.

### <a name="to-configure-content-pipeline-properties"></a>Para configurar as propriedades de pipeline de conteúdo

1. No **Gerenciador de Soluções**, no seu projeto, abra o menu de atalho para o arquivo do ativo e selecione **Propriedades**.

   A caixa de diálogo **Página de Propriedades** do ativo é exibida.

2. Verifique se as propriedades **Configuração** e **Plataforma** estão definidas para os valores aos quais você deseja aplicar as suas alterações.

3. Em **Propriedades de configuração**, escolha o nó do pipeline de conteúdo (por exemplo, **Pipeline de conteúdo de imagem** para ativos de textura e imagens) e, em seguida, na grade de propriedades, defina as propriedades para os valores apropriados. Por exemplo, para gerar mipmaps para um ativo de textura no tempo de build, defina a propriedade **Gerar Mips** como **Sim**.

4. Clique no botão **OK**.

### <a name="image-content-pipeline-configuration"></a>Configuração do pipeline de conteúdo da imagem

Ao usar a ferramenta de pipeline de conteúdo da imagem para compilar um ativo de textura, é possível compactar a textura de várias maneiras, indicar se os níveis de MIP devem ser gerados no tempo de compilação e alterar o nome do arquivo de saída.

|Propriedade|Descrição|
|--------------|-----------------|
|**Compactar**|Especifica o tipo de compactação usado para o arquivo de saída.<br /><br /> As opções disponíveis são:<br /><br /> -   **Sem compactação**<br />-   **Compactação de BC1_UNORM**<br />-   **Compactação BC1_UNORM_SRGB**<br />-   **Compactação de BC2_UNORM**<br />-   **Compactação BC2_UNORM_SRGB**<br />-   **Compactação de BC3_UNORM**<br />-   **Compactação BC3_UNORM_SRGB**<br />-   **Compactação BC4_UNORM**<br />-   **Compactação BC4_SNORM**<br />-   **Compactação BC5_UNORM**<br />-   **Compactação BC5_SNORM**<br />-   **Compactação BC6H_UF16**<br />-   **Compactação BC6H_SF16**<br />-   **Compactação BC7_UNORM**<br />-   **Compactação BC7_UNORM_SRGB**<br /><br /> Para obter informações sobre quais formatos de compactação têm suporte em diferentes versões do DirectX, consulte [Guia de programação para DXGI](/windows/win32/direct3ddxgi/dx-graphics-dxgi-overviews).|
|Converter para formato alfa pré-multiplicado|**Sim** para converter a imagem para um formato alfa pré-multiplicado no arquivo de saída; caso contrário, **Não**. Apenas o arquivo de saída é alterado, a imagem de origem permanece inalterada.|
|**Gerar Mips**|**Sim** para gerar uma cadeia de MIP completa no tempo de build no arquivo de saída; caso contrário, **Não**. Se **Não** e o arquivo de origem já contiver uma cadeia de mipmap, o arquivo de saída terá uma cadeia MIP; caso contrário, o arquivo de saída não terá uma cadeia MIP.|
|**Saída de conteúdo**|Especifica o nome do arquivo de saída. **Importante:** alterar a extensão de nome de arquivo de saída não tem efeito sobre o formato do arquivo.|

### <a name="mesh-content-pipeline-configuration"></a>Configuração do pipeline de conteúdo da malha

Quando você usar a ferramenta de pipeline de conteúdo da malha para criar um ativo de malha, é possível alterar o nome do arquivo de saída.

|Propriedade|Descrição|
|--------------|-----------------|
|**Saída de conteúdo**|Especifica o nome do arquivo de saída. **Importante:** alterar a extensão de nome de arquivo de saída não tem efeito sobre o formato do arquivo.|

### <a name="shader-content-pipeline-configuration"></a>Configuração do pipeline de conteúdo do sombreador

Quando você usar a ferramenta de pipeline de conteúdo do sombreador para criar um ativo de sombreador, é possível alterar o nome do arquivo de saída.

|Propriedade|Descrição|
|--------------|-----------------|
|**Saída de conteúdo**|Especifica o nome do arquivo de saída. **Importante:** alterar a extensão de nome de arquivo de saída não tem efeito sobre o formato do arquivo.|

## <a name="load-and-use-3d-assets-at-run-time"></a>Carregar e usar ativos 3D em tempo de execução

### <a name="use-textures-and-images"></a>Usar texturas e imagens

Direct3D fornece funções para criar recursos de textura. No Direct3D 11, a biblioteca do utilitário D3DX11 fornece funções adicionais para criar recursos de textura e visualizações de recursos diretamente de arquivos de imagem. Para obter mais informações sobre como criar um recurso de textura em Direct3D 11, consulte [Texturas](/windows/win32/direct3d11/overviews-direct3d-11-resources-textures). Para obter mais informações sobre como usar a biblioteca D3DX11 para criar um recurso de textura ou um modo de exibição de recursos com base em um arquivo de imagem, confira [Como inicializar uma textura de um arquivo](/windows/win32/direct3d11/overviews-direct3d-11-resources-textures-how-to).

### <a name="use-3d-models"></a>Usar modelos 3D

O Direct3D 11 não fornece funções para criar recursos de modelos 3D. Em vez disso, você precisa gravar código que leia o arquivo de modelo 3D e crie buffers de índice e vértice que representem o modelo 3D e quaisquer recursos que o modelo exija, como texturas ou sombreadores.

### <a name="use-shaders"></a>Usar sombreadores

O Direct3D fornece funções para criar recursos do sombreador e associá-los ao pipeline gráfico programável. Para obter mais informações sobre como criar um recurso de sombreador no Direct3D e associá-lo ao pipeline, confira [Guia de programação para HLSL](/windows/win32/direct3dhlsl/dx-graphics-hlsl-pguide).

No pipeline gráfico programável, cada estágio do pipeline deve dar ao próximo estágio do pipeline um resultado que esteja formatado de modo que possa ser entendido. Como o Designer do Sombreador só pode criar sombreadores de pixel, significa que é responsabilidade do aplicativo garantir que os dados recebidos estejam no formato esperado. Vários estágios do sombreador programável ocorrem antes do sombreador de pixel, e eles realizam transformações geométricas (o sombreador de vértice, o sombreador Hull, o sombreador de domínio e o sombreador de geometria). O estágio de mosaico não programável também ocorre antes do sombreador de pixel. Não importa qual desses estágios precedem diretamente o sombreador de pixel, ele deve apresentar seu resultado neste formato:

```hlsl
struct PixelShaderInput
{
    float4 pos : SV_POSITION;
    float4 diffuse : COLOR;
    float2 uv : TEXCOORD0;
    float3 worldNorm : TEXCOORD1;
    float3 worldPos : TEXCOORD2;
    float3 toEye : TEXCOORD3;
    float4 tangent : TEXCOORD4;
    float3 normal : TEXCOORD5;
};
```

Dependendo dos nós do Designer do Sombreador usados no seu sombreador, também pode ser necessário fornecer dados adicionais em um formato de acordo com estas definições:

```hlsl
Texture2D Texture1 : register( t0 );
Texture2D Texture2 : register( t1 );
Texture2D Texture3 : register( t2 );
Texture2D Texture4 : register( t3 );
Texture2D Texture5 : register( t4 );
Texture2D Texture6 : register( t5 );
Texture2D Texture7 : register( t6 );
Texture2D Texture8 : register( t7 );

TextureCube CubeTexture1 : register( t8 );
TextureCube CubeTexture2 : register( t9 );
TextureCube CubeTexture3 : register( t10 );
TextureCube CubeTexture4 : register( t11 );
TextureCube CubeTexture5 : register( t12 );
TextureCube CubeTexture6 : register( t13 );
TextureCube CubeTexture7 : register( t14 );
TextureCube CubeTexture8 : register( t15 );

SamplerState TexSampler : register( s0 );

cbuffer MaterialVars : register (b0)
{
    float4 MaterialAmbient;
    float4 MaterialDiffuse;
    float4 MaterialSpecular;
    float4 MaterialEmissive;
    float MaterialSpecularPower;
};

cbuffer LightVars : register (b1)
{
    float4 AmbientLight;
    float4 LightColor[4];
    float4 LightAttenuation[4];
    float3 LightDirection[4];
    float LightSpecularIntensity[4];
    uint IsPointLight[4];
    uint ActiveLights;
}

cbuffer ObjectVars : register(b2)
{
    float4x4 LocalToWorld4x4;
    float4x4 LocalToProjected4x4;
    float4x4 WorldToLocal4x4;
    float4x4 WorldToView4x4;
    float4x4 UVTransform4x4;
    float3 EyePosition;
};

cbuffer MiscVars : register(b3)
{
    float ViewportWidth;
    float ViewportHeight;
    float Time;
};
```

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Como exportar uma textura que contenha mipmaps](../designers/how-to-export-a-texture-that-contains-mipmaps.md)|Descreve como usar o Pipeline de Conteúdo da Imagem para exportar uma textura contendo mipmaps pré-calculados.|
|[Como exportar uma textura que tenha Alfa pré-multiplicado](../designers/how-to-export-a-texture-that-has-premultiplied-alpha.md)|Descreve como usar o Pipeline de Conteúdo da Imagem para exportar uma textura contendo valores alfa pré-multiplicados.|
|[Como: exportar uma textura para uso com aplicativos Direct2D ou JavaScript](../designers/how-to-export-a-texture-for-use-with-direct2d-or-javascipt-apps.md)|Descreve como usar o Pipeline de Conteúdo da Imagem para exportar uma textura que possa ser usada em um aplicativo Direct2D ou JavaScript.|
|[Trabalhando com ativos 3D para jogos e aplicativos](../designers/working-with-3-d-assets-for-games-and-apps.md)|Descreve as ferramentas de edição que o Visual Studio fornece para criar e manipular ativos 3D, incluindo texturas e imagens, modelos 3D e sombreadores.|
|[Como: exportar um sombreador](../designers/how-to-export-a-shader.md)|Descreve como exportar o sombreador do Designer do Sombreador.|
