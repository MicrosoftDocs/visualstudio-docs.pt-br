---
title: Editar consulta (VSPackage de controle do código-fonte) de salvamento de consulta | Microsoft Docs
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
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 170056db4269b8dd69f241093c467243b75131b7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51763249"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>Editar e salvar consulta (VSPackage de controle do código-fonte)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] editores podem transmitir eventos de consulta Editar consulta salvar (QEQS). [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Stub de controle de origem implementa o serviço QEQS, para que ele seja o destinatário de eventos do QEQS. Esses eventos, em seguida, são delegados VSPackage de controle de origem ativa no momento. O controle de origem ativa VSPackage implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> e seus métodos. Os métodos do `IVsQueryEditQuerySave2` interface normalmente são chamados imediatamente antes de um documento é editado pela primeira vez e imediatamente antes de um documento é salvo.  
  
## <a name="queryeditquerysave-events"></a>Eventos de QueryEditQuerySave  
 O VSPackage de controle de fonte deve tratar os eventos QEQS Implementando o `IVsQueryEditQuerySave2` interface e os métodos necessários. Abaixo está uma breve descrição dos dois métodos que o VSPackage deve implementar no mínimo. A implementação real deve estar em conformidade com a lógica do modelo de controle de origem.  
  
### <a name="queryeditfiles-method"></a>Método QueryEditFiles  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> é chamado quando qualquer editor ou projeto quer modificar um arquivo. Idealmente, esse método é chamado *antes de* o arquivo é modificado e quando um arquivo é salvo. Quando invocado, o `IVsQueryEditQuerySave2::QueryEditFiles` método verifica se os arquivos de determinado estão sob controle do código-fonte, necessidade de fazer check-out e se eles podem ser recarregados. Se as circunstâncias impedir que os arquivos que estão sendo editável, a `IVsQueryEditQuerySave2::QueryEditFiles` método informa o programa de chamada para cancelar a edição. Também é possível que o chamador especifique um modo de chamada. No modo "silencioso", esse método usa a ação somente se ele não faz com que qualquer interface do usuário seja exibido. Se a interface do usuário é inevitável, um sinalizador deve ser retornado para indicar o problema.  
  
 O método se comporta de maneira transacional; ou seja, se a edição seja cancelada em um único arquivo, a edição foi cancelada para todos os arquivos. Por outro lado, se a edição é permitida, é permitido para todos os arquivos. Se esse método permite a edição de uma vez para um determinado conjunto de arquivos, ele sempre deve permitir a edição em chamadas subsequentes para o mesmo conjunto de arquivos. Permitir edição loop continuará até que os arquivos são fechados, salvo e recarregados. até que alteram seus atributos (Propriedades); ou, até que o pacote de controle de origem é alterado. Casos a serem considerados na implementação de `IVsQueryEditQuerySave2::QueryEditFiles` incluir vários arquivos, arquivos especiais de método, cancelar de usuário e edições de memória.  
  
### <a name="querysavefiles-method"></a>Método QuerySaveFiles  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> é chamado quando qualquer editor ou projeto precisa salvar um conjunto de arquivos. Quando invocado, o `IVsQueryEditQuerySave2::QuerySaveFiles` método verifica se os arquivos de determinado são somente leitura e que estão sob controle do código-fonte. Se os arquivos precisam fazer check-out, a chamada é delegada para o pacote de controle de origem. Se as circunstâncias impedir que os arquivos sejam salvos, o `IVsQueryEditQuerySave2::QuerySaveFiles` método deve informar o editor para cancelar a gravação. Assim como acontece com o `IVsQueryEditQuerySave2::QueryEditFiles` método, é possível que o chamador especifique um modo de chamada. No modo "silencioso", esse método usa a ação somente se ele não faz com que qualquer interface do usuário seja exibido. Se a interface do usuário é inevitável, um sinalizador deve ser retornado para indicar o problema.  
  
 Esse método deve se comportar de maneira transacional; ou seja, se o salvamento for cancelado em um único arquivo, salvar foi cancelada para todos os arquivos. Por outro lado, se o salvamento for permitido, ele deve ter permissão para todos os arquivos. Assim como acontece com o `IVsQueryEditQuerySave2::QueryEditFiles` casos a serem considerados na implementação de um método, o `IVsQueryEditQuerySave2::QuerySaveFiles` incluir vários arquivos, arquivos especiais de método, cancelar de usuário e edições de memória.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>

