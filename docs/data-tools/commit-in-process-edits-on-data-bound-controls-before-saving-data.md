---
title: Edições não confirmadas
description: Confirmar edições em processo em controles de Windows Forms associados a dados antes de salvar dados. Chame EndEdit para todos os componentes BindingSource em um formulário.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- committing edited records
- data-bound controls, in-process edits
- DataBinding class, committing edited records
- hierarchical update, committing edited records
- BindingSource class, committing edited records
- EndEdit method
ms.assetid: 61af4798-eef7-468c-b229-5e1497febb2f
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 53101505230a51f109ace904c2f8322659733b4b
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216313"
---
# <a name="commit-in-process-edits-on-data-bound-controls-before-saving-data"></a>Confirmar edições no processo em controles associados a dados antes de salvar os dados

Ao editar valores em controles vinculados a dados, os usuários devem navegar para fora do registro atual para confirmar o valor atualizado para a fonte de dados subjacente à qual o controle está associado. Quando você arrasta itens da [janela fontes de dados](add-new-data-sources.md) para um formulário, o primeiro item que você remove gera código para o evento de clique do botão **salvar** do <xref:System.Windows.Forms.BindingNavigator> . Esse código chama o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método do <xref:System.Windows.Forms.BindingSource> . Portanto, a chamada para o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método é gerada somente para o primeiro <xref:System.Windows.Forms.BindingSource> que é adicionado ao formulário.

A chamada <xref:System.Windows.Forms.BindingSource.EndEdit%2A> confirma as alterações que estão em processo em qualquer controle de associação de dados sendo editado no momento. Portanto, se um controle associado a dados ainda estiver em foco e você clicar no botão **Salvar**, todas as edições pendentes nesse controle serão confirmadas antes da gravação real (o método `TableAdapterManager.UpdateAll`).

Você pode configurar seu aplicativo para confirmar as alterações automaticamente, mesmo se um usuário tentar salvar dados sem confirmar as alterações, como parte do processo de salvamento.

> [!NOTE]
> O designer adiciona o `BindingSource.EndEdit` código somente para o primeiro item descartado em um formulário. Portanto, você precisa adicionar uma linha de código para chamar o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método para cada <xref:System.Windows.Forms.BindingSource> no formulário. Você pode adicionar manualmente uma linha de código para chamar o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método para cada <xref:System.Windows.Forms.BindingSource> . Como alternativa, você pode adicionar o `EndEditOnAllBindingSources` método ao formulário e chamá-lo antes de executar um salvamento.

O código a seguir usa uma consulta [LINQ (consulta integrada à linguagem)](/dotnet/csharp/linq/) para iterar todos os <xref:System.Windows.Forms.BindingSource> componentes e chamar o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método para cada <xref:System.Windows.Forms.BindingSource> um em um formulário.

## <a name="to-call-endedit-for-all-bindingsource-components-on-a-form"></a>Para chamar EndEdit para todos os componentes BindingSource em um formulário

1. Adicione o código a seguir ao formulário que contém os <xref:System.Windows.Forms.BindingSource> componentes.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/CS/Form1.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/VB/Form1.vb" id="Snippet1":::

2. Adicione a seguinte linha de código imediatamente antes de qualquer chamada para salvar os dados do formulário (o `TableAdapterManager.UpdateAll()` método):

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/CS/Form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/VB/Form1.vb" id="Snippet2":::

## <a name="see-also"></a>Confira também

- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Atualização hierárquica](../data-tools/hierarchical-update.md)
