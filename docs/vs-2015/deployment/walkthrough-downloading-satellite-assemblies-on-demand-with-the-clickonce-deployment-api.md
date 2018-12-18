---
title: 'Passo a passo: Baixando Assemblies satélite por demanda com a API de implantação do ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 6e6de316fd0ff66e0815da7fa935d21e23a8285e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49306326"
---
# <a name="walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api"></a>Instruções passo a passo: baixando assemblies satélite por demanda com a API de implantação do ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplicativos do Windows Forms podem ser configurados para várias culturas com o uso de assemblies satélite. Um *assembly satélite* é um assembly que contém os recursos de aplicativo para uma cultura que não seja a cultura padrão do aplicativo.  
  
 Conforme discutido em [localizando aplicativos do ClickOnce](../deployment/localizing-clickonce-applications.md), você pode incluir vários assemblies de satélite para várias culturas dentro do mesmo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação. Por padrão, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] baixará todos os assemblies de satélite em sua implantação para o computador cliente, embora um único cliente provavelmente exigirá apenas um assembly satélite.  
  
 Este passo a passo demonstra como marcar seus assemblies satélites como opcionais e baixar somente o assembly precisa de um computador cliente para suas configurações de cultura. O procedimento a seguir usa as ferramentas disponíveis no [!INCLUDE[winsdklong](../includes/winsdklong-md.md)]. Você também pode executar esta tarefa no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  Consulte também [instruções passo a passo: baixando Assemblies de satélite sob demanda com o ClickOnce Deployment API usando o Designer](http://msdn.microsoft.com/library/ms366788\(v=vs.110\)) ou [passo a passo: baixando Assemblies de satélite por demanda com a API de implantação do ClickOnce Usando o Designer](http://msdn.microsoft.com/library/ms366788\(v=vs.120\)).  
  
> [!NOTE]
>  Para fins de teste, o exemplo de código a seguir por meio de programação define a cultura para `ja-JP`. Consulte a seção "Próximas etapas" mais adiante neste tópico para obter informações sobre como ajustar esse código para um ambiente de produção.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico pressupõe que você saiba como adicionar recursos localizados ao seu aplicativo usando o Visual Studio. Para obter instruções detalhadas, consulte [instruções passo a passo: Localizando Windows Forms](https://msdn.microsoft.com/library/vstudio/y99d1cd3\(v=vs.100\).aspx).  
  
### <a name="to-download-satellite-assemblies-on-demand"></a>Para baixar os assemblies satélite por demanda  
  
1.  Adicione o seguinte código ao seu aplicativo para habilitar o download sob demanda dos assemblies satélites.  
  
     [!code-csharp[ClickOnce.SatelliteAssembliesSDK#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesSDK/CS/Program.cs#1)]
     [!code-vb[ClickOnce.SatelliteAssembliesSDK#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesSDK/VB/Form1.vb#1)]  
  
2.  Gerar assemblies de satélite para o seu aplicativo usando o [Resgen.exe (gerador de arquivo de recurso)](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4) ou [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
3.  Gerar um manifesto de aplicativo, ou abra o manifesto do aplicativo existente, usando MageUI.exe. Para obter mais informações sobre essa ferramenta, consulte [MageUI.exe (Manifest Generation and Editing Tool, cliente gráfico)](http://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14).  
  
4.  Clique o **arquivos** guia.  
  
5.  Clique o **reticências** botão (**...** ) e selecione o diretório que contém todos os assemblies e arquivos, incluindo os assemblies de satélite gerado usando Resgen.exe do seu aplicativo. (Um assembly satélite terá um nome na forma *isoCode*\ApplicationName.resources.dll, onde *isoCode* é um identificador de idioma no formato RFC 1766.)  
  
6.  Clique em **popular** para adicionar os arquivos para sua implantação.  
  
7.  Selecione o **opcional** caixa de seleção para cada assembly satélite.  
  
8.  Defina o campo de grupo para cada assembly satélite para o seu identificador de idioma ISO. Por exemplo, para um assembly satélite japonês, você especificaria um nome de grupo de download de `ja-JP`. Isso permitirá que o código adicionado na etapa 1 para baixar o assembly satélite adequado, dependendo do usuário <xref:System.Threading.Thread.CurrentUICulture%2A> configuração da propriedade.  
  
## <a name="next-steps"></a>Próximas etapas  
 Em um ambiente de produção, provavelmente será necessário remover a linha no código de exemplo que define <xref:System.Threading.Thread.CurrentUICulture%2A> como um valor específico, porque máquinas de cliente será tem o valor correto definido por padrão. Quando seu aplicativo é executado em um computador cliente japonês, por exemplo, <xref:System.Threading.Thread.CurrentUICulture%2A> será `ja-JP` por padrão. Definir esse valor por meio de programação é uma boa maneira de testar seus assemblies satélites antes de implantar seu aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Localizando aplicativos ClickOnce](../deployment/localizing-clickonce-applications.md)



