---
title: Baixar o assembly satélite sob demanda (API do ClickOnce)
description: Saiba como marcar assemblies satélite como opcionais e baixar apenas o assembly de que um computador cliente precisa para suas configurações de cultura atuais.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, globalization
- localization, Windows Forms
- Windows Forms, localization
- globalization, ClickOnce
- satellite assemblies, ClickOnce
- ClickOnce deployment, on-demand download
- localization, ClickOnce deployment
- ClickOnce deployment, localization
ms.assetid: fdaa553f-a27e-44eb-a4e2-08c122105a87
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d6ebcb455147b1cb014eb7aafc9f6a9e658e0131
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217002"
---
# <a name="walkthrough-download-satellite-assemblies-on-demand-with-the-clickonce-deployment-api"></a>Walkthrough: baixar assemblies satélite sob demanda com a API de implantação do ClickOnce
Windows Forms aplicativos podem ser configurados para várias culturas por meio do uso de assemblies satélite. Um *assembly satélite* é um assembly que contém recursos de aplicativo para uma cultura diferente da cultura padrão do aplicativo.

 Como discutido em [Localizar aplicativos ClickOnce](../deployment/localizing-clickonce-applications.md), você pode incluir vários assemblies satélite para várias culturas na mesma [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação. Por padrão, o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] baixará todos os assemblies satélite em sua implantação para o computador cliente, embora um único cliente provavelmente exigirá apenas um assembly satélite.

 Este tutorial demonstra como marcar seus assemblies satélite como opcionais e baixar apenas o assembly de que um computador cliente precisa para suas configurações de cultura atuais. O procedimento a seguir usa as ferramentas disponíveis no [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] . Você também pode executar essa tarefa no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .  Confira também [passo a passos: baixar assemblies satélite sob demanda com a API de implantação do ClickOnce usando o designer](/previous-versions/visualstudio/visual-studio-2012/ms366788(v=vs.110)) ou [passo a passos: baixar assemblies satélite sob demanda com a API de implantação do ClickOnce usando o designer](/previous-versions/visualstudio/visual-studio-2013/ms366788(v=vs.120)).

> [!NOTE]
> Para fins de teste, o exemplo de código a seguir define programaticamente a cultura como `ja-JP` . Consulte a seção "próximas etapas" mais adiante neste tópico para obter informações sobre como ajustar esse código para um ambiente de produção.

## <a name="prerequisites"></a>Pré-requisitos
 Este tópico pressupõe que você saiba como adicionar recursos localizados ao seu aplicativo usando o Visual Studio. Para obter instruções detalhadas, consulte [Walkthrough: Localize Windows Forms](/previous-versions/visualstudio/visual-studio-2010/y99d1cd3(v=vs.100)).

### <a name="to-download-satellite-assemblies-on-demand"></a>Para baixar assemblies satélite sob demanda

1. Adicione o código a seguir ao seu aplicativo para habilitar o download sob demanda de assemblies satélite.

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesSDK/CS/Program.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesSDK/VB/Form1.vb" id="Snippet1":::

2. Gere assemblies satélite para seu aplicativo usando [Resgen.exe (gerador de arquivo de recurso)](/dotnet/framework/tools/resgen-exe-resource-file-generator) ou [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

3. Gere um manifesto do aplicativo ou abra o manifesto do aplicativo existente usando *MageUI.exe*. Para obter mais informações sobre essa ferramenta, consulte [MageUI.exe (manifest Generation and Editing Tool, cliente gráfico)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client).

4. Clique na guia **arquivos** .

5. Clique no botão de **reticências** (**...**) e selecione o diretório que contém todos os assemblies e arquivos do seu aplicativo, incluindo os assemblies satélite gerados usando *Resgen.exe*. (Um assembly satélite terá um nome no formulário *\<isoCode>\ApplicationName.resources.dll*, em que \<isoCode> é um identificador de idioma no formato RFC 1766.)

6. Clique em **popular** para adicionar os arquivos à sua implantação.

7. Marque a caixa de seleção **opcional** para cada assembly satélite.

8. Defina o campo de grupo para cada assembly satélite para seu identificador de idioma ISO. Por exemplo, para um assembly satélite em Japonês, você deve especificar um nome de grupo de download de `ja-JP` . Isso habilitará o código adicionado na etapa 1 para baixar o assembly satélite apropriado, dependendo da configuração de Propriedade do usuário <xref:System.Threading.Thread.CurrentUICulture%2A> .

## <a name="next-steps"></a>Próximas etapas
 Em um ambiente de produção, provavelmente você precisará remover a linha no exemplo de código que define <xref:System.Threading.Thread.CurrentUICulture%2A> para um valor específico, pois os computadores cliente terão o valor correto definido por padrão. Quando o aplicativo é executado em um computador cliente japonês, por exemplo, <xref:System.Threading.Thread.CurrentUICulture%2A> será `ja-JP` por padrão. Definir esse valor programaticamente é uma boa maneira de testar seus assemblies satélites antes de implantar seu aplicativo.

## <a name="see-also"></a>Confira também
- [Localizar aplicativos ClickOnce](../deployment/localizing-clickonce-applications.md)
