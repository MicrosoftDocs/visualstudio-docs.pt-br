---
title: Idiomas de recursos naturais para localização
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- localization [Visual Studio], resources
- NeutralResourcesLanguageAttribute class
- globalization [Visual Studio], resources
- resources [Visual Studio], fallback system
- culture, locating resources
- neutral resources
ms.assetid: ef064995-3b84-4698-a708-9689b7723533
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 34013c0b896f47e919a105680d18812aaba60dd0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906982"
---
# <a name="neutral-resources-languages-for-localization"></a>Idiomas de recursos naturais para localização

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

- <xref:System.Resources.ResourceManager>
- [Introdução a aplicativos internacionais com base no .NET Framework](../ide/introduction-to-international-applications-based-on-the-dotnet-framework.md)
- [Organização hierárquica de recursos para localização](../ide/hierarchical-organization-of-resources-for-localization.md)
- [Localizando aplicativos](../ide/localizing-applications.md)
- [Globalizando e localizando aplicativos](../ide/globalizing-and-localizing-applications.md)