---
title: Organização hierárquica de recursos para localização | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- resource files, localized
- localization [Visual Studio], resources
- fallback resources
- international applications [Visual Studio], storing resources
- satellite assemblies, resource hierarchies
- globalization [Visual Studio], resources
- satellite assemblies
- resources [Visual Studio], fallback system
- resource files, fallback processes
ms.assetid: dadf8f2c-f74c-44d7-bec0-a1e956d8d38d
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0a79caca18c7813605ff851eea6bda642e6300a0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "72645610"
---
# <a name="hierarchical-organization-of-resources-for-localization"></a>Organização hierárquica de recursos para localização
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, os recursos localizados (dados como cadeias de caracteres e imagens apropriadas para cada cultura) são armazenados em arquivos separados e carregados de acordo com a configuração de cultura da interface do usuário. Para entender como os recursos localizados são carregados, é útil pensar neles como organizados de forma hierárquica.

## <a name="kinds-of-resources-in-the-hierarchy"></a>Tipos de recursos na hierarquia

- Na parte superior da hierarquia estão os recursos de fallback para sua cultura padrão, por exemplo, inglês ("en"). Esses são os únicos recursos que não têm seu próprio arquivo, eles são armazenados no assembly principal.

- Os recursos de fallback abaixo são os recursos para qualquer cultura neutra. Uma cultura neutra é associada a um idioma, mas não a um país/região. Por exemplo, francês (“fr”) é uma cultura neutra. (Observe que os recursos de fallback são também para uma cultura neutra, mas uma específica.)

- Abaixo daqueles estão os recursos para quaisquer culturas específicas. Uma cultura específica é associada a um idioma e a um país/região. Por exemplo, francês canadense ("fr-CA") é uma cultura específica.

  Se um aplicativo tenta carregar qualquer recurso localizado, como uma cadeia de caracteres e não o encontra, ele percorrerá a hierarquia para cima até encontrar um arquivo de recurso que contenha o recurso solicitado.

  A melhor maneira de armazenar seus recursos é generalizá-los o máximo possível. Isso significa armazenar cadeias de caracteres localizadas, imagens e assim por diante nos arquivos de recursos para culturas neutras em vez de culturas específicas sempre que possível. Por exemplo, se você tiver recursos para a cultura francês belga ("fr-BE") e os recursos imediatamente acima forem os recursos de fallback em inglês, poderá ocorrer um problema quando alguém usar o aplicativo em um sistema configurado para a cultura do francês canadense. O sistema procurará por um assembly satélite para “fr-CA”, não o encontrará e carregará o assembly principal que contém o recurso de fallback, que está em inglês, em vez de carregar os recursos em francês. A figura a seguir mostra este cenário indesejável.

  ![Apenas recursos específicos](../ide/media/vbspecificresourcesonly.gif "vbSpecificResourcesOnly")

  Se você seguir a prática recomendada de colocar o máximo de recursos possível em um arquivo de recurso neutro para a cultura “fr”, o usuário do francês canadense não verá os recursos marcados para a cultura “fr-BE”, mas verá cadeias de caracteres em francês. A situação a seguir mostra esse cenário preferencial.

  ![Gráfico NeutralSpecificResources](../ide/media/vbneutralspecificresources.gif "vbNeutralSpecificResources")

## <a name="see-also"></a>Consulte Também
 [Idiomas de recursos neutros para segurança de localização](../ide/neutral-resources-languages-for-localization.md) [e assemblies de satélite localizados](../ide/security-and-localized-satellite-assemblies.md) [Localizando aplicativos](../ide/localizing-applications.md) [Globalizando e Localizando aplicativos](../ide/globalizing-and-localizing-applications.md) [como: definir a cultura e a cultura da interface do usuário para Windows Forms globalização](https://msdn.microsoft.com/694e049f-0b91-474a-9789-d35124f248f0) [como: definir a cultura e a cultura da interface do usuário para globalização de página da Web ASP.net](https://msdn.microsoft.com/library/76091f86-f967-4687-a40f-de87bd8cc9a0)
