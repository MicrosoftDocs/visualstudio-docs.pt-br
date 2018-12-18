---
title: Contextos de arquivo de espaço de trabalho no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 7aaa0e65-f492-49ea-a845-35bd14910ca7
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: cdb013bb10c72041b03fce43e115806ecb3faeac
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31146345"
---
# <a name="workspace-file-contexts"></a>Contextos de arquivo de espaço de trabalho

Todas as informações sobre [Abrir pasta](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) espaços de trabalho são produzidos por "arquivo provedores de contexto" que implementam o <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> interface. Essas extensões podem procurar padrões em pastas ou arquivos, ler arquivos do MSBuild e makefiles, detectarem dependências de pacote, etc. para acumular as informações que precisam para definir o contexto de um arquivo. Um contexto de arquivo por si só não executará qualquer ação, mas em vez disso, fornece dados de outra extensão pode agir em seguida.

Cada <xref:Microsoft.VisualStudio.Workspace.FileContext> tem um `Guid` associados a ele que identifica o tipo de dados ele realiza. Um espaço de trabalho usa essa `Guid` posteriormente para correspondência com extensões que consomem os dados por meio de <xref:Microsoft.VisualStudio.Workspace.FileContext.Context> propriedade. Um provedor de contexto do arquivo é exportado com metadados que identificam qual contexto de arquivo `Guid`s podem ser dados.

Depois de definido, um contexto de arquivo pode ser associado a qualquer número de arquivos ou pastas no espaço de trabalho. Um determinado arquivo ou pasta pode ser associada a qualquer número de contextos de arquivo. É uma relação muitos-para-muitos.

Os cenários mais comuns para contextos de arquivo estão relacionados a compilação, depuração e serviços de idioma. Para obter mais informações, consulte os outros tópicos relacionados a esses cenários.

## <a name="file-context-lifecycle"></a>Ciclo de vida de contexto de arquivo

Os ciclos de vida de um `FileContext` são não determinísticas. A qualquer momento, um componente de forma assíncrona pode solicitar do mesmo conjunto de tipos de contexto. Provedores que dão suporte a alguns subconjuntos dos tipos de contexto de solicitação serão consultados. O `IWorkspace` instância atua como o homem intermediária entre os consumidores e provedores por meio de <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> método. Consumidores podem solicitar um contexto e executam alguma ação de curto prazo com base no contexto, enquanto outras podem solicitar um contexto e manter uma referência a vida útil longa. 

Alterações podem ocorrer para arquivos que causam um contexto de arquivo para se tornar desatualizadas. O provedor pode acionar um evento no `FileContext` para notificar os consumidores de atualizações. Por exemplo, se um contexto de compilação é fornecido para alguns arquivos, mas uma alteração no disco invalida nesse contexto, o produtor original pode invocar o evento. Consumidores ainda fazendo referência a ela `FileContext` , em seguida, pode repetir a consulta para um novo `FileContext`.

>[!NOTE]
>Não há nenhum modelo de push para os consumidores. Os consumidores não serão notificados de um provedor novo `FileContext` após sua solicitação.

## <a name="expensive-file-context-computations"></a>Cálculos de contexto de arquivos caras

Conteúdo do arquivo de leitura de disco pode ser caro, especialmente quando um provedor precisa resolver a relação entre arquivos. Por exemplo, um provedor pode ser consultado para o contexto do arquivo de alguns arquivos de origem, mas o contexto de arquivo é dependente de metadados de um arquivo de projeto. Ao analisar o arquivo de projeto ou avaliá-lo com o MSBuild é caro. Em vez disso, a extensão pode exportar um `IFileScanner` criar `FileDataValue` dados durante a indexação de espaço de trabalho. Agora quando for solicitado para contextos de arquivo, o `IFileContextProvider` podem consultar rapidamente para que os dados indexados. Para obter mais informações sobre indexação, consulte o [espaço de trabalho de indexação](workspace-indexing.md) tópico.

>[!WARNING]
>Tenha cuidado de outras maneiras seu `FileContext` pode ser caro de computação. Algumas interações de interface do usuário são síncronas e contam com um alto volume de `FileContext` solicitações. Os exemplos incluem abrindo uma guia editor e abrindo uma **Solution Explorer** menu de contexto. Essas ações fazer contexto de compilação muitas solicitações de tipo.

## <a name="file-context-related-apis"></a>APIs relacionadas ao contexto de arquivo

- <xref:Microsoft.VisualStudio.Workspace.FileContext> mantém os dados e metadados.
- <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> e <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider`1> criar o contexto de arquivo.
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextProviderAttribute> Exporta um provedor de contexto do arquivo.
- <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> é usado para os consumidores para obter os contextos de arquivo.
- <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes> Define os tipos de contexto de compilação que consumirá Abrir pasta.

## <a name="file-context-actions"></a>Ações de contexto do arquivo

Enquanto um `FileContext` em si é apenas os dados sobre alguns arquivos, um <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> é uma maneira de express e agir sobre dados. `IFileContextAction` é flexível em seu uso. Dois dos seus casos mais comuns são criar e depurar.

## <a name="reporting-progress"></a>Relatório de progresso

O <xref:Microsoft.VisualStudio.Workspace.IFileContextActionBase.ExecuteAsync%2A> método `IProgress<IFileContextActionProgressUpdate>`, mas o argumento não deve ser usado como tipo. `IFileContextActionProgressUpdate` é uma interface vazia e chamar `IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)` poderá gerar `NotImplementedException`. Em vez disso, o `IFileContextAction` deve converter o argumento para outro tipo, conforme necessário para o cenário.

Para obter informações sobre os tipos fornecidos pelo Visual Studio, consulte a documentação do respectivo cenário.

## <a name="file-context-action-related-apis"></a>APIs relacionadas à ação de contexto do arquivo

- <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> executa algum comportamento com base em um `FileContext`.
- <xref:Microsoft.VisualStudio.Workspace.IFileContextActionProvider> cria instâncias de `IFileContextAction`.
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextActionProviderAttribute> Exporta o tipo `IWorkspaceProviderFactory<IFileContextActionProvider>`.

## <a name="file-watching"></a>Observação de arquivo

Um espaço de trabalho escuta as notificações de alteração de arquivo e fornece o <xref:Microsoft.VisualStudio.Workspace.IFileWatcherService> via <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A>. Arquivos correspondentes a configuração de "ExcludedItems" não produzirá os eventos de notificação de arquivo. Um limite entre os eventos é usado para a simplificação de notificação e redução duplicada. Quando você precisar de reagir a uma alteração de arquivo, você deve assinar este serviço.

>[!TIP]
>Um espaço de trabalho [serviço de indexação](workspace-indexing.md) assina os eventos de arquivo por padrão. Arquivo adições e modificações causará relevantes `IFileScanner`eventos s a ser invocado para novos dados para esse arquivo. Exclusões de arquivo removerá os dados indexados. Você não precisa assinar seu `IFileScanner` o serviço de Inspetor.

## <a name="next-steps"></a>Próximas etapas

* [Indexação](workspace-indexing.md) -espaço de trabalho de indexação coleta e persiste as informações sobre o espaço de trabalho.
* [Espaços de trabalho](workspaces.md) -examine os conceitos do espaço de trabalho e configurações de armazenamento.
