---
title: Espaço de trabalho de indexação no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 3163e98c-1c79-48a7-813f-7923be894ba1
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 5004db0d895d1fdc697c18606c346c24cd484527
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49939144"
---
# <a name="workspace-indexing"></a>Espaço de trabalho de indexação

Em uma solução, sistemas de projeto são responsáveis por fornecer funcionalidade para compilação, depuração e **GoTo** pesquisa de símbolo e muito mais. Sistemas de projeto podem fazer esse trabalho, pois eles entendem a relação e a recursos de arquivos dentro de um projeto. Uma [Abrir pasta](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) o mesmo insight para fornecer recursos avançados do IDE também precisa de espaço de trabalho. A coleta e o armazenamento persistente de dados é um processo chamado de espaço de trabalho de indexação. Esses dados indexados podem ser consultados por meio de um conjunto de APIs assíncronas. Extensores podem participar do processo de indexação fornecendo <xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScanner>s que sabe como lidar com certos tipos de arquivos.

## <a name="types-of-indexed-data"></a>Tipos de dados indexados

Há três tipos de dados que são indexados. Observe o tipo esperado de scanners de arquivo é diferente do tipo desserializado do índice.

|Dados|Tipo de scanner de arquivo|Tipo de resultado de consulta de índice|Tipos relacionados|
|--|--|--|--|
|Referências|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfo>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfoType>|
|Símbolos|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinition>|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinitionSearchResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.ISymbolService> deve ser usado em vez de `IIndexWorkspaceService` para consultas|
|Valores de dados|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataValue>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataResult`1>||

## <a name="querying-for-indexed-data"></a>Consultando dados indexados

Há dois tipos de assíncronos disponíveis para acessar os dados persistentes. A primeira é por meio de <xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceData>. Ele fornece acesso básico para um único arquivo `FileReferenceResult` e `FileDataResult` dados e armazena em cache os resultados. O segundo é o <xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceService> que não usa o armazenamento em cache, mas permite mais funcionalidades de consulta.

```csharp
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Indexing;

private static IIndexWorkspaceData GetCachedIndexedData(IWorkspace workspace)
{
    // Gets access to indexed data wrapped in a cache.
    return workspace?.GetIndexWorkspaceDataService()?.CreateIndexWorkspaceData();
}

private static IIndexWorkspaceService GetDirectIndexedData(IWorkspace workspace)
{
    // Gets direct access to indexed data.
    // Can also be casted to IIndexWorkspaceService2.
    return workspace?.GetIndexWorkspaceService();
}
```

## <a name="participating-in-indexing"></a>Participando de indexação

Aproximadamente a indexação de espaço de trabalho segue a sequência a seguir:

1. A descoberta e persistência de entidades do sistema de arquivos no espaço de trabalho (somente na verificação inicial de abertura).
1. Por arquivo, o provedor de correspondência com a prioridade mais alta é solicitado a verificar `FileReferenceInfo`s.
1. Por arquivo, o provedor de correspondência com a prioridade mais alta é solicitado a verificar `SymbolDefinition`s.
1. Por arquivo, todos os provedores são solicitados para `FileDataValue`s.

Extensões podem exportar um scanner implementando `IWorkspaceProviderFactory<IFileScanner>` e exportar o tipo com <xref:Microsoft.VisualStudio.Workspace.Indexing.ExportFileScannerAttribute>. O `SupportedTypes` argumento de atributo deve ser um ou mais valores de <xref:Microsoft.VisualStudio.Workspace.Indexing.FileScannerTypeConstants>. Para um scanner de exemplo, consulte o SDK do VS [exemplo](https://github.com/Microsoft/VSSDK-Extensibility-Samples/blob/master/Open_Folder_Extensibility/C%23/SymbolScannerSample/TxtFileSymbolScanner.cs).

> [!WARNING]
> Não exporte um verificador de arquivo que dá suporte a `FileScannerTypeConstants.FileScannerContentType` tipo. Ele é usado para fins internos de Microsoft, apenas.

Em situações avançadas, uma extensão dinamicamente pode oferecer suporte um conjunto arbitrário de tipos de arquivo. Em vez de exportação de MEF `IWorkspaceProviderFactory<IFileScanner>`, uma extensão pode exportar `IWorkspaceProviderFactory<IFileScannerProvider>`. Quando a indexação é iniciada, esse tipo de fábrica será importado, instanciado e ter seu <xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScannerProvider.GetSymbolScannersAsync%2A> método invocado. `IFileScanner` instâncias que dão suporte a qualquer valor de `FileScannerTpeConstants` será respeitada, não apenas símbolos.

## <a name="next-steps"></a>Próximas etapas

* [Espaços de trabalho e serviços de linguagem](workspace-language-services.md) -Saiba como integrar serviços de linguagem em um espaço de trabalho de abrir pasta.
* [Compilação de espaço de trabalho](workspace-build.md) -Abrir pasta suporta cria sistemas como o MSBuild e makefiles.