---
title: Introdução a aplicativos internacionais baseados no .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- strings [Visual Studio], localizing
- Web applications [.NET Framework], globalization
- Windows Forms, globalization
- localization [Visual Studio], culture setting
- fallback resources
- culture, setting
- globalization [Visual Studio], culture setting
- resources [Visual Studio], localization
- localization [Visual Studio], .NET localization model
- Assembly Resource file template
- resources [Visual Studio], fallback system
- international applications [Visual Studio], about international applications
- globalization [Visual Studio], international applications
- ASP.NET, globalization
- resource files, fallback processes
- user interface, culture setting
ms.assetid: b0788993-e62d-4f68-8235-5f87b1d48525
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 3d1539d832b67a160e29b22b71066f72609e35b8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49270018"
---
# <a name="introduction-to-international-applications-based-on-the-net-framework"></a>Introdução a aplicativos internacionais com base no .NET Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], há duas partes para criar um aplicativo pronto para o mundo: globalização, o processo de criação de aplicativos que podem se adaptar a diferentes culturas, e localização, o processo de traduzir recursos para uma cultura específica. Para obter informações gerais sobre como criar aplicativos para um público internacional, consulte [Melhores práticas para o desenvolvimento de aplicativos prontos para o mundo](http://msdn.microsoft.com/library/f08169c7-aad8-4ec3-9a21-9ebd3b89986c).  
  
 O modelo de localização do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] consiste em um assembly principal que contém o código do aplicativo e os recursos de fallback – cadeias de caracteres, imagens e outros objetos para o idioma no qual o aplicativo foi originalmente desenvolvido. Cada aplicativo localizado terá assemblies satélites, ou assemblies que contêm somente os recursos localizados. Como o assembly principal sempre contém os recursos de fallback, se um recurso não for encontrado no assembly satélite localizado, o <xref:System.Resources.ResourceManager> tentará carregá-lo de forma hierárquica, eventualmente recorrendo ao recurso no assembly principal. O sistema de fallback de recurso é explicado mais detalhadamente em [Organização hierárquica de recursos para localização](../ide/hierarchical-organization-of-resources-for-localization.md).  
  
 Um recurso de localização que você deve considerar usar é o glossário para todos os produtos localizados da Microsoft. Esse arquivo CSV contém mais de 12.000 termos em inglês, além das traduções de termos em até 59 idiomas diferentes. O glossário está disponível para download na página da Web [Traduções de terminologia da Microsoft](http://go.microsoft.com/fwlink/?LinkId=128146).  
  
 O sistema do projeto dos aplicativos Windows Forms pode gerar arquivos de recurso para fallback e para cada cultura de interface do usuário adicional desejada. O arquivo de recurso de fallback é compilado no assembly principal e os arquivos de recurso específicos à cultura são então compilados em assemblies satélites, um para cada cultura de interface do usuário. Ao compilar um projeto, os arquivos de recursos são compilados do formato XML do Visual Studio (.resx) para um formato binário intermediário (.resources), que são então inseridos em assemblies satélites.  
  
 O sistema do projeto do Windows Forms e do Web Forms permite compilar arquivos de recurso usando um modelo de Arquivo de Recurso de Assembly, além de acessar os recursos e compilar o projeto. Assemblies satélites serão criados juntamente com o assembly principal.  
  
 Quando um aplicativo localizado é executado, sua aparência é determinada por dois valores de cultura. (Uma *cultura* é um conjunto de informações de preferência do usuário relacionadas ao idioma, ao ambiente e às convenções culturais do usuário.) A configuração de cultura de interface do usuário determina quais recursos serão carregados. A cultura de interface do usuário é definida como `UICulture` nos arquivos Web.config e em diretivas de páginas e como <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> no código do Visual Basic ou do Visual C#. A configuração de cultura determina a formatação de valores, como datas, números, moeda e assim por diante. A cultura é definida como `Culture` nos arquivos Web.config e em diretivas de páginas e como <xref:System.Globalization.CultureInfo.CurrentCulture%2A> no código do Visual Basic ou do Visual C#.  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Globalization>   
 <xref:System.Resources>   
 [Globalizando e localizando aplicativos](../ide/globalizing-and-localizing-applications.md)   
 [Security and Localized Satellite Assemblies](../ide/security-and-localized-satellite-assemblies.md) (Assemblies satélite de segurança e localizados)

