---
title: Detalhes de configuração de controle de origem | Microsoft Docs
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
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 55e2364ca096b5329369e51ccdadf07f191720e8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753704"
---
# <a name="source-control-configuration-details"></a>Detalhes de configuração de controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para implementar o controle do código-fonte, você precisa configurar corretamente o sistema de projeto ou o editor para fazer o seguinte:  
  
-   Solicitar permissão para fazer a transição para estado alterado  
  
-   Solicitar permissão para salvar um arquivo  
  
-   Solicitar permissão para adicionar, remover ou renomear arquivos no projeto  
  
## <a name="request-permission-to-transition-to-changed-state"></a>Solicitar permissão para fazer a transição para estado alterado  
 Um editor ou projeto deve solicitar permissão para fazer a transição para o estado de alteração (sujo) chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>. Cada editor que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> deve chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> e receber aprovação para alterar o documento do ambiente antes de retornar `True` para `M:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty(System.Int32@)`. Um projeto é essencialmente um editor para um arquivo de projeto e tem como resultado, a responsabilidade de mesma para implementar o acompanhamento de estado alterado para o arquivo de projeto como um editor de texto faz para seus arquivos. O ambiente manipula o estado alterado da solução, mas você deve lidar com o estado de alteração de qualquer objeto na solução faz referência, mas não armazena, como um arquivo de projeto ou seus itens. Em geral, se seu projeto ou o editor é responsável por gerenciar a persistência para um item, é responsável por implementar o acompanhamento de estado alterado.  
  
 Em resposta ao `IVsQueryEditQuerySave2::QueryEditFiles` chamar, o ambiente pode fazer o seguinte:  
  
- Rejeitar a chamada para alterar, caso em que o editor ou projeto deve permanecer no estado inalterado (limpo).  
  
- Indicam que os dados do documento devem ser recarregados. Para um projeto, o ambiente será recarregar os dados para o projeto. Um editor deve recarregar os dados do disco por meio de seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> implementação. Em ambos os casos, o contexto no projeto ou no editor pode ser alterado quando os dados são recarregados.  
  
  É uma tarefa complexa e difícil fazer ajustes apropriados `IVsQueryEditQuerySave2::QueryEditFiles` chamadas em uma base de código existente. Como resultado, essas chamadas devem ser integradas durante a criação do projeto ou no editor.  
  
## <a name="request-permission-to-save-a-file"></a>Solicitar permissão para salvar um arquivo  
 Antes de um editor ou projeto salva um arquivo, ele deve chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>. Para arquivos de projeto, essas chamadas são concluídas automaticamente pela solução, que saiba quando salvar um arquivo de projeto. Editores são responsáveis por fazer essas chamadas, a menos que a implementação do editor de `IVsPersistDocData2` usa a função auxiliar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>. Se o editor implementa `IVsPersistDocData2` dessa maneira e, em seguida, a chamada para `IVsQueryEditQuerySave2::QuerySaveFile` ou `IVsQueryEditQuerySave2::QuerySaveFiles` é feita para você.  
  
> [!NOTE]
>  Sempre fazer essas chamadas preventivamente — ou seja, quando o editor for capaz de receber um cancelamento.  
  
## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>Solicitar permissão para adicionar, remover ou renomear arquivos no projeto  
 Antes de um projeto pode adicionar, renomear ou remover um arquivo ou diretório, deve chamar apropriado `IVsTrackProjectDocuments2::OnQuery*` método solicitar permissão do ambiente. Se a permissão é concedida, o projeto deve concluir a operação e, em seguida, chamar o `IVsTrackProjectDocuments2::OnAfter*` método para notificar o ambiente de que a operação foi concluída. O projeto deve chamar os métodos do <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> interface para todos os arquivos (por exemplo, arquivos especiais) e não apenas os arquivos do pai. Chamadas de arquivo são obrigatórias, mas as chamadas de diretório são opcionais. Se seu projeto tiver informações de diretório, ele deverá chamar apropriado <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> métodos, mas se ele não tiver essas informações, o ambiente irá inferir informações de diretório.  
  
 O projeto não deve chamar os métodos de `IVsTrackProjectDocuments2` no projeto abrir ou fechar. Os ouvintes que quiser que essas informações durante a inicialização podem aguardar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> eventos e iterar por meio da solução para localizar as informações necessárias. Durante o desligamento, essa informação não é necessária. `IVsTrackProjectDocuments2` é fornecido pela <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>.  
  
 Para cada adicionar, renomear e remover ação, há um `OnQuery*` método e um `OnAfter*` método. Chamar o `OnQuery*` método pedir permissão para adicionar, renomear ou remover o arquivo ou diretório. Chamar o `OnAfter*` método depois que o arquivo ou diretório foi adicionado, renomeado ou removido e o estado do projeto reflete o novo estado.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>   
 [Oferecer suporte ao controle do código-fonte](../../extensibility/internals/supporting-source-control.md)

