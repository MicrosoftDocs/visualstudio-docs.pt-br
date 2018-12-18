---
title: Tabela de documento em execução | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- read locks
- running document table (RDT), IVsDocumentLockHolder interface
- running document table (RDT)
- running document table (RDT), edit locks
- document data objects, running document table
ms.assetid: bbec74f3-dd8e-48ad-99c1-2df503c15f5a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4a49a5267fcccbde60e194e3fc58b0f6b6ea7552
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31134083"
---
# <a name="running-document-table"></a>Tabela de documento em execução
O IDE mantém a lista de todos os documentos abertos em uma estrutura interna chamada tabela de documento em execução (RDT). Essa lista inclui todos os documentos abertos na memória, independentemente de se esses documentos estão sendo editados atualmente. Um documento é qualquer item que é mantido, incluindo arquivos em um projeto ou o arquivo de projeto principal (por exemplo, um arquivo. vcxproj).  
  
## <a name="elements-of-the-running-document-table"></a>Elementos da tabela documento em execução  
 A tabela de documento em execução contém as entradas a seguir.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Moniker do documento|Uma cadeia de caracteres que identifica exclusivamente o objeto de dados de documento. Isso pode ser o caminho de arquivo absoluto para um sistema de projeto que gerencia arquivos (por exemplo, C:\MyProject\MyFile). Essa cadeia de caracteres também é usada para projetos salvos em repositórios diferentes sistemas de arquivos, como procedimentos armazenados em um banco de dados. Nesse caso, o sistema do projeto pode criar uma cadeia de caracteres exclusiva que ele possa reconhecer e possivelmente analisar para determinar como armazenar o documento.|  
|Proprietário da hierarquia|O objeto de hierarquia que possui o documento, conforme representado por um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface.|  
|ID do item|Identificador do item para um item específico dentro da hierarquia. Esse valor é exclusivo entre todos os documentos na hierarquia que possui este documento, mas esse valor não é garantido como sendo exclusivo em hierarquias diferentes.|  
|Objeto de dados de documento|No mínimo, este é um `IUnknown`<br /><br /> . O IDE não requer qualquer interface específica, além de `IUnknown` interface para o objeto de dados de documento de um editor personalizado. No entanto, para um editor padrão, a implementação do editor do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> interface é necessária para lidar com chamadas de persistência do arquivo do projeto. Para obter mais informações, consulte [salvar um documento padrão](../../extensibility/internals/saving-a-standard-document.md).|  
|Sinalizadores|Sinalizadores que controlam se o documento é salvo, se um bloqueio de leitura ou editar é aplicado e assim por diante, podem ser especificados quando as entradas são adicionadas para o RDT. Para obter mais informações, consulte a enumeração <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>.|  
|Editar o número de bloqueios|Contagem de bloqueios de edição. Um bloqueio de edição indica que algum editor tem o documento aberto para edição. Quando a contagem de bloqueios de edição faz a transição para zero, o usuário é solicitado a salvar o documento, se ele tiver sido modificado. Por exemplo, sempre que você abrir um documento em um editor usando o **nova janela** de comando, um bloqueio de edição é adicionado para o documento no RDT. Para um bloqueio de edição a ser definido, o documento deve ter uma hierarquia ou item ID.|  
|Contagem de bloqueio de leitura|Contagem de bloqueios de leitura. Um bloqueio de leitura indica que o documento está sendo lido por algum outro mecanismo, como um assistente. Um bloqueio de leitura contém um documento ativo no RDT ao mesmo tempo, indicando que o documento não pode ser editado. Você pode definir um bloqueio de leitura, mesmo se o documento não possui uma hierarquia ou item ID. Esse recurso permite que você abrir um documento na memória e insira o RDT sem o documento que pertença a nenhuma hierarquia. Este recurso é raramente usado.|  
|Proprietário do bloqueio|Uma instância de um <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface. O proprietário do bloqueio é implementado por recursos, como assistentes que abrir e editar documentos fora de um editor. Um proprietário de bloqueio permite que o recurso Adicionar um bloqueio de edição ao documento para impedir que o documento que está sendo fechado enquanto ele ainda está sendo editado. Normalmente, editar bloqueios só são adicionados por janelas de documento (ou seja, editores).|  
  
 Cada entrada no RDT tem uma hierarquia exclusiva ou a ID do item associado a ele, que geralmente corresponde a um nó do projeto. Todos os documentos disponíveis para edição normalmente pertencentes a uma hierarquia. As entradas feitas no RDT controlam qual projeto, ou — com mais precisão — a hierarquia, que atualmente possui o objeto de dados de documento que está sendo editado. Usando as informações de RDT, o IDE pode impedir que um documento que está sendo aberto por mais de um projeto por vez.  
  
 A hierarquia também controla a persistência de dados e usa as informações de RDT para atualizar o **salvar** e **Salvar como** caixas de diálogo. Quando os usuários modificar um documento e, em seguida, escolha o **Exit** comando o **arquivo** menu, o IDE solicita-los com o **salvar alterações** caixa de diálogo para mostrar todos os projetos e itens de projeto que são modificadas no momento. Isso permite que os usuários podem escolher qual salvar os documentos. A lista de documentos para salvar (ou seja, aqueles documentos que têm alterações) é gerada a partir de RDT. Todos os itens que você espera ver no **salvar alterações** caixa de diálogo ao sair do aplicativo deve ter registros no RDT. O RDT coordena os documentos são salvos e se o usuário é avisado sobre salvar operação usando os valores especificados na entrada de sinalizadores para cada documento. Para obter mais informações sobre os sinalizadores RDT, consulte o <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> enumeração.  
  
## <a name="edit-locks-and-read-locks"></a>Bloqueios de edição e bloqueios de leitura  
 Bloqueios de edição e bloqueios de leitura residem no RDT. Os incrementos de janela de documento e diminui a edição de bloqueio. Portanto, quando um usuário abre uma nova janela de documento, os incrementos de contagem de bloqueio de editar por um. Quando o número de bloqueios de edição chega a zero, a hierarquia é sinalizada para persistir ou salvar os dados para o documento associado. A hierarquia pode, em seguida, persistir os dados de qualquer forma, incluindo como um arquivo ou um item em um repositório de persistência. Você pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A> método o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> interface para adicionar os bloqueios de edição e bloqueios de leitura e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> método para remover esses bloqueios.  
  
 Normalmente, quando a janela de documento para um editor é instanciada, o quadro de janela automaticamente adiciona um bloqueio de edição para o documento de RDT. No entanto, se você criar uma exibição personalizada de um documento que não usam uma janela de documento padrão (ou seja, ele não implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> interface), em seguida, você precisará definir seu próprio bloqueio de edição. Por exemplo, um assistente, um documento é editado sem que está sendo aberto em um editor. Ordem de bloqueios de documento a ser aberto por assistentes e semelhante de entidades, essas entidades devem implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface. Para registrar seu proprietário de bloqueio de documento, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> método e passar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> implementação. Isso adiciona o proprietário do bloqueio de documento para o RDT. Outro cenário para a implementação de um proprietário de bloqueio de documento é se você abrir um documento por meio de uma janela de ferramentas especial. Nesse caso, não será possível para que a janela da ferramenta fechar o documento. No entanto, registrando-se como um proprietário de bloqueio de documento no RDT, o IDE pode chamar a implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A> método para solicitar um fechamento do documento.  
  
## <a name="other-uses-of-the-running-document-table"></a>Outros usos da tabela documento em execução  
 Outras entidades no IDE usam o RDT para obter informações sobre documentos. Por exemplo, o Gerenciador de controle de origem usa a RDT informar ao sistema para recarregar um documento no editor, depois que ele obtém a versão mais recente do arquivo. Para fazer isso, o Gerenciador de controle de origem procura os arquivos em RDT para ver se algum deles estão abertas. Se forem, o Gerenciador de controle de origem primeiro verifica se a hierarquia implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> método. Se o projeto não implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> manager procura uma implementação de controla o método e, em seguida, a fonte do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> método no objeto de dados de documento diretamente.  
  
 O IDE também usa o RDT para repavimentar (Trazer para frente) um documento aberto, se um usuário solicitar esse documento. Para obter mais informações, consulte [exibindo arquivos usando o comando Abrir do arquivo](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md). Para determinar se um arquivo é aberto no RDT, siga um procedimentos.  
  
-   Consulta para o moniker do documento (ou seja, o caminho completo do documento) descobrir se o item estiver aberto.  
  
-   Use a ID de hierarquia ou um item para solicitar o sistema de projeto para o caminho de documento completo e, em seguida, examinar o item para cima o RDT.  
  
## <a name="see-also"></a>Consulte também  
 [Uso de RDT_ReadLock](../../extensibility/internals/rdt-readlock-usage.md)   
 [Persistência e tabela de documento em execução](../../extensibility/internals/persistence-and-the-running-document-table.md)