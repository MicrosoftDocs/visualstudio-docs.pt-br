---
title: Algoritmo de roteamento de comando | Microsoft Docs
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
- commands, routing
- command routing
ms.assetid: 998b616b-bd08-45cb-845f-808efb8c33bc
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 44fc431f008c59a7d4ceff2d9b9ec14d85091daf
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727999"
---
# <a name="command-routing-algorithm"></a>Algoritmo de roteamento de comando
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

No Visual Studio comandos são tratados por um número de diferentes componentes. Comandos são roteados do contexto interno, que se baseia na seleção atual, para o contexto mais externo de (também conhecido como global). Para obter mais informações, consulte [disponibilidade](../../extensibility/internals/command-availability.md).  
  
## <a name="order-of-command-resolution"></a>Ordem de resolução de comando  
 Comandos são passados para os seguintes níveis de contexto do comando:  
  
1.  Suplementos: O ambiente primeiro oferece o comando para quaisquer suplementos que estão presentes.  
  
2.  Comandos de prioridade: esses comandos são registrados usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget>. Eles são chamados para cada comando no Visual Studio e são chamados na ordem em que eles foram registrados.  
  
3.  Comandos de menu de contexto: um comando localizado em um menu de contexto é oferecido pela primeira vez para o destino do comando que é fornecido para o menu de contexto e, depois disso para o roteamento típico.  
  
4.  Barra de ferramentas do conjunto de destinos de comando: esses destinos de comando são registrados quando você chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell4.SetupToolbar2%2A>. O `pCmdTarget` parâmetro pode ser `null`. Se não for `null`, em seguida, o destino do comando é usado para atualizar todos os comandos localizados na barra de ferramentas que você está configurando. Se o shell é a configuração sua barra de ferramentas, ele passa o quadro de janela como o `pCmdTarget` , de modo que todas as atualizações para os comandos em seu fluxo de barra de ferramentas por meio do quadro de janela, mesmo quando ele não estiver em foco.  
  
5.  Janela de ferramenta: Janelas, que normalmente implementam o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface, também deve implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface para que o Visual Studio pode obter o destino do comando quando a janela de ferramentas é a janela ativa. No entanto, se a janela da ferramenta que tem foco é a **Project** janela e, em seguida, o comando é roteado para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface que é o pai comum dos itens selecionados. Se essa seleção se estender por vários projetos, o comando é roteado para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> hierarquia. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface contém o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> métodos que são análogos aos comandos correspondentes no <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface.  
  
6.  Janela de documento: Se o comando tem o sinalizador de RouteToDocs definido em seu arquivo. VSCT, Visual Studio procura por um destino do comando no objeto de exibição de documento, que é uma instância de um <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface ou uma instância de um objeto de documento (normalmente um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>interface ou um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> interface). Se o objeto de exibição de documento não dá suporte para o comando, o Visual Studio encaminha o comando para o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface que é retornado. (Isso é uma interface opcional para objetos de dados de documento).  
  
7.  Hierarquia atual: A hierarquia atual pode ser o projeto que possui a janela de documento ativo ou a hierarquia que está selecionada na **Gerenciador de soluções**. Visual Studio procura o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface é implementada na hierarquia atual ou ativa. A hierarquia deve dar suporte a comandos válidos sempre que a hierarquia está ativa, mesmo se uma janela do documento de um item de projeto tem o foco. No entanto, comandos que se aplicam somente quando **Gerenciador de soluções** tem foco deve ter suporte usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface e seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>métodos.  
  
     **Recortar**, **cópia**, **colar**, **excluir**, **Renomear**, **insira**e **DoubleClick** comandos exigem tratamento especial. Para obter informações sobre como manipular **exclua** e **remover** comandos em hierarquias, consulte o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler> interface.  
  
8.  Global: Se um comando não foi tratado pelos contextos mencionados anteriormente, o Visual Studio tenta encaminhá-lo para o VSPackage que possui um comando que implementa o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Se o VSPackage já não foi carregado, ele não será carregado quando o Visual Studio chama o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método. O VSPackage é carregado somente quando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método é chamado.  
  
## <a name="see-also"></a>Consulte também  
 [Design de comando](../../extensibility/internals/command-design.md)

