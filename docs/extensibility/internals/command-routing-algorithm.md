---
title: Algoritmo de roteamento de comando | Microsoft Docs
description: Saiba mais sobre a ordem de resolução de comando no Visual Studio, pois comandos são tratados por componentes diferentes e roteados do contexto mais interno para o mais externo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing
ms.assetid: 998b616b-bd08-45cb-845f-808efb8c33bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0e02493cbb2f872806ade33d77609d45d1938ccd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057306"
---
# <a name="command-routing-algorithm"></a>Algoritmo de roteamento de comando
Nos comandos do Visual Studio são tratados por vários componentes diferentes. Os comandos são roteados do contexto mais interno, que é baseado na seleção atual, para o contexto mais externo (também conhecido como global). Para obter mais informações, consulte [disponibilidade de comando](../../extensibility/internals/command-availability.md).

## <a name="order-of-command-resolution"></a>Ordem de resolução de comando
 Os comandos são passados pelos seguintes níveis de contexto de comando:

1. Suplementos: o ambiente primeiro oferece o comando a todos os suplementos presentes.

2. Comandos de prioridade: esses comandos são registrados usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> . Eles são chamados para cada comando no Visual Studio e são chamados na ordem em que foram registrados.

3. Comandos do menu de contexto: um comando localizado em um menu de contexto é oferecido primeiro ao destino do comando que é fornecido ao menu de contexto e depois disso para o roteamento típico.

4. Destinos de comando Set da barra de ferramentas: esses destinos de comando são registrados quando você chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell4.SetupToolbar2%2A> . O `pCmdTarget` parâmetro pode ser `null` . Se não estiver `null` , esse destino de comando será usado para atualizar todos os comandos localizados na barra de ferramentas que você está configurando. Se o Shell estiver configurando sua barra de ferramentas, ele passará o quadro da janela como o `pCmdTarget` para que todas as atualizações dos comandos na barra de ferramentas fluam pelo quadro da janela, mesmo quando ela não estiver em foco.

5. Janela de ferramentas: janelas de ferramentas, que normalmente implementam a <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface, também devem implementar a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface para que o Visual Studio possa obter o destino de comando quando a janela de ferramentas for a janela ativa. No entanto, se a janela de ferramentas que tem o foco for a janela do **projeto** , o comando será roteado para a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface que é o pai comum dos itens selecionados. Se essa seleção abranger vários projetos, o comando será roteado para a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> hierarquia. A <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface contém os <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> métodos e que são análogos aos comandos correspondentes na <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface.

6. Janela de documento: se o comando tiver o `RouteToDocs` sinalizador definido em seu arquivo *. vsct* , o Visual Studio procurará um destino de comando no objeto de exibição de documento, que é uma instância de uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface ou uma instância de um objeto de documento (normalmente uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> interface ou <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> interface). Se o objeto de exibição de documento não oferecer suporte ao comando, o Visual Studio direcionará o comando para a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface que é retornada. (Essa é uma interface opcional para objetos de dados de documento.)

7. Hierarquia atual: a hierarquia atual pode ser o projeto que possui a janela de documento ativo ou a hierarquia selecionada no **Gerenciador de soluções**. O Visual Studio procura a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface implementada na hierarquia atual ou ativa. A hierarquia deve dar suporte a comandos que são válidos sempre que a hierarquia estiver ativa, mesmo se uma janela de documento de um item de projeto tiver foco. No entanto, os comandos que se aplicam somente quando **Gerenciador de soluções** tem foco devem ter suporte usando a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface e seus <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> métodos e.

     Os comandos **recortar**, **copiar**, **colar**, **excluir**, **renomear**, **Inserir** e **DoubleClick** exigem tratamento especial. Para obter informações sobre como tratar os comandos **delete** e **Remove** em hierarquias, consulte a <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler> interface.

8. Global: se um comando não tiver sido tratado pelos contextos mencionados anteriormente, o Visual Studio tentará circulá-lo para o VSPackage que possui um comando que implementa a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Se o VSPackage já não tiver sido carregado, ele não será carregado quando o Visual Studio chamar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método. O VSPackage é carregado somente quando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método é chamado.

## <a name="see-also"></a>Confira também
- [Design de comando](../../extensibility/internals/command-design.md)
