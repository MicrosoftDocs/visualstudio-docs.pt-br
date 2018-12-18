---
title: 'Passo a passo: Baixando Assemblies satélite por demanda com a implantação do ClickOnce usando o Designer de API | Microsoft Docs'
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
- Windows Forms, globalization
- ClickOnce deployment, globalization
- localization, Windows Forms
- ClickOnce, on-demand download
- Windows Forms, localization
- ClickOnce deployment, localization
- walkthroughs, localization
ms.assetid: 82b85a47-b223-4221-a17c-38a52c3fb6e2
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 5ca86e2ed1a05c8e325a99686281db3a7cf8f56e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49306222"
---
# <a name="walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer"></a>Instruções passo a passo: baixando assemblies satélite por demanda com a API de implantação do ClickOnce usando o designer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplicativos do Windows Forms podem ser configurados para várias culturas com o uso de assemblies satélite. Um *assembly satélite* é um assembly que contém os recursos de aplicativo para uma cultura que não seja a cultura padrão do aplicativo.  
  
 Conforme discutido em [localizando aplicativos do ClickOnce](../deployment/localizing-clickonce-applications.md), você pode incluir vários assemblies de satélite para várias culturas dentro do mesmo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação. Por padrão, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] baixará todos os assemblies de satélite em sua implantação para o computador cliente, embora um único cliente provavelmente exigirá apenas um assembly satélite.  
  
 Este passo a passo demonstra como marcar seus assemblies satélites como opcionais e baixar somente o assembly precisa de um computador cliente para suas configurações de cultura.  
  
> [!NOTE]
>  Para fins de teste, os exemplos de código a seguir por meio de programação definem a cultura `ja-JP`. Consulte a seção "Próximas etapas" mais adiante neste tópico para obter informações sobre como ajustar esse código para um ambiente de produção.  
  
### <a name="to-mark-satellite-assemblies-as-optional"></a>Para marcar os assemblies satélites como opcionais  
  
1.  Criar o projeto. Isso irá gerar assemblies de satélite para todas as culturas que você estiver localizando a.  
  
2.  Clique com botão direito no nome do projeto no Gerenciador de soluções e, em seguida, clique em **propriedades**.  
  
3.  Clique o **Publish** guia e, em seguida, clique em **arquivos de aplicativo**.  
  
4.  Selecione o **Mostrar todos os arquivos** caixa de seleção para exibir os assemblies satélites. Por padrão, todos os assemblies satélite serão incluídos em sua implantação e estarão visíveis na caixa de diálogo.  
  
     Um assembly satélite terá um nome na forma *isoCode*\ApplicationName.resources.dll, onde *isoCode* é um identificador de idioma no formato RFC 1766.  
  
5.  Clique em **novo...**  no **grupo de Download** lista para cada identificador de idioma. Quando solicitado a fornecer um nome de grupo de download, insira o identificador de idioma. Por exemplo, para um assembly satélite japonês, você especificaria o nome do grupo de download `ja-JP`.  
  
6.  Fechar o **arquivos de aplicativo** caixa de diálogo.  
  
### <a name="to-download-satellite-assemblies-on-demand-in-c"></a>Para baixar os assemblies satélite sob demanda em c#  
  
1.  Abra o arquivo Program.cs. Se você não vir esse arquivo no Gerenciador de soluções, selecione seu projeto e sobre o **projeto** menu, clique em **Mostrar todos os arquivos**.  
  
2.  Use o código a seguir para baixar o assembly satélite adequado e iniciar o aplicativo.  
  
     [!code-csharp[ClickOnce.SatelliteAssemblies#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnce.SatelliteAssemblies/CS/Program.cs#1)]  
  
### <a name="to-download-satellite-assemblies-on-demand-in-visual-basic"></a>Para baixar os assemblies satélite sob demanda no Visual Basic  
  
1.  No **propriedades** janela do aplicativo, clique no **aplicativo** guia.  
  
2.  Na parte inferior da página da guia, clique em **exibir eventos do aplicativo**.  
  
3.  Adicione as importações a seguir ao início do arquivo ApplicationEvents VB.  
  
     [!code-vb[ClickOnce.SatelliteAssembliesVB#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesVB/VB/ApplicationEvents.vb#1)]  
  
4.  Adicione o seguinte código para o `MyApplication` classe.  
  
     [!code-vb[ClickOnce.SatelliteAssembliesVB#2](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesVB/VB/ApplicationEvents.vb#2)]  
  
## <a name="next-steps"></a>Próximas etapas  
 Em um ambiente de produção, provavelmente será necessário remover a linha nos exemplos de código que define <xref:System.Threading.Thread.CurrentUICulture%2A> como um valor específico, porque máquinas de cliente será tem o valor correto definido por padrão. Quando seu aplicativo é executado em um computador cliente japonês, por exemplo, <xref:System.Threading.Thread.CurrentUICulture%2A> será `ja-JP` por padrão. Defini-lo por meio de programação é uma boa maneira de testar seus assemblies satélites antes de implantar seu aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Baixando Assemblies satélite por demanda com a API de implantação do ClickOnce](../deployment/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api.md)   
 [Localizando aplicativos ClickOnce](../deployment/localizing-clickonce-applications.md)



