---
title: Organização hierárquica de recursos para localização
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
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
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f21b4c6d53a70cb3d695c05e412b0e2f52a607bb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49874553"
---
# <a name="hierarchical-organization-of-resources-for-localization"></a>Organização hierárquica de recursos para localização

No Visual Studio, os recursos localizados (dados como cadeias de caracteres e imagens apropriadas para cada cultura) são armazenados em arquivos separados e carregados de acordo com a configuração de cultura da interface do usuário. Para entender como os recursos localizados são carregados, é útil pensar neles como organizados de forma hierárquica.

## <a name="kinds-of-resources-in-the-hierarchy"></a>Tipos de recursos na hierarquia

- Os recursos de fallback para sua cultura padrão, por exemplo, inglês ("en") estão no topo da hierarquia. Esses recursos de fallback são os únicos que não têm seu próprio arquivo, eles são armazenados no assembly principal.

- Os recursos de fallback abaixo são os recursos para qualquer cultura neutra. Uma cultura neutra é associada a um idioma, mas não a um país/região. Por exemplo, francês (“fr”) é uma cultura neutra. (Os recursos de fallback são também para uma cultura neutra, mas uma específica.)

- Os recursos de cultura neutra são recursos adequados para qualquer cultura específica. Uma cultura específica é associada a um idioma e a um país/região. Por exemplo, francês canadense ("fr-CA") é uma cultura específica.

Se um aplicativo tenta carregar qualquer recurso localizado, como uma cadeia de caracteres e não o encontra, ele percorrerá a hierarquia para cima até encontrar um arquivo de recurso que contenha o recurso solicitado.

A melhor maneira de armazenar seus recursos é generalizá-los o máximo possível. Isso significa armazenar cadeias de caracteres localizadas, imagens e assim por diante nos arquivos de recursos para culturas neutras em vez de culturas específicas sempre que possível. Por exemplo, se você tiver recursos para a cultura francês belga ("fr-BE") e os recursos imediatamente acima forem os recursos de fallback em inglês, poderá ocorrer um problema quando alguém usar o aplicativo em um sistema configurado para a cultura do francês canadense. O sistema procura por um assembly satélite para “fr-CA”, mas não o encontra e carrega o assembly principal que contém o recurso de fallback, em inglês, em vez de carregar os recursos em francês. A figura a seguir mostra este cenário indesejável.

![Apenas recursos específicos](../ide/media/vbspecificresourcesonly.gif)

Se você seguir a prática recomendada de colocar o máximo de recursos possível em um arquivo de recurso neutro para a cultura “fr”, o usuário do francês canadense não verá os recursos marcados para a cultura “fr-BE”, mas verá cadeias de caracteres em francês. A situação a seguir mostra esse cenário preferencial.

![Gráfico NeutralSpecificResources](../ide/media/vbneutralspecificresources.gif)

## <a name="see-also"></a>Consulte também

- [Idiomas de recursos neutros para localização](../ide/neutral-resources-languages-for-localization.md)
- [Assemblies satélite de segurança e localizados](../ide/security-and-localized-satellite-assemblies.md)
- [Localizar aplicativos](../ide/localizing-applications.md)
- [Globalizando e localizando aplicativos](../ide/globalizing-and-localizing-applications.md)