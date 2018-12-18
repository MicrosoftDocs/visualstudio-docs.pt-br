---
title: Editar consulta salvar (VSPackage de controle de origem) de consulta | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bf4fd74544e0646a84e4fdc37f35ba84b301f693
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131511"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>Editar consulta salvar (VSPackage de controle de origem)
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] editores podem transmitir eventos de consulta Editar consulta salvar (QEQS). [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Stub de controle do código-fonte implementa o serviço QEQS, para que ele é o destinatário de eventos do QEQS. Esses eventos são, em seguida, delegados para o controle de origem ativa atualmente VSPackage. O controle de origem ativa VSPackage implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> e seus métodos. Os métodos do `IVsQueryEditQuerySave2` interface normalmente são chamadas imediatamente antes de um documento é editado pela primeira vez e imediatamente antes de um documento é salvo.  
  
## <a name="queryeditquerysave-events"></a>Eventos de QueryEditQuerySave  
 O controle de origem VSPackage deve tratar os eventos QEQS Implementando o `IVsQueryEditQuerySave2` interface e os métodos necessários. Abaixo está uma breve descrição dos dois métodos que o VSPackage deve implementar no mínimo. A implementação real deve estar em conformidade com a lógica do modelo de controle de origem.  
  
### <a name="queryeditfiles-method"></a>Método QueryEditFiles  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> é chamado quando qualquer editor ou projeto deseja modificar um arquivo. Idealmente, esse método é chamado *antes de* o arquivo é modificado, e quando um arquivo é salvo. Quando chamado, o `IVsQueryEditQuerySave2::QueryEditFiles` método verifica se os arquivos de determinado estão sob o controle de origem, se eles precisam fazer check-out e se pode ser recarregados. Se circunstâncias impedir que os arquivos que está sendo editado, a `IVsQueryEditQuerySave2::QueryEditFiles` método informa o programa de chamada para cancelar a edição. Também é possível que o chamador pode especificar um modo de chamada. No modo "silencioso", este método usa a ação somente se não causa nenhuma interface do usuário seja exibido. Se a interface do usuário é inevitável, um sinalizador deve ser retornado para indicar o problema.  
  
 O método se comporta de forma transacional; ou seja, se a edição for cancelada em um único arquivo, a edição é cancelada para todos os arquivos. Por outro lado, se a edição é permitida, é permitido para todos os arquivos. Se esse método permite a edição de uma vez para um determinado conjunto de arquivos, ele sempre deve permitir a edição em chamadas subsequentes para o mesmo conjunto de arquivos. Permitir a edição loop continua até que os arquivos são fechados, salvo e recarregados. até que alteram seus atributos (Propriedades); ou, até que o pacote de controle de origem é alterado. Casos a serem considerados na implementação de `IVsQueryEditQuerySave2::QueryEditFiles` método incluir vários arquivos, arquivos especiais, cancele do usuário e edições de memória.  
  
### <a name="querysavefiles-method"></a>Método QuerySaveFiles  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> é chamado quando qualquer editor ou projeto precisa salvar um conjunto de arquivos. Quando chamado, o `IVsQueryEditQuerySave2::QuerySaveFiles` método verifica se os arquivos de determinado são somente leitura e se eles estão sob o controle de origem. Se os arquivos precisam fazer check-out, a chamada é delegada ao pacote de controle de origem. Se circunstâncias impedir que os arquivos sejam salvos, o `IVsQueryEditQuerySave2::QuerySaveFiles` método deve informar o editor para cancelar a gravação. Assim como acontece com o `IVsQueryEditQuerySave2::QueryEditFiles` método, é possível que o chamador pode especificar um modo de chamada. No modo "silencioso", este método usa a ação somente se não causa nenhuma interface do usuário seja exibido. Se a interface do usuário é inevitável, um sinalizador deve ser retornado para indicar o problema.  
  
 Esse método se comportam de forma transacional; ou seja, se o salvamento for cancelado em um único arquivo, salvar foi cancelada para todos os arquivos. Por outro lado, se é permitido salvar, ele deve ter permissão para todos os arquivos. Assim como acontece com o `IVsQueryEditQuerySave2::QueryEditFiles` método, casos a serem considerados na implementação de `IVsQueryEditQuerySave2::QuerySaveFiles` método incluir vários arquivos, arquivos especiais, cancele do usuário e edições de memória.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>