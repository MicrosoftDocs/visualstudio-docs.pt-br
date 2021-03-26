---
title: Executando tabela de documentos | Microsoft Docs
description: Saiba como o IDE do Visual Studio mantém a tabela de documentos em execução, que inclui todos os documentos abertos na memória.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- read locks
- running document table (RDT), IVsDocumentLockHolder interface
- running document table (RDT)
- running document table (RDT), edit locks
- document data objects, running document table
ms.assetid: bbec74f3-dd8e-48ad-99c1-2df503c15f5a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 615910684fd79d3cbd8d8a1e012c239e27abc180
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080964"
---
# <a name="running-document-table"></a>Tabela de documento em execução
O IDE mantém a lista de todos os documentos abertos no momento em uma estrutura interna chamada RDT (tabela de documentos em execução). Essa lista inclui todos os documentos abertos na memória, independentemente se esses documentos estão sendo editados no momento. Um documento é qualquer item persistido, incluindo arquivos em um projeto ou no arquivo de projeto principal (por exemplo, um arquivo. vcxproj).

## <a name="elements-of-the-running-document-table"></a>Elementos da tabela de documentos em execução
 A tabela documento em execução contém as entradas a seguir.

|Elemento|Descrição|
|-------------|-----------------|
|Moniker do documento|Uma cadeia de caracteres que identifica exclusivamente o objeto de dados do documento. Esse seria o caminho de arquivo absoluto para um sistema de projeto que gerencia arquivos (por exemplo, C:\MyProject\MyFile). Essa cadeia de caracteres também é usada para projetos salvos em repositórios diferentes de sistemas de arquivos, como procedimentos armazenados em um banco de dados. Nesse caso, o sistema de projeto pode inventar uma cadeia de caracteres exclusiva que pode ser reconhecida e possivelmente analisada para determinar como armazenar o documento.|
|Proprietário da hierarquia|O objeto de hierarquia que possui o documento, conforme representado por uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface.|
|ID do item|Identificador de item para um item específico dentro da hierarquia. Esse valor é exclusivo entre todos os documentos na hierarquia que possui este documento, mas esse valor não tem garantia de ser exclusivo entre hierarquias diferentes.|
|Objeto de dados do documento|No mínimo, trata-se de um `IUnknown`<br /><br /> . O IDE não requer nenhuma interface específica além da `IUnknown` interface para um objeto de dados de documento do editor personalizado. No entanto, para um editor padrão, a implementação do editor da <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> interface é necessária para manipular chamadas de persistência de arquivo do projeto. Para obter mais informações, consulte [salvando um documento padrão](../../extensibility/internals/saving-a-standard-document.md).|
|Flags|Sinalizadores que controlam se o documento é salvo, se um bloqueio de leitura ou de edição é aplicado e assim por diante, pode ser especificado quando as entradas são adicionadas ao RDT. Para obter mais informações, consulte a enumeração <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>.|
|Editar contagem de bloqueios|Contagem de bloqueios de edição. Um bloqueio de edição indica que algum editor tem o documento aberto para edição. Quando a contagem de bloqueios de edição faz a transição para zero, o usuário é solicitado a salvar o documento, se ele tiver sido modificado. Por exemplo, toda vez que você abre um documento em um editor usando o comando **nova janela** , um bloqueio de edição é adicionado ao documento no RDT. Para que um bloqueio de edição seja definido, o documento deve ter uma hierarquia ou ID de item.|
|Contagem de bloqueios de leitura|Contagem de bloqueios de leitura. Um bloqueio de leitura indica que o documento está sendo lido por meio de algum mecanismo, como um assistente. Um bloqueio de leitura mantém um documento ativo no RDT enquanto indica que o documento não pode ser editado. Você pode definir um bloqueio de leitura mesmo que o documento não tenha uma ID de item ou de hierarquia. Esse recurso permite abrir um documento na memória e inseri-lo no RDT sem que o documento seja de propriedade de qualquer hierarquia. Esse recurso é raramente usado.|
|Proprietário do bloqueio|Uma instância de uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface. O proprietário do bloqueio é implementado por recursos como assistentes que abrem e editam documentos fora de um editor. Um proprietário de bloqueio permite que o recurso adicione um bloqueio de edição ao documento para impedir que o documento seja fechado enquanto ainda está sendo editado. Normalmente, os bloqueios de edição são adicionados apenas por janelas de documentos (ou seja, editores).|

 Cada entrada no RDT tem uma hierarquia exclusiva ou ID de item associada a ela, que geralmente corresponde a um nó no projeto. Todos os documentos disponíveis para edição normalmente são de propriedade de uma hierarquia. As entradas feitas no RDT controlam qual projeto, ou — mais precisamente — qual hierarquia, atualmente é proprietária do objeto de dados de documento que está sendo editado. Usando as informações no RDT, o IDE pode impedir que um documento seja aberto por mais de um projeto por vez.

 A hierarquia também controla a persistência de dados e usa as informações no RDT para atualizar as caixas de diálogo **salvar** e **salvar como** . Quando os usuários modificam um documento e escolhem o comando **sair** no menu **arquivo** , o IDE os solicita com a caixa de diálogo **salvar alterações** para mostrar todos os projetos e itens de projeto que estão atualmente modificados. Isso permite que os usuários escolham quais documentos salvar. A lista de documentos a serem salvos (ou seja, os documentos que têm alterações) é gerada por meio do RDT. Todos os itens que você espera ver na caixa de diálogo **salvar alterações** após sair do aplicativo devem ter registros no RDT. O RDT coordena quais documentos são salvos e se o usuário é avisado sobre uma operação de salvamento usando os valores especificados na entrada de sinalizadores para cada documento. Para obter mais informações sobre os sinalizadores RDT, consulte a <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> enumeração.

## <a name="edit-locks-and-read-locks"></a>Editar bloqueios e ler bloqueios
 Editar bloqueios e bloqueios de leitura residem no RDT. A janela do documento incrementa e decrementa o bloqueio de edição. Assim, quando um usuário abre uma nova janela de documento, a contagem de bloqueios de edição é incrementada em um. Quando o número de bloqueios de edição chega a zero, a hierarquia é sinalizada para persistir ou salvar os dados do documento associado. A hierarquia pode persistir os dados de qualquer forma, incluindo a persistência como um arquivo ou como um item em um repositório. Você pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A> método na <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> interface para adicionar bloqueios de edição e de leitura e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> método para remover esses bloqueios.

 Normalmente, quando a janela do documento de um editor é instanciada, o quadro da janela adiciona automaticamente um bloqueio de edição para o documento no RDT. No entanto, se você criar uma exibição personalizada de um documento que não usa uma janela de documento padrão (ou seja, ela não implementa a <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> interface), você precisará definir seu próprio bloqueio de edição. Por exemplo, em um assistente, um documento é editado sem ser aberto em um editor. Para que os bloqueios de documentos sejam abertos por assistentes e entidades semelhantes, essas entidades devem implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface. Para registrar o proprietário do bloqueio de documento, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> método e passe sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> implementação. Isso adiciona o proprietário do bloqueio de documento ao RDT. Outro cenário para implementar um detentor de bloqueio de documento é se você abrir um documento por meio de uma janela de ferramenta especial. Nessa instância, você não pode fazer com que a janela de ferramentas feche o documento. No entanto, ao se registrar como um detentor de bloqueio de documento no RDT, o IDE pode chamar sua implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A> método para solicitar um fechamento do documento.

## <a name="other-uses-of-the-running-document-table"></a>Outros usos da tabela de documentos em execução
 Outras entidades no IDE usam o RDT para obter informações sobre documentos. Por exemplo, o Gerenciador de controle do código-fonte usa o RDT para instruir o sistema a recarregar um documento no editor, depois de obter a versão mais recente do arquivo. Para fazer isso, o Gerenciador de controle do código-fonte pesquisa os arquivos no RDT para ver se algum deles está aberto. Se estiverem, o Gerenciador de controle do código-fonte primeiro verificará se a hierarquia implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> método. Se o projeto não implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> método, o Gerenciador de controle do código-fonte verificará se há uma implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> método diretamente no objeto de dados do documento.

 O IDE também usa o RDT para resuperfície (trazer para a frente) um documento aberto, se um usuário solicitar esse documento. Para obter mais informações, consulte [exibindo arquivos usando o comando abrir arquivo](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md). Para determinar se um arquivo está aberto no RDT, siga um destes procedimentos.

- Consulte o moniker do documento (ou seja, o caminho completo do documento) para descobrir se o item está aberto.

- Use a hierarquia ou a ID do item para pedir ao sistema do projeto o caminho completo do documento e, em seguida, procure o item no RDT.

## <a name="see-also"></a>Confira também
- [Uso de RDT_ReadLock](../../extensibility/internals/rdt-readlock-usage.md)
- [Persistência e a tabela de documentos em execução](../../extensibility/internals/persistence-and-the-running-document-table.md)
