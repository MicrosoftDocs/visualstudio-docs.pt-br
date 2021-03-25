---
title: Determinando o status do comando usando assemblies de interoperabilidade | Microsoft Docs
description: Saiba como determinar o status dos comandos que são manipulados em um VSPackage, usando a interface Microsoft. VisualStudio. OLE. Interop. IOleCommandTarget.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ef6940aef83ad3865385b4e39fd9cfd62b8866d7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090896"
---
# <a name="determine-command-status-by-using-interop-assemblies"></a>Determinar o status do comando usando assemblies de interoperabilidade
Um VSPackage deve acompanhar o estado dos comandos que ele pode manipular. O ambiente não pode determinar quando um comando manipulado em seu VSPackage se torna habilitado ou desabilitado. É responsabilidade do seu VSPackage informar o ambiente sobre os Estados de comando, por exemplo, o estado de comandos gerais, como **recortar**, **copiar** e **colar**.

## <a name="status-notification-sources"></a>Fontes de notificação de status
 O ambiente recebe informações sobre comandos por meio do método VSPackages ' <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> , que faz parte da implementação da interface do VSPackage <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> . O ambiente chama o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método de VSPackage em duas condições:

- Quando um usuário abre um menu principal ou um menu de contexto (clicando com o botão direito do mouse), o ambiente executa o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método em todos os comandos nesse menu para determinar seu estado.

- Quando o VSPackage solicita que o ambiente atualize a interface do usuário atual (IU). Essa atualização ocorre como comandos visíveis no momento para o usuário, como o agrupamento **recortar**, **copiar** e **colar** na barra de ferramentas padrão, torna-se habilitado e desabilitado em resposta a contexto e ações do usuário.

  Como o Shell hospeda vários VSPackages, o desempenho do Shell seria inaceitável se fosse necessário para sondar cada VSPackage para determinar o status do comando. Em vez disso, seu VSPackage deve notificar o ambiente ativamente quando sua interface do usuário é alterada no momento da alteração. Para obter mais informações sobre a notificação de atualização, consulte [atualizar a interface do usuário](../../extensibility/updating-the-user-interface.md).

## <a name="status-notification-failure"></a>Falha na notificação de status
 Falha de seu VSPackage para notificar o ambiente de uma alteração de estado de comando pode posicionar a interface do usuário em um estado inconsistente. Lembre-se de que qualquer um dos comandos menu ou menu de contexto pode ser colocado em uma barra de ferramentas pelo usuário. Portanto, atualizar a interface do usuário somente quando um menu ou menu de contexto é aberto não é suficiente.

## <a name="see-also"></a>Confira também
- [Como VSPackages adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Implementação](../../extensibility/internals/command-implementation.md)
