---
title: Quando implementar um controle do código-fonte VSPackage
description: Saiba mais sobre as opções de plug-ins de controle do código-fonte e VSPackages de controle do código-fonte disponíveis para estender soluções de controle do código-fonte do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 89e2ea0db7f162c70261ab2ba9aab187f9c11bd0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090883"
---
# <a name="determine-whether-to-implement-a-source-control-vspackage"></a>Determinar se uma VSPackage de controle do código-fonte deve ser implementada

Esta seção elabora as opções de plug-ins de controle do código-fonte e VSPackages de controle do código-fonte para estender soluções de controle do código-fonte e fornece diretrizes abrangentes sobre como escolher um caminho de integração adequado.

## <a name="small-source-control-solution-with-limited-resources"></a>Pequena solução de controle do código-fonte com recursos limitados

 Se você tiver recursos limitados e não puder ser carregado com a sobrecarga de escrever um pacote de controle do código-fonte, você poderá criar plug-ins baseados em API de plug-in de controle do código-fonte. Isso permite que você trabalhe lado a lado com pacotes de controle do código-fonte, e você pode alternar entre plug-ins de controle do código-fonte e pacotes sob demanda. Para obter mais informações, consulte [registro e seleção](../../extensibility/internals/registration-and-selection-source-control-vspackage.md).

## <a name="large-source-control-solution-with-a-rich-feature-set"></a>Solução de controle do código-fonte grande com um rico conjunto de recursos

 Se você quiser implementar uma solução de controle do código-fonte que fornece um modelo de controle do código-fonte avançado que não é capturado adequadamente usando a API de plug-in de controle do código-fonte, você pode considerar um pacote de controle do código-fonte como o caminho de integração. Isso se aplica especialmente se você preferir substituir o pacote do adaptador de controle do código-fonte (que se comunica com plug-ins de controle do código-fonte e fornece uma interface do usuário de controle do código-fonte básica) com o seu próprio para que você possa manipular os eventos de controle do código-fonte de maneira personalizada. Se você já tiver uma interface do usuário de controle do código-fonte satisfatória e quiser preservar essa experiência no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , a opção do pacote de controle do código-fonte permitirá que você faça exatamente isso. O pacote de controle do código-fonte não é genérico e é projetado exclusivamente para uso com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.

 Se você quiser implementar uma solução de controle do código-fonte que forneça flexibilidade e controle mais avançado sobre a lógica de controle do código-fonte e a interface do usuário, você pode preferir a rota de integração do pacote de controle do código-fonte Você pode:

1. Registre seu próprio VSPackage de controle do código-fonte (consulte [registro e seleção](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)).

2. Substitua a interface do usuário do controle do código-fonte por sua interface do usuário personalizada (consulte a [interface de usuários personalizada](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)).

3. Especifique os glifos a serem usados e manipule Gerenciador de Soluções eventos de glifo (consulte [controle de glifo](../../extensibility/internals/glyph-control-source-control-vspackage.md)).

4. Manipule eventos de edição de consulta e salvar consulta (veja [consulta editar consulta salvar](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)).

## <a name="see-also"></a>Confira também

- [Criar um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)
