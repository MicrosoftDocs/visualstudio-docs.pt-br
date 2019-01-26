---
title: Suporte a vários modos de exibição de documento | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - multiple document views
ms.assetid: c7ec2366-91c4-477f-908d-e89068bdb3e3
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ba85e4a6974330cf28ce6ef3f1c30c6688765802
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54956331"
---
# <a name="supporting-multiple-document-views"></a>Dando suporte a várias exibições de documento
Você pode fornecer mais de uma exibição de um documento com a criação de dados de documento separado e objetos de exibição de documento para que o editor. Alguns casos em que uma exibição de documento adicional seria útil são:  
  
- Novo suporte de janela: Você deseja que seu editor para fornecer dois ou mais exibições do mesmo tipo, para que um usuário que já tem uma janela Abrir no editor pode abrir uma nova janela, selecionando o **nova janela** comando da **janela** menu.  
  
- Suporte de modo de exibição de formulário e o código: Você deseja que o editor fornecer modos de exibição de tipos diferentes. [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], por exemplo, fornece um modo de exibição de formulário e um modo de exibição de código.  
  
  Para obter mais informações sobre isso, consulte o procedimento de CreateEditorInstance no arquivo EditorFactory.cs no projeto do editor personalizado criado pelo modelo de pacote do Visual Studio. Para obter mais informações sobre esse projeto, consulte [passo a passo: Criar um Editor personalizado](../extensibility/walkthrough-creating-a-custom-editor.md).  
  
## <a name="synchronizing-views"></a>Sincronizando modos de exibição  
 Quando você implementa vários modos de exibição, o objeto de dados de documento é responsável por manter sincronizadas com os dados de todas as exibições. Você pode usar o evento tratamento interfaces em <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> para sincronizar vários modos de exibição com os dados.  
  
 Se você não usar o <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> objeto para sincronizar vários modos de exibição, em seguida, você deve implementar seu próprio sistema de eventos para manipular as alterações feitas no objeto de dados do documento. Você pode usar diferentes níveis de granularidade para manter vários modos de exibição atualizado. Com uma configuração de granularidade máxima, conforme você digita em um modo de exibição os outros modos de exibição são atualizados imediatamente. Com a granularidade mínima, outros modos de exibição não são atualizados até que elas são habilitadas.  
  
## <a name="determining-whether-document-data-is-already-open"></a>Determinando os dados de documento se ainda estiver aberto  
 A tabela de documento (RDT) em execução no ambiente de desenvolvimento integrado (IDE) ajuda a controlar se os dados para um documento já estão abertos, conforme mostrado no diagrama a seguir.  
  
 ![Gráfico de DocDataView](../extensibility/media/docdataview.gif "Docdataview")  
Vários modos de exibição  
  
 Por padrão, cada modo de exibição (objeto de exibição de documento) está contido no seu próprio quadro de janela (<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>). Como já observamos, no entanto, os dados de documento podem ser exibidos em vários modos de exibição. Para habilitar isso, o Visual Studio verifica o RDT para determinar se o documento em questão já está aberto em um editor. Quando chama o IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> para criar o editor, um valor não nulo é retornado no `punkDocDataExisting` parâmetro indica que o documento já está aberto em outro editor. Para obter mais informações sobre como as funções RDT, consulte [tabela de documento em execução](../extensibility/internals/running-document-table.md).  
  
 No seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> implementação, examinar o objeto de dados de documento retornado no `punkDocDataExisting` para determinar se os dados do documento são apropriados para seu editor. (Por exemplo, apenas os dados HTML devem ser exibidos por um editor de HTML.) Se for o caso, sua fábrica de editor deve fornecer um segundo modo de exibição para os dados. Se o `punkDocDataExisting` parâmetro não é `NULL`, é possível também que o objeto de dados de documento é aberto em outro editor, ou, mais provável, que os dados do documento já estão abertos em uma exibição diferente com o mesmo editor. Se os dados do documento estão abertos em um editor diferente que não dão suporte à sua fábrica de editor, o Visual Studio falhará abrir sua fábrica de editor. Para obter mais informações, confira [Como: Anexar exibições para dados de documentos](../extensibility/how-to-attach-views-to-document-data.md).