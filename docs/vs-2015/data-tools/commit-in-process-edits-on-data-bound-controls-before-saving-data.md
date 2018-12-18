---
title: Confirmar edições em processo em controles ligados a dados antes de salvar dados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- commiting edited records
- data-bound controls, in-process edits
- DataBinding class, commiting edited records
- hierarchical update, commiting edited records
- BindingSource class, commiting edited records
- EndEdit method
ms.assetid: 61af4798-eef7-468c-b229-5e1497febb2f
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 3af1534e6436eec2eac1f294be8c2428c949ce9d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49296018"
---
# <a name="commit-in-process-edits-on-data-bound-controls-before-saving-data"></a>Confirmar edições no processo em controles associados a dados antes de salvar os dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Ao editar valores em controles ligados a dados, os usuários devem navegar fora do registro atual para confirmar o valor atualizado para a fonte de dados subjacente que o controle está vinculado. Quando você arrasta itens da [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) para um formulário, o primeiro item que você solta gera código para o **salve** eventos de clique de botão a <xref:System.Windows.Forms.BindingNavigator>. Esse código chama o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método da <xref:System.Windows.Forms.BindingSource>. Portanto, a chamada para o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método é gerado somente para o primeiro <xref:System.Windows.Forms.BindingSource> que é adicionado ao formulário.  
  
 O <xref:System.Windows.Forms.BindingSource.EndEdit%2A> chamada confirma as alterações que estão em processo, em todos os controles ligados a dados que estão sendo editados atualmente. Portanto, se um controle associado a dados ainda tem foco e você clicar o **salve** botão, todas as edições pendentes nesse controle serão confirmadas antes da gravação real (o `TableAdapterManager.UpdateAll` método).  
  
 Você pode configurar seu aplicativo para confirmar as alterações, automaticamente, mesmo se um usuário tenta salvar os dados sem confirmar as alterações, como parte do salvamento processo.  
  
> [!NOTE]
>  O designer adiciona a `BindingSource.EndEdit` código somente para o primeiro item é solto em um formulário. Portanto, você precisa adicionar uma linha de código para chamar o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método para cada <xref:System.Windows.Forms.BindingSource> no formulário. Você pode adicionar manualmente uma linha de código para chamar o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método para cada <xref:System.Windows.Forms.BindingSource>. Como alternativa, você pode adicionar o `EndEditOnAllBindingSources` método ao formulário e chamá-lo antes de salvar.  
  
 O código a seguir usa uma [LINQ (consulta integrada à linguagem)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) consulta para iterar todas <xref:System.Windows.Forms.BindingSource> componentes e chame o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método para cada <xref:System.Windows.Forms.BindingSource> em um formulário.  
  
## <a name="to-call-endedit-for-all-bindingsource-components-on-a-form"></a>Para chamar EndEdit para todos os componentes de BindingSource em um formulário  
  
1.  Adicione o seguinte código ao formulário que contém o <xref:System.Windows.Forms.BindingSource> componentes.  
  
     [!code-csharp[VSProDataOrcasEndEditOnAll#1](../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/CS/Form1.cs#1)]
     [!code-vb[VSProDataOrcasEndEditOnAll#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/VB/Form1.vb#1)]  
  
2.  Adicione a seguinte linha de código imediatamente antes de quaisquer chamadas para salvar os dados do formulário (o `TableAdapterManager.UpdateAll()` método):  
  
     [!code-csharp[VSProDataOrcasEndEditOnAll#2](../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/CS/Form1.cs#2)]
     [!code-vb[VSProDataOrcasEndEditOnAll#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/VB/Form1.vb#2)]  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Atualização hierárquica](../data-tools/hierarchical-update.md)

