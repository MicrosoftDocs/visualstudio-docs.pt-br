---
title: Noções básicas de integração de controle do código-fonte | Microsoft Docs
description: 'Saiba mais sobre os dois tipos de integração de controle do código-fonte com suporte do Visual Studio: um plug-in de controle do código-fonte e uma solução de controle do código-fonte baseada em VSPackage.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Source Control Integration, essentials
- Source Control Integration,overview
- essentials, Source Control Integration
ms.assetid: 442057cb-fd54-4283-96f8-2f6dc8bf2de7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 155e662eae0dda6689a233e31fd62bb72259ae8b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069329"
---
# <a name="source-control-integration-essentials"></a>Conceitos básicos da integração do controle do código-fonte
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] dá suporte a dois tipos de integração de controle de origem: um plug-in de controle do código-fonte que fornece funcionalidade básica e é criado usando a API de plug-in de controle do código-fonte (anteriormente conhecida como API MSSCCI) e uma solução de integração de controle do código-fonte baseada em VSPackage que fornece funcionalidade mais robusta.

## <a name="source-control-plug-in"></a>Plug-in de controle do código-fonte
 Um plug-in de controle do código-fonte é escrito como uma DLL que implementa a API de plug-in de controle do código-fonte. A funcionalidade de integração de controle do código-fonte e de registro é fornecida por meio da API. Essa abordagem é mais fácil de implementar do que um VSPackage de controle do código-fonte e usa a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface do usuário (IU) para a maioria das operações de controle do código-fonte.

 Para implementar um plug-in de controle do código-fonte usando a API de plug-in de controle do código-fonte, siga estas etapas:

1. Crie uma DLL que implemente as funções especificadas em [plug-ins de controle do código-fonte](../../extensibility/source-control-plug-ins.md).

2. Registre a DLL fazendo as entradas de registro apropriadas, conforme descrito em [como instalar um plug-in de controle do código-fonte](../../extensibility/internals/how-to-install-a-source-control-plug-in.md).

3. Crie uma interface do usuário auxiliar e exiba-a quando solicitado pelo pacote do adaptador de controle do código-fonte (o componente que manipula a funcionalidade de controle do código-fonte [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] através de plug-ins de controle do código-fonte

   Para obter mais informações, consulte [criando um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md).

## <a name="source-control-vspackage"></a>VSPackage de controle do código-fonte
 Uma implementação de VSPackage de controle do código-fonte permite desenvolver uma substituição personalizada para a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface do usuário do controle do código-fonte. Essa abordagem fornece controle total sobre a integração de controle do código-fonte, mas requer que você forneça os elementos da interface do usuário e implemente as interfaces de controle do código-fonte que, de outra forma, seriam fornecidas sob a abordagem de plug-in.

 Para implementar um VSPackage de controle do código-fonte, você deve:

1. Crie e Registre seu próprio controle do código-fonte VSPackage, conforme descrito em [registro e seleção](../../extensibility/internals/registration-and-selection-source-control-vspackage.md).

2. Substitua a interface do usuário do controle do código-fonte por sua interface do usuário personalizada. Consulte [interface do usuário personalizada](../../extensibility/internals/custom-user-interface-source-control-vspackage.md).

3. Especifique os glifos a serem usados e manipule **Gerenciador de soluções** eventos de glifo. Consulte [controle de glifo](../../extensibility/internals/glyph-control-source-control-vspackage.md).

4. Manipule eventos de editar consulta e salvar consulta, conforme mostrado em [consulta editar consulta salvar](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md).

   Para obter mais informações, consulte [criando um controle do código-fonte VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md).

## <a name="see-also"></a>Confira também
- [Visão geral](../../extensibility/internals/source-control-integration-overview.md)
- [Criando um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)
