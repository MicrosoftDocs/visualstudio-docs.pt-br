---
title: 'Como: abrir editores padrão | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening
- projects [Visual Studio SDK], opening standard editors
ms.assetid: d5ce10f9-047a-4b74-aa1d-295128898b89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c12e831654e7e138289d33b6e6f0409328e22c8c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905787"
---
# <a name="how-to-open-standard-editors"></a>Como: abrir editores padrão
Quando você abre um editor padrão, permite que o IDE determine um editor padrão para um tipo de arquivo designado, em vez de especificar um editor específico do projeto para o arquivo.

 Conclua o procedimento a seguir para implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> método. Isso abrirá um arquivo de projeto em um editor padrão.

## <a name="to-implement-the-openitem-method-with-a-standard-editor"></a>Para implementar o método OpenItem com um editor padrão

1. Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> ( `RDT_EditLock` ) para determinar se o arquivo de objeto de dados do documento já está aberto.

2. Se o arquivo já estiver aberto, reponha o arquivo chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> método, especificando um valor de `IDO_ActivateIfOpen` para o `grfIDO` parâmetro.

     Se o arquivo estiver aberto e o documento pertencer a um projeto diferente do projeto de chamada, seu projeto receberá um aviso de que o editor que está sendo aberto é de outro projeto. A janela de arquivo é, então, na superfície.

3. Se o documento não estiver aberto ou não estiver na tabela de documentos em execução, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método ( `OSE_ChooseBestStdEditor` ) para abrir um editor padrão para o arquivo.

     Quando você chama o método, o IDE executa as seguintes tarefas:

    1. O IDE examina a subchave editores/{guidEditorType}/Extensions no registro para determinar qual editor pode abrir o arquivo e tem a prioridade mais alta para fazer isso.

    2. Depois que o IDE tiver determinado qual editor pode abrir o arquivo, o IDE chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> . A implementação do editor desse método retorna informações necessárias para o IDE chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> e site o documento recentemente aberto.

    3. Por fim, o IDE carrega o documento usando a interface de persistência usual, como <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> .

    4. Se o IDE tiver determinado anteriormente que o item de hierarquia ou hierarquia está disponível, o IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> método no projeto para obter um ponteiro de contexto de nível de projeto <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> para retransmiti-lo com a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> chamada de método.

4. Retorne um <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> ponteiro para o IDE quando o IDE chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> seu projeto se você quiser permitir que o editor obtenha o contexto do seu projeto.

     A execução dessa etapa permite que o projeto ofereça serviços adicionais ao editor.

     Se o objeto de exibição de documento ou de exibição de documento tiver sido site com êxito em um quadro de janela, o objeto será inicializado com seus dados chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.LoadDocData%2A> .

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [Abrir e salvar itens de projeto](../extensibility/internals/opening-and-saving-project-items.md)
- [Como: abrir editores específicos do projeto](../extensibility/how-to-open-project-specific-editors.md)
- [Como abrir editores para documentos abertos](../extensibility/how-to-open-editors-for-open-documents.md)
- [Exibir arquivos usando o comando abrir arquivo](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
