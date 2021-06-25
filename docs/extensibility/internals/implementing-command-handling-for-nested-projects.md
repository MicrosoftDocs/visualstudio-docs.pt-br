---
title: Implementando o tratamento de comandos para projetos aninhados | Microsoft Docs
description: Saiba como implementar a manipulação de comandos para projetos aninhados no Visual Studio IDE (ambiente de desenvolvimento integrado).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- nested projects, implementing command handling
ms.assetid: 48a9d66e-d51c-4376-a95a-15796643a9f2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4324e207d7b424295137f9523ed0bed538b3d806
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899980"
---
# <a name="implementing-command-handling-for-nested-projects"></a>Implementando a manipulação de comando para projetos aninhados
O IDE pode passar comandos que são passados por meio de e as interfaces para projetos aninhados ou projetos pai podem filtrar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ou substituir os comandos.

> [!NOTE]
> Somente comandos normalmente manipulados pelo projeto pai podem ser filtrados. Comandos como **Build e** **Implantação** que são manipulados pelo IDE não podem ser filtrados.

 As etapas a seguir descrevem o processo de implementação do tratamento de comandos.

## <a name="procedures"></a>Procedimentos

#### <a name="to-implement-command-handling"></a>Para implementar a manipulação de comandos

1. Quando o usuário seleciona um projeto aninhado ou um nó em um projeto aninhado:

   1. O IDE chama o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método .

      — ou —

   2. Se o comando tiver sido originado em uma janela de hierarquia, como um comando de menu de atalho no Gerenciador de Soluções, o IDE chamará o método no <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> pai do projeto.

2. O projeto pai pode examinar os parâmetros a serem passados para , como e , para determinar se o `QueryStatus` `pguidCmdGroup` projeto pai deve `prgCmds` filtrar os comandos. Se o projeto pai for implementado para filtrar comandos, ele deverá definir:

   ```
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;
   // make sure it is disabled
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;
   ```

    Em seguida, o projeto pai deve retornar `S_OK` .

    Se o projeto pai não filtrar o comando, ele deverá apenas retornar `S_OK` . Nesse caso, o IDE encaminha automaticamente o comando para o projeto filho.

    O projeto pai não precisa roteá-lo para o projeto filho. O IDE executa essa tarefa..

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [Comandos, menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md)
- [Aninhando projetos](../../extensibility/internals/nesting-projects.md)
