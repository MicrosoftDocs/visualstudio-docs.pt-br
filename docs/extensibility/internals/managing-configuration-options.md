---
title: Gerenciando opções de configuração | Microsoft Docs
description: Saiba como gerenciar definições de configuração de projeto e solução no Visual Studio para controlar como seu projeto será compilado, empacotado, implantado e executado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- configuration options
ms.assetid: 596c28ee-f48d-4252-a5c4-f730c43a39e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f773148f11a115ee82c8ee84a8d4668001908000
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095193"
---
# <a name="managing-configuration-options"></a>Gerenciando opções de configuração
Ao criar um novo tipo de projeto, você deve gerenciar definições de configuração de projeto e solução que determinam como seu projeto será compilado, empacotado, implantado e executado. Os tópicos a seguir abordam a configuração de projeto e solução.

## <a name="in-this-section"></a>Nesta seção
- [Visão geral](../../extensibility/internals/configuration-options-overview.md)

 Descreve como os projetos no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] podem dar suporte a várias configurações.

- [Páginas de propriedade](../../extensibility/internals/property-pages.md)

 Explica que os usuários podem exibir e alterar propriedades dependentes de configuração do projeto e propriedades independentes usando páginas de propriedades.

- [Configuração da solução](../../extensibility/internals/solution-configuration.md)

 Fornece informações sobre o que é armazenado nas configurações da solução e como as configurações de solução direcionam o comportamento dos comandos **Start** e **Build** .

- [Objeto de configuração de projeto](../../extensibility/internals/project-configuration-object.md)

 Explica como o objeto de configuração do projeto gerencia a exibição de informações de configuração para a interface do usuário.

- [Configuração de projeto para compilar](../../extensibility/internals/project-configuration-for-building.md)

 Explica como uma lista de configurações de solução para uma solução específica é gerenciada pela caixa de diálogo **configurações de solução** .

- [Configuração de projeto para gerenciar a implantação](../../extensibility/internals/project-configuration-for-managing-deployment.md)

 Define o ato de implantação e as duas maneiras de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] suporte a projetos que dão suporte à implantação.

- [Configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md)

 Explica os processos de compilação para os quais cada configuração pode dar suporte e as interfaces e métodos pelos quais os itens de saída podem ser disponibilizados.

## <a name="related-sections"></a>Seções relacionadas
- [Tipos de Projeto](../../extensibility/internals/project-types.md)

 Fornece uma visão geral dos projetos como os blocos de construção básicos do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado). São fornecidos links para tópicos adicionais que explicam como os projetos controlam a criação e a compilação de código.
