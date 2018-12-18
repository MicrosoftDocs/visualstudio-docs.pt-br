---
title: Determinando o Status de comando usando Assemblies de interoperabilidade | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9b678e5a7ab87df69ec5f3f41f65a191ecf35911
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49822547"
---
# <a name="determine-command-status-by-using-interop-assemblies"></a>Determinar o status de comando usando assemblies de interoperabilidade
Um VSPackage deve controlar do estado dos comandos que ele pode manipular. O ambiente não pode determinar quando um comando tratado dentro do seu VSPackage fica habilitado ou desabilitado. É responsabilidade do VSPackage para informar o ambiente sobre estados de comando, por exemplo, o estado do geral comandos como **Recortar**, **cópia**, e **colar**.  
  
## <a name="status-notification-sources"></a>Fontes de notificação de status  
 O ambiente recebe informações sobre comandos por meio de 'VSPackages <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método, que é parte da implementação do VSPackage do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. O ambiente chama o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método do VSPackage em duas condições:  
  
- Quando um usuário abre um menu principal ou um menu de contexto (clicando com o), o ambiente é executado o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método em todos os comandos no menu para determinar seu estado.  
  
- Quando o VSPackage solicita que o ambiente de atualizar a interface do usuário (UI) atual. Essa atualização ocorre como comandos que estão atualmente visíveis para o usuário, como o **Recortar**, **cópia**, e **colar** de agrupamento na barra de ferramentas padrão, se tornam habilitados e desabilitados em resposta às ações de contexto e o usuário.  
  
  Uma vez que o shell hospeda vários VSPackages, desempenho do shell seria inaceitavelmente ser prejudicado se ele foi necessária para sondar cada VSPackage para determinar o status do comando. Em vez disso, o VSPackage ativamente deve notificar o ambiente quando sua interface do usuário é alterado no momento da alteração. Para obter mais informações sobre a notificação de atualização, consulte [atualizar a interface do usuário](../../extensibility/updating-the-user-interface.md).  
  
## <a name="status-notification-failure"></a>Falha no status da notificação  
 Falha do VSPackage para notificar o ambiente de um comando de alteração de estado pode colocar a interface do usuário em um estado inconsistente. Lembre-se de que qualquer um dos seus comandos de menu de contexto ou menu pode ser colocado em uma barra de ferramentas pelo usuário. Portanto, atualizar a interface do usuário somente quando abre um menu ou menu de contexto não é suficiente.  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Implementação](../../extensibility/internals/command-implementation.md)