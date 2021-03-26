---
title: Detalhes de configuração do controle do código-fonte | Microsoft Docs
description: Saiba como implementar o controle do código-fonte para um tipo de projeto no Visual Studio, que envolve a configuração do seu sistema ou editor de projeto para solicitar permissões.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a5c93e690922057116b395bed3881627e8a37847
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069342"
---
# <a name="source-control-configuration-details"></a>Detalhes de configuração de controle do código-fonte
Para implementar o controle do código-fonte, você precisa configurar corretamente seu sistema ou editor de projeto para fazer o seguinte:

- Solicitar permissão para passar para o estado alterado

- Solicitar permissão para salvar um arquivo

- Solicitar permissão para adicionar, remover ou renomear arquivos no projeto

## <a name="request-permission-to-transition-to-changed-state"></a>Solicitar permissão para passar para o estado alterado
 Um projeto ou editor deve solicitar permissão para fazer a transição para o estado alterado (sujo) chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> . Cada editor que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> o deve chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> e receber aprovação para alterar o documento do ambiente antes de retornar `True` para <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> . Um projeto é essencialmente um editor para um arquivo de projeto e, consequentemente, tem a mesma responsabilidade de implementar o acompanhamento de estado alterado para o arquivo de projeto como um editor de texto para seus arquivos. O ambiente manipula o estado alterado da solução, mas você deve manipular o estado alterado de qualquer objeto que a solução faz referência, mas não armazena, como um arquivo de projeto ou seus itens. Em geral, se seu projeto ou editor for responsável por gerenciar a persistência de um item, ele será responsável por implementar o acompanhamento de estado alterado.

 Em resposta à `IVsQueryEditQuerySave2::QueryEditFiles` chamada, o ambiente pode fazer o seguinte:

- Rejeite a chamada para alterar, caso em que o editor ou projeto deve permanecer no estado inalterado (limpo).

- Indique que os dados do documento devem ser recarregados. Para um projeto, o ambiente recarregará os dados para o projeto. Um editor deve recarregar os dados do disco por meio de sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> implementação. Em ambos os casos, o contexto no projeto ou editor pode ser alterado quando os dados são recarregados.

  É uma tarefa complexa e difícil de adaptar as `IVsQueryEditQuerySave2::QueryEditFiles` chamadas apropriadas para uma base de código existente. Como resultado, essas chamadas devem ser integradas durante a criação do projeto ou editor.

## <a name="request-permission-to-save-a-file"></a>Solicitar permissão para salvar um arquivo
 Antes que um projeto ou editor salve um arquivo, ele deve chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> . Para arquivos de projeto, essas chamadas são automaticamente concluídas pela solução, que sabe quando salvar um arquivo de projeto. Os editores são responsáveis por fazer essas chamadas, a menos que a implementação do editor do `IVsPersistDocData2` use a função auxiliar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> . Se o seu editor for implementado `IVsPersistDocData2` dessa forma, a chamada para `IVsQueryEditQuerySave2::QuerySaveFile` ou `IVsQueryEditQuerySave2::QuerySaveFiles` será feita para você.

> [!NOTE]
> Sempre faça essas chamadas preemptivas, ou seja, por vez, quando o editor for capaz de receber um cancelamento.

## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>Solicitar permissão para adicionar, remover ou renomear arquivos no projeto
 Antes que um projeto possa adicionar, renomear ou remover um arquivo ou diretório, ele deve chamar o `IVsTrackProjectDocuments2::OnQuery*` método apropriado para solicitar permissão do ambiente. Se a permissão for concedida, o projeto deverá concluir a operação e, em seguida, chamar o `IVsTrackProjectDocuments2::OnAfter*` método apropriado para notificar o ambiente de que a operação foi concluída. O projeto deve chamar os métodos da <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> interface para todos os arquivos (por exemplo, arquivos especiais) e não apenas os arquivos pai. As chamadas de arquivo são obrigatórias, mas as chamadas de diretório são opcionais. Se o seu projeto tiver informações de diretório, ele deverá chamar os <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> métodos apropriados, mas se não tiver essas informações, o ambiente inferirá as informações de diretório.

 O projeto não deve chamar os métodos de `IVsTrackProjectDocuments2` no projeto aberto ou fechado. Os ouvintes que desejam essas informações na inicialização podem aguardar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> evento e iterar pela solução para encontrar as informações de que precisam. Ao desligar, essas informações não são necessárias. `IVsTrackProjectDocuments2` é fornecido do <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> .

 Para cada ação adicionar, renomear e remover, há um `OnQuery*` método e um `OnAfter*` método. Chame o `OnQuery*` método para solicitar permissão para adicionar, renomear ou remover o arquivo ou diretório. Chame o `OnAfter*` método depois que o arquivo ou diretório tiver sido adicionado, renomeado ou removido e o estado do projeto refletir o novo estado.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>
- [Suporte para controle do código-fonte](../../extensibility/internals/supporting-source-control.md)
