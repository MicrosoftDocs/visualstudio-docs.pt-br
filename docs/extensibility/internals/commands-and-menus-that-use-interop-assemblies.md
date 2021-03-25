---
title: Comandos e menus que usam assemblies de interoperabilidade | Microsoft Docs
description: Saiba mais sobre as tarefas que devem ser concluídas ao implementar comandos de menu e barra de ferramentas em um VSPackage usando assemblies de interoperabilidade.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, using interop assemblies
- interop assemblies, using in commands and menus
- commands, handling using interop assemblies
- command handling with interop assemblies
ms.assetid: 8f4af525-39e5-4e69-92c8-d3efabe80bb2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b5a487c2fe6f97e338924a0b8c682f9dd9798571
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057228"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>Comandos e menus que usam assemblies de interoperabilidade
Um VSPackage que implementa comandos de menu e barra de ferramentas usando assemblies de interoperabilidade deve:

- Informe o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE) sobre os comandos que ele suporta e se eles estão habilitados no momento.

- Siga as regras (contrato) para manipular comandos.

- Implemente explicitamente o tratamento de comandos usando <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface ou.

  A seção a seguir descreve como executar essas tarefas.

## <a name="in-this-section"></a>Nesta seção
- [Determinar o status do comando usando assemblies de interoperabilidade](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)

 Descreve como um VSPackage notifica o IDE sobre quais comandos ele suporta e se eles estão habilitados no momento.

- [Contratos de comando em assemblies de interoperabilidade](../../extensibility/internals/command-contracts-in-interop-assemblies.md)

 Fornece uma definição do contrato de comando básico usado por todos os VSPackages implementando comandos usando assemblies de interoperabilidade.

- [Implementação de comando](../../extensibility/internals/command-implementation.md)

 Fornece uma visão geral de como um VSPackage implementa um comando.

- [Registrar manipuladores de comando do assembly de interoperabilidade](../../extensibility/internals/registering-interop-assembly-command-handlers.md)

 Descreve as entradas de Registro necessárias para notificar o IDE que um VSPackage fornece um manipulador de comando.

## <a name="related-sections"></a>Seções relacionadas
- [Disponibilidade do comando](../../extensibility/internals/command-availability.md)

 Descreve os critérios usados pelo IDE para determinar quais comandos VSPackage estão disponíveis e qual objeto manipula-os.

- [Como VSPackages adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 Fornece detalhes sobre como criar uma interface do usuário que usa o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] suporte a comandos.

- [Roteamento de comandos em VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)

 Uma visão geral do processo usado para relacionar um objeto com a solicitação de comando correta.
