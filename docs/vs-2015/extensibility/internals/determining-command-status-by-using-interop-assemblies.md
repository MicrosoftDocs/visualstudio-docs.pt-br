---
title: Determinando o Status de comando usando Assemblies de interoperabilidade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1983f66158c00e5812823bbbf36eeea3aa139ea8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789298"
---
# <a name="determining-command-status-by-using-interop-assemblies"></a>Determinar o status do comando usando assemblies de interoperabilidade
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um VSPackage deve controlar do estado dos comandos que ele pode manipular. O ambiente não pode determinar quando um comando tratado dentro do seu VSPackage fica habilitado ou desabilitado. É responsabilidade do VSPackage para informar o ambiente sobre estados de comando, por exemplo, o estado do geral comandos como **Recortar**, **cópia**, e **colar**.  
  
## <a name="status-notification-sources"></a>Fontes de notificação de status  
 O ambiente recebe informações sobre comandos por meio de 'VSPackages <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método, que é parte da implementação do VSPackage do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. O ambiente chama o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método do VSPackage em duas condições:  
  
- Quando um usuário abre um menu principal ou um menu de contexto (clicando com o), o ambiente é executado o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método em todos os comandos no menu para determinar seu estado.  
  
- Quando o VSPackage solicita que o ambiente de atualizar a interface do usuário (UI) atual. Isso ocorre como comandos que estão atualmente visíveis para o usuário, como o **Recortar**, **cópia**, e **colar** de agrupamento na barra de ferramentas padrão, se tornar habilitado e desabilitado em resposta a ações do usuário e de contexto.  
  
  Uma vez que o shell hospeda vários VSPackages, desempenho do shell seria inaceitavelmente ser prejudicado se ele foi necessária para sondar cada VSPackage para determinar o status do comando. Em vez disso, o VSPackage ativamente deve notificar o ambiente quando sua interface do usuário é alterado no momento da alteração. Para obter mais informações sobre a notificação de atualização, consulte [atualizando a Interface do usuário](../../extensibility/updating-the-user-interface.md).  
  
## <a name="status-notification-failure"></a>Falha no status da notificação  
 Falha do VSPackage para notificar o ambiente de um comando de alteração de estado pode colocar a interface do usuário em um estado inconsistente. Lembre-se de que qualquer um dos seus comandos de menu de contexto ou menu pode ser colocado em uma barra de ferramentas pelo usuário. Portanto, atualizar a interface do usuário somente quando abre um menu ou menu de contexto não é suficiente.  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da Interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Implementação](../../extensibility/internals/command-implementation.md)

