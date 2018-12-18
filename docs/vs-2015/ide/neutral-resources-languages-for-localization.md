---
title: Idiomas de recursos neutros para localização | Microsoft Docs
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
- localization [Visual Studio], resources
- NeutralResourcesLanguageAttribute class
- globalization [Visual Studio], resources
- resources [Visual Studio], fallback system
- culture, locating resources
- neutral resources
ms.assetid: ef064995-3b84-4698-a708-9689b7723533
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 45fadacc75b2772ba32d7cb0d796c972076b81ef
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49256681"
---
# <a name="neutral-resources-languages-for-localization"></a>Idiomas de recursos naturais para localização
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A classe <xref:System.Resources.NeutralResourcesLanguageAttribute> especifica a cultura dos recursos incluídos no assembly principal. Esse atributo é usado como um aperfeiçoamento do desempenho, de modo que o objeto <xref:System.Resources.ResourceManager> não pesquise recursos que estão incluídos no assembly principal.  
  
 O código a seguir mostra como definir o idioma de recursos neutros. O código pode ser colocado em um script de build ou no arquivo AssemblyInfo.vb ou AssemblyInfo.cs.  
  
```vb  
' Set neutral resources language for assembly.  
<Assembly: NeutralResourcesLanguageAttribute("en")>  
  
```  
  
```csharp  
// Set neutral resources language for assembly.  
[assembly: NeutralResourcesLanguageAttribute("en")]  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Resources.ResourceManager>   
 [Introdução a aplicativos internacionais com base no .NET Framework](../ide/introduction-to-international-applications-based-on-the-dotnet-framework.md)   
 [Organização hierárquica de recursos para localização](../ide/hierarchical-organization-of-resources-for-localization.md)   
 [Localizando aplicativos](../ide/localizing-applications.md)   
 [Globalizando e localizando aplicativos](../ide/globalizing-and-localizing-applications.md)

