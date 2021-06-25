---
title: Executando a tabela de documentos | Microsoft Docs
description: Saiba como o Visual Studio IDE mantém a tabela de documentos em execução, que inclui todos os documentos abertos na memória.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: d260534d58853afc6b84ba484eb3a806250e2aa6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900402"
---
# <a name="running-document-table"></a>Tabela de documento em execução
O IDE mantém a lista de todos os documentos abertos no momento em uma estrutura interna chamada RDT (tabela de documentos em execução). Essa lista inclui todos os documentos abertos na memória, independentemente de esses documentos estarem sendo editados no momento. Um documento é qualquer item persistente, incluindo arquivos em um projeto ou no arquivo de projeto principal (por exemplo, um arquivo .vcxproj).

## <a name="elements-of-the-running-document-table"></a>Elementos da tabela de documentos em execução
 A tabela de documentos em execução contém as entradas a seguir.

|Elemento|Descrição|
|-------------|-----------------|
|Moniker de documento|Uma cadeia de caracteres que identifica exclusivamente o objeto de dados do documento. Esse seria o caminho de arquivo absoluto para um sistema de projeto que gerencia arquivos (por exemplo, C:\MyProject\MyFile). Essa cadeia de caracteres também é usada para projetos salvos em armazenamentos diferentes de sistemas de arquivos, como procedimentos armazenados em um banco de dados. Nesse caso, o sistema de projeto pode inventar uma cadeia de caracteres exclusiva que ele pode reconhecer e, possivelmente, analisar para determinar como armazenar o documento.|
|Proprietário da hierarquia|O objeto de hierarquia que possui o documento, conforme representado por uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface .|
|Item ID|Identificador de item para um item específico dentro da hierarquia. Esse valor é exclusivo entre todos os documentos na hierarquia que possui este documento, mas não há garantia de que esse valor seja exclusivo em hierarquias diferentes.|
|Objeto de dados do documento|No mínimo, este é um `IUnknown`<br /><br /> . O IDE não requer nenhuma interface específica além da interface para o objeto de dados de documento de um `IUnknown` editor personalizado. No entanto, para um editor padrão, a implementação da interface do editor é necessária para lidar com chamadas de persistência <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> de arquivo do projeto. Para obter mais informações, consulte [Salvando um documento padrão.](../../extensibility/internals/saving-a-standard-document.md)|
|Flags|Sinalizadores que controlam se o documento é salvo, se um bloqueio de leitura ou edição é aplicado e assim por diante, podem ser especificados quando as entradas são adicionadas ao RDT. Para obter mais informações, consulte a enumeração <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>.|
|Editar Contagem de Bloqueios|Contagem de bloqueios de edição. Um bloqueio de edição indica que algum editor tem o documento aberto para edição. Quando a contagem de bloqueios de edição faz a transição para zero, o usuário é solicitado a salvar o documento, se ele tiver sido modificado. Por exemplo, sempre que você abre um documento em um editor usando o comando **Nova Janela,** um bloqueio de edição é adicionado para esse documento no RDT. Para que um bloqueio de edição seja definido, o documento deve ter uma hierarquia ou uma ID de item.|
|Contagem de bloqueios de leitura|Contagem de bloqueios de leitura. Um bloqueio de leitura indica que o documento está sendo lido por meio de algum mecanismo, como um assistente. Um bloqueio de leitura mantém um documento vivo no RDT, indicando que o documento não pode ser editado. Você pode definir um bloqueio de leitura mesmo que o documento não tenha uma hierarquia ou uma ID de item. Esse recurso permite que você abra um documento na memória e insira-o no RDT sem que o documento seja de propriedade de nenhuma hierarquia. Esse recurso raramente é usado.|
|Titular de bloqueio|Uma instância de uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface. O titular do bloqueio é implementado por recursos como assistentes que abrem e editam documentos fora de um editor. Um titular de bloqueio permite que o recurso adicione um bloqueio de edição ao documento para impedir que o documento seja fechado enquanto ele ainda está sendo editado. Normalmente, os bloqueios de edição são adicionados apenas por janelas de documento (ou seja, editores).|

 Cada entrada no RDT tem uma hierarquia ou ID de item exclusiva associada a ela, que geralmente corresponde a um nó no projeto. Todos os documentos disponíveis para edição normalmente pertencem a uma hierarquia. Entradas feitas no controle RDT de qual projeto, ou , com mais precisão, qual hierarquia, atualmente possui o objeto de dados do documento que está sendo editado. Usando as informações no RDT, o IDE pode impedir que um documento seja aberto por mais de um projeto por vez.

 A hierarquia também controla a persistência de dados e usa as informações no RDT para atualizar as caixas de **diálogo** Salvar e Salvar **como.** Quando os usuários modificam  um documento e, em seguida, escolhem o  comando Sair no **menu** Arquivo, o IDE solicita a eles a caixa de diálogo Salvar Alterações para mostrar todos os projetos e itens de projeto que estão modificados no momento. Isso permite que os usuários escolham qual dos documentos salvar. A lista de documentos a salvar (ou seja, os documentos que têm alterações) é gerada do RDT. Todos os itens que você espera ver na **caixa** de diálogo Salvar Alterações ao sair do aplicativo devem ter registros no RDT. O RDT coordena quais documentos são salvos e se o usuário é solicitado sobre uma operação de salvar usando os valores especificados na entrada Sinalizadores para cada documento. Para obter mais informações sobre os sinalizadores RDT, consulte a <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> enumeração .

## <a name="edit-locks-and-read-locks"></a>Editar bloqueios e bloqueios de leitura
 Editar bloqueios e bloqueios de leitura residem no RDT. A janela do documento incrementa e diminui o bloqueio de edição. Assim, quando um usuário abre uma nova janela de documento, a contagem de bloqueios de edição é incrementada em uma. Quando o número de bloqueios de edição atinge zero, a hierarquia é sinalizada para persistir ou salvar os dados do documento associado. A hierarquia pode persistir os dados de qualquer forma, incluindo persistir como um arquivo ou como um item em um repositório. Você pode usar o método na interface para adicionar bloqueios de edição e bloqueios de leitura <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A> e o método para remover esses <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> bloqueios.

 Normalmente, quando a janela do documento para um editor é instautada, o quadro de janela adiciona automaticamente um bloqueio de edição para o documento no RDT. No entanto, se você criar uma exibição personalizada de um documento que não usa uma janela de documento padrão (ou seja, ela não implementa a interface), você precisará definir seu próprio bloqueio <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> de edição. Por exemplo, em um assistente, um documento é editado sem ser aberto em um editor. Para que os bloqueios de documentos sejam abertos por assistentes e entidades semelhantes, essas entidades devem implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface . Para registrar o titular do bloqueio do documento, chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> o método e passe sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> implementação. Isso adiciona o titular do bloqueio de documento ao RDT. Outro cenário para implementar um titular de bloqueio de documento é se você abrir um documento por meio de uma janela de ferramenta especial. Nesse caso, não é possível fazer com que a janela de ferramentas feche o documento. No entanto, ao registrar-se como um titular de bloqueio de documento no RDT, o IDE pode chamar sua implementação do método para solicitar um <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A> fechamento do documento.

## <a name="other-uses-of-the-running-document-table"></a>Outros usos da tabela de documentos em execução
 Outras entidades no IDE usam o RDT para obter informações sobre documentos. Por exemplo, o gerenciador de controle do código-fonte usa o RDT para dizer ao sistema para recarregar um documento no editor, depois de obter a versão mais recente do arquivo. Para fazer isso, o gerenciador de controle do código-fonte pesquisa os arquivos no RDT para ver se algum deles está aberto. Se eles são, o gerenciador de controle do código-fonte primeiro verifica se a hierarquia implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> método . Se o projeto não implementar o método , o gerenciador de controle do código-fonte verificará uma implementação do método no <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> objeto de dados do documento <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> diretamente.

 O IDE também usa o RDT para ressurgir (trazer para a frente) um documento aberto, se um usuário solicitar esse documento. Para obter mais informações, [consulte Exibindo arquivos usando o comando Abrir Arquivo](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md). Para determinar se um arquivo está aberto no RDT, faça o seguinte.

- Consulte o moniker do documento (ou seja, o caminho completo do documento) para descobrir se o item está aberto.

- Use a hierarquia ou a ID do item para solicitar ao sistema de projeto o caminho completo do documento e, em seguida, procure o item no RDT.

## <a name="see-also"></a>Confira também
- [Uso de RDT_ReadLock](../../extensibility/internals/rdt-readlock-usage.md)
- [Persistência e a tabela de documentos em execução](../../extensibility/internals/persistence-and-the-running-document-table.md)
