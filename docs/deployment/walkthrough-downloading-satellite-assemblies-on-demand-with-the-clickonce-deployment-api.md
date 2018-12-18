---
title: 'Passo a passo: Baixando Assemblies satélite por demanda com a API de implantação do ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 506495f8be0b552f35bed0610e9fb43a77efb151
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49883023"
---
# <a name="walkthrough-download-satellite-assemblies-on-demand-with-the-clickonce-deployment-api"></a>Passo a passo: Fazer o Download de assemblies satélite por demanda com a API de implantação do ClickOnce
Aplicativos do Windows Forms podem ser configurados para várias culturas com o uso de assemblies satélite. Um *assembly satélite* é um assembly que contém os recursos de aplicativo para uma cultura que não seja a cultura padrão do aplicativo.  
  
 Conforme discutido em [aplicativos ClickOnce localizar](../deployment/localizing-clickonce-applications.md), você pode incluir vários assemblies de satélite para várias culturas dentro do mesmo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação. Por padrão, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] baixará todos os assemblies de satélite em sua implantação para o computador cliente, embora um único cliente provavelmente exigirá apenas um assembly satélite.  
  
 Este passo a passo demonstra como marcar seus assemblies satélites como opcionais e baixar somente o assembly precisa de um computador cliente para suas configurações de cultura. O procedimento a seguir usa as ferramentas disponíveis no [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)]. Você também pode executar esta tarefa no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  Consulte também [passo a passo: baixar os assemblies satélite por demanda com a API usando o Designer de implantação do ClickOnce](/previous-versions/visualstudio/visual-studio-2012/ms366788(v=vs.110)) ou [passo a passo: baixar os assemblies satélite sob demanda com a API de implantação do ClickOnce usando o Designer](/previous-versions/visualstudio/visual-studio-2013/ms366788(v=vs.120)).  
  
> [!NOTE]
>  Para fins de teste, o exemplo de código a seguir por meio de programação define a cultura para `ja-JP`. Consulte a seção "Próximas etapas" mais adiante neste tópico para obter informações sobre como ajustar esse código para um ambiente de produção.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico pressupõe que você saiba como adicionar recursos localizados ao seu aplicativo usando o Visual Studio. Para obter instruções detalhadas, consulte [instruções passo a passo: formulários do Windows localizar](/previous-versions/visualstudio/visual-studio-2010/y99d1cd3(v=vs.100)).  
  
### <a name="to-download-satellite-assemblies-on-demand"></a>Para baixar os assemblies satélite por demanda  
  
1. Adicione o seguinte código ao seu aplicativo para habilitar o download sob demanda dos assemblies satélites.  
  
    [!code-csharp[ClickOnce.SatelliteAssembliesSDK#1](../deployment/codesnippet/CSharp/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api_1.cs)]
    [!code-vb[ClickOnce.SatelliteAssembliesSDK#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api_1.vb)]  
  
2. Gerar assemblies de satélite para o seu aplicativo usando o [Resgen.exe (gerador de arquivo de recurso)](/dotnet/framework/tools/resgen-exe-resource-file-generator) ou [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
3. Gerar um manifesto de aplicativo, ou abra o manifesto do aplicativo existente, usando *MageUI.exe*. Para obter mais informações sobre essa ferramenta, consulte [MageUI.exe (Manifest Generation and Editing Tool, cliente gráfico)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client).  
  
4. Clique o **arquivos** guia.  
  
5. Clique o **reticências** botão (**...** ) e selecione o diretório que contém todos os assemblies e arquivos, incluindo os assemblies de satélite gerado usando o seu aplicativo *Resgen.exe*. (Um assembly satélite terá um nome na forma  *\<isoCode > \ApplicationName.resources.dll*, onde \<isoCode > é um identificador de idioma no formato RFC 1766.)  
  
6. Clique em **popular** para adicionar os arquivos para sua implantação.  
  
7. Selecione o **opcional** caixa de seleção para cada assembly satélite.  
  
8. Defina o campo de grupo para cada assembly satélite para o seu identificador de idioma ISO. Por exemplo, para um assembly satélite japonês, você especificaria um nome de grupo de download de `ja-JP`. Isso permitirá que o código adicionado na etapa 1 para baixar o assembly satélite adequado, dependendo do usuário <xref:System.Threading.Thread.CurrentUICulture%2A> configuração da propriedade.  
  
## <a name="next-steps"></a>Próximas etapas  
 Em um ambiente de produção, provavelmente será necessário remover a linha no código de exemplo que define <xref:System.Threading.Thread.CurrentUICulture%2A> como um valor específico, porque máquinas de cliente será tem o valor correto definido por padrão. Quando seu aplicativo é executado em um computador cliente japonês, por exemplo, <xref:System.Threading.Thread.CurrentUICulture%2A> será `ja-JP` por padrão. Definir esse valor por meio de programação é uma boa maneira de testar seus assemblies satélites antes de implantar seu aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Localizar aplicativos ClickOnce](../deployment/localizing-clickonce-applications.md)