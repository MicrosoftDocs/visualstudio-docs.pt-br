---
title: Tabela de documento em execução | Microsoft Docs
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
- read locks
- running document table (RDT), IVsDocumentLockHolder interface
- running document table (RDT)
- running document table (RDT), edit locks
- document data objects, running document table
ms.assetid: bbec74f3-dd8e-48ad-99c1-2df503c15f5a
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: bd7b8cd44c72ea058f71575bdd1774efafa86731
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51746295"
---
# <a name="running-document-table"></a>Tabela de documento em execução
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O IDE mantém a lista de todos os documentos abertos no momento em uma estrutura interna chamada tabela de documento em execução (RDT). Essa lista inclui todos os documentos abertos na memória, independentemente de se esses documentos estão sendo editados. Um documento é qualquer item que é persistida, incluindo arquivos em um projeto ou arquivo de projeto principal (por exemplo, um arquivo. vcxproj).  
  
## <a name="elements-of-the-running-document-table"></a>Elementos da tabela documento em execução  
 A tabela de documento em execução contém as entradas a seguir.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Moniker do documento|Uma cadeia de caracteres que identifica exclusivamente o objeto de dados do documento. Isso seria o caminho de arquivo absoluto para um sistema de projeto que gerencia os arquivos (por exemplo, C:\MyProject\MyFile). Essa cadeia de caracteres também é usada para projetos salvos em armazenamentos diferentes sistemas de arquivos, como procedimentos armazenados em um banco de dados. Nesse caso, o sistema de projeto pode ser inventado uma cadeia de caracteres exclusiva que ele possa reconhecer e, possivelmente, analisá-lo para determinar como armazenar o documento.|  
|Proprietário da hierarquia|O objeto de hierarquia que possui o documento, conforme representado por um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface.|  
|ID do item|Identificador do item para um item específico dentro da hierarquia. Esse valor é exclusivo entre todos os documentos na hierarquia que possui esse documento, mas esse valor não é garantido para ser exclusivo entre hierarquias diferentes.|  
|Objeto de dados de documento|No mínimo, esse é um `IUnknown`<br /><br /> . O IDE não requer nenhuma interface específica, além de `IUnknown` interface para o objeto de dados de documento de um editor personalizado. No entanto, para um editor padrão, a implementação do editor do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> interface é necessária para lidar com chamadas de persistência de arquivo do projeto. Para obter mais informações, consulte [salvando um documento padrão](../../extensibility/internals/saving-a-standard-document.md).|  
|Sinalizadores|Sinalizadores que controlam se o documento é salvo, se um bloqueio de leitura ou edição é aplicado e assim por diante, podem ser especificados quando são adicionadas entradas para o RDT. Para obter mais informações, consulte a enumeração <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>.|  
|Editar contagem de bloqueio|Contagem de bloqueios de edição. Um bloqueio de edição indica que algum editor tem o documento aberto para edição. Quando a contagem de bloqueios de edição faz a transição para zero, o usuário é solicitado a salvar o documento, se ele tiver sido modificado. Por exemplo, sempre que você abrir um documento em um editor usando o **nova janela** de comando, um bloqueio de edição é adicionado para o documento no RDT. Em ordem para um bloqueio de edição a ser definido, o documento deve ter uma hierarquia ou ID de item|  
|Contagem de bloqueio de leitura|Contagem de bloqueios de leitura. Um bloqueio de leitura indica que o documento está sendo lido por algum outro mecanismo, como um assistente. Um bloqueio de leitura contém um documento ativo no RDT ao mesmo tempo que indica que o documento não pode ser editado. Você pode definir um bloqueio de leitura, mesmo se o documento não tem uma hierarquia ou ID de item Esse recurso permite que você abrir um documento na memória e insira-o a RDT sem o documento sendo pertencente a qualquer hierarquia. Esse recurso é raramente usado.|  
|Proprietário do bloqueio|Uma instância de um <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface. O proprietário do bloqueio é implementado por recursos, como assistentes que abrir e editar documentos fora de um editor. Um proprietário de bloqueio permite que o recurso Adicionar um bloqueio de editar o documento para impedir que o documento que está sendo fechado enquanto ele ainda está sendo editado. Normalmente, edite os bloqueios são adicionados apenas por janelas de documento (ou seja, editores).|  
  
 Cada entrada no RDT tem uma hierarquia exclusiva ou a ID do item associado a ele, que geralmente corresponde a um nó do projeto. Todos os documentos disponíveis para edição normalmente pertencentes a uma hierarquia. As entradas feitas na RDT controlam qual projeto, ou — com mais precisão — a hierarquia, que atualmente possui o objeto de dados de documento que está sendo editado. Usando as informações a RDT, o IDE pode impedir que um documento que está sendo aberto por mais de um projeto por vez.  
  
 A hierarquia também controla a persistência de dados e usa as informações a RDT para atualizar o **salve** e **Salvar como** caixas de diálogo. Quando os usuários modificar um documento e, em seguida, escolha o **Exit** comando da **arquivo** menu, o IDE avisará-los com o **salvar alterações** caixa de diálogo para mostrar todos os projetos e itens de projeto que são modificados no momento. Isso permite que os usuários escolham quais dos documentos para salvar. A lista de documentos para salvar (ou seja, aqueles documentos que têm alterações) é gerado a partir de RDT. Todos os itens que você espera ver na **salvar alterações** caixa de diálogo após o fechamento do aplicativo deve ter registros no RDT. O RDT coordena quais documentos são salvos e se o usuário é avisado sobre um salvamento operação usando os valores especificados na entrada de sinalizadores para cada documento. Para obter mais informações sobre os sinalizadores RDT, consulte o <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> enumeração.  
  
## <a name="edit-locks-and-read-locks"></a>Bloqueios de edição e bloqueios de leitura  
 Bloqueios de edição e bloqueios de leitura residem no RDT. Os incrementos de janela de documento e diminui a edição de bloqueio. Assim, quando um usuário abre uma nova janela de documento, os incrementos de contagem de bloqueio de edição por um. Quando o número de bloqueios de edição chega a zero, a hierarquia é sinalizada para persistir ou salvar os dados para o documento associado. A hierarquia pode persistir os dados de qualquer forma, incluindo como um arquivo ou como um item em um repositório de persistência. Você pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A> método na <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> interface Adicionar bloqueios de edição e ler bloqueios e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> método para remover esses bloqueios.  
  
 Normalmente, quando a janela de documento para um editor é instanciada, o quadro de janela adiciona automaticamente um bloqueio de edição para o documento no RDT. No entanto, se você criar uma exibição personalizada de um documento que não usa uma janela de documento padrão (ou seja, ele não implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> interface), em seguida, você precisa definir seu próprio bloqueio de edição. Por exemplo, um assistente, um documento é editado sem ser aberto em um editor. Para os bloqueios de documento a ser aberto por assistentes e entidades semelhantes, essas entidades devem implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface. Para registrar seu proprietário do bloqueio de documento, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> método e passar seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> implementação. Isso adiciona seu proprietário do bloqueio de documento para o RDT. Outro cenário para a implementação de um proprietário de bloqueio de documento é se você abrir um documento por meio de uma janela de ferramentas especial. Nesse caso, você não conseguir têm a janela da ferramenta de fechar o documento. No entanto, ao se registrar como um proprietário de bloqueio de documento no RDT, o IDE pode chamar sua implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A> método para solicitar um fechamento do documento.  
  
## <a name="other-uses-of-the-running-document-table"></a>Outros usos da tabela documento em execução  
 Outras entidades no IDE usam o RDT para obter informações sobre documentos. Por exemplo, o Gerenciador de controle de origem usa a RDT para informar ao sistema para recarregar um documento no editor, depois que ele obtém a versão mais recente do arquivo. Para fazer isso, o Gerenciador de controle do código-fonte procura os arquivos a RDT para ver se algum deles estiver aberto. Se eles são, então, o Gerenciador de controle de origem primeiro verifica para ver que a hierarquia implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> método. Se o projeto não implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> manager procura uma implementação de controlar o método e, em seguida, o código-fonte a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> método no objeto de dados de documento diretamente.  
  
 O IDE também usa o RDT para repavimentar (Trazer para frente) um documento aberto, se um usuário solicita esse documento. Para obter mais informações, consulte [exibindo arquivos usando o comando Abrir do arquivo](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md). Para determinar se um arquivo é aberto no RDT, siga um procedimentos.  
  
-   Consulta para o moniker do documento (ou seja, o caminho completo do documento) descobrir se o item for aberto.  
  
-   Use a ID de hierarquia ou um item para pedir que o sistema de projeto para o caminho completo do documento e, em seguida, examinar o item de a RDT.  
  
## <a name="see-also"></a>Consulte também  
 [Uso de RDT_ReadLock](../../extensibility/internals/rdt-readlock-usage.md)   
 [Persistência e tabela de documento em execução](../../extensibility/internals/persistence-and-the-running-document-table.md)

