---
title: Suporte a vários modos de exibição de documento | Microsoft Docs
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
- editors [Visual Studio SDK], custom - multiple document views
ms.assetid: c7ec2366-91c4-477f-908d-e89068bdb3e3
caps.latest.revision: 26
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6be1e48917c8ad5e7035f01caa4f74b78a6fa3d0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792249"
---
# <a name="supporting-multiple-document-views"></a>Dando suporte a várias exibições de documento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode fornecer mais de uma exibição de um documento com a criação de dados de documento separado e objetos de exibição de documento para que o editor. Alguns casos em que uma exibição de documento adicional seria útil são:  
  
- Novo suporte de janela: você deseja que seu editor para fornecer dois ou mais exibições do mesmo tipo, para que um usuário que já tem uma janela Abrir no editor pode abrir uma nova janela, selecionando o **nova janela** comando do **janela** menu.  
  
- Exibir o formulário e o código de suporte: você deseja que o editor fornecer modos de exibição de tipos diferentes. [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], por exemplo, fornece um modo de exibição de formulário e um modo de exibição de código.  
  
  Para obter mais informações sobre isso, consulte o procedimento de CreateEditorInstance no arquivo EditorFactory.cs no projeto do editor personalizado criado pelo modelo de pacote do Visual Studio. Para obter mais informações sobre esse projeto, consulte [instruções passo a passo: Criando um Editor personalizado](../extensibility/walkthrough-creating-a-custom-editor.md).  
  
## <a name="synchronizing-views"></a>Sincronizando modos de exibição  
 Quando você implementa vários modos de exibição, o objeto de dados de documento é responsável por manter sincronizadas com os dados de todas as exibições. Você pode usar o evento tratamento interfaces em <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> para sincronizar vários modos de exibição com os dados.  
  
 Se você não usar o <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> objeto para sincronizar vários modos de exibição, em seguida, você deve implementar seu próprio sistema de eventos para manipular as alterações feitas no objeto de dados do documento. Você pode usar diferentes níveis de granularidade para manter vários modos de exibição atualizado. Com uma configuração de granularidade máxima, conforme você digita em um modo de exibição os outros modos de exibição são atualizados imediatamente. Com a granularidade mínima, outros modos de exibição não são atualizados até que elas são habilitadas.  
  
## <a name="determining-whether-document-data-is-already-open"></a>Determinando os dados de documento se ainda estiver aberto  
 A tabela de documento (RDT) em execução no ambiente de desenvolvimento integrado (IDE) ajuda a controlar se os dados para um documento já estão abertos, conforme mostrado no diagrama a seguir.  
  
 ![Gráfico de DocDataView](../extensibility/media/docdataview.gif "Docdataview")  
Vários modos de exibição  
  
 Por padrão, cada modo de exibição (objeto de exibição de documento) está contido no seu próprio quadro de janela (<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>). Como já observamos, no entanto, os dados de documento podem ser exibidos em vários modos de exibição. Para habilitar isso, o Visual Studio verifica o RDT para determinar se o documento em questão já está aberto em um editor. Quando chama o IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> para criar o editor, um valor não nulo é retornado no `punkDocDataExisting` parâmetro indica que o documento já está aberto em outro editor. Para obter mais informações sobre como as funções RDT, consulte [tabela de documento em execução](../extensibility/internals/running-document-table.md).  
  
 No seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> implementação, examinar o objeto de dados de documento retornado no `punkDocDataExisting` para determinar se os dados do documento são apropriados para seu editor. (Por exemplo, apenas os dados HTML devem ser exibidos por um editor de HTML.) Se for o caso, sua fábrica de editor deve fornecer um segundo modo de exibição para os dados. Se o `punkDocDataExisting` parâmetro não é `NULL`, é possível também que o objeto de dados de documento é aberto em outro editor, ou, mais provável, que os dados do documento já estão abertos em uma exibição diferente com o mesmo editor. Se os dados do documento estão abertos em um editor diferente que não dão suporte à sua fábrica de editor, o Visual Studio falhará abrir sua fábrica de editor. Para obter mais informações, consulte [como: anexar exibições para dados de documento](../extensibility/how-to-attach-views-to-document-data.md).

