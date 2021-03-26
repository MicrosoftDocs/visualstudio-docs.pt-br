---
title: Consulta editar consulta salvar (controle do código-fonte VSPackage) | Microsoft Docs
description: Saiba mais sobre a função de eventos de Query-Edit Query-Save e como eles são manipulados pelo VSPackage de controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9295644a07a1840cd4874b8bfff298ad9d46c928
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060907"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>Editar e salvar consulta (VSPackage de controle do código-fonte)
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] os editores podem difundir eventos de salvamento de consulta de edição de consulta (QEQS). [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] O stub de controle do código-fonte implementa o serviço QEQS, para que ele seja o destinatário de eventos de QEQS. Esses eventos são então delegados para o VSPackage de controle do código-fonte ativo no momento. O controle do código-fonte ativo VSPackage implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> e seus métodos. Os métodos da `IVsQueryEditQuerySave2` interface são normalmente chamados imediatamente antes de um documento ser editado pela primeira vez e imediatamente antes de um documento ser salvo.

## <a name="queryeditquerysave-events"></a>Eventos de QueryEditQuerySave
 O VSPackage de controle do código-fonte deve manipular os eventos QEQS implementando a `IVsQueryEditQuerySave2` interface e os métodos necessários. Veja abaixo uma breve descrição dos dois métodos que o VSPackage deve implementar no mínimo. A implementação real deve estar de acordo com a lógica do modelo de controle do código-fonte.

### <a name="queryeditfiles-method"></a>Método QueryEditFiles
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> é chamado quando qualquer projeto ou editor deseja modificar um arquivo. O ideal é que esse método seja chamado *antes* de o arquivo ser modificado e quando um arquivo é salvo. Quando invocado, o `IVsQueryEditQuerySave2::QueryEditFiles` método verifica se os arquivos fornecidos estão sob controle do código-fonte, se eles precisam ser extraídos e se podem ser recarregados. Se as circunstâncias impedirem que os arquivos sejam editáveis, o `IVsQueryEditQuerySave2::QueryEditFiles` método instruirá o programa de chamada a cancelar a edição. Também é possível que o chamador especifique um modo de invocação. No modo "silencioso", esse método executará uma ação somente se não fizer com que nenhuma interface do usuário apareça. Se a interface do usuário for inevitável, um sinalizador deverá ser retornado para indicar o problema.

 O método se comporta de forma transacional; ou seja, se a edição for cancelada em um único arquivo, a edição será cancelada para todos os arquivos. Por outro lado, se a edição for permitida, ela será permitida para todos os arquivos. Se esse método permitir a edição uma vez para um determinado conjunto de arquivos, ele deverá sempre permitir a edição nas chamadas subsequentes para o mesmo conjunto de arquivos. O loop Allow-Edit continua até que os arquivos sejam fechados, salvos e recarregados; até que seus atributos (Propriedades) mudem; ou até que o pacote de controle do código-fonte seja alterado. Os casos a serem considerados na implementação do `IVsQueryEditQuerySave2::QueryEditFiles` método incluem vários arquivos, arquivos especiais, cancelamento do usuário e edições na memória.

### <a name="querysavefiles-method"></a>Método QuerySaveFiles
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> é chamado quando qualquer projeto ou editor precisa salvar um conjunto de arquivos. Quando invocado, o `IVsQueryEditQuerySave2::QuerySaveFiles` método verifica se os arquivos fornecidos são somente leitura e se estão sob controle do código-fonte. Se for necessário fazer check-out dos arquivos, a chamada será delegada ao pacote de controle do código-fonte. Se as circunstâncias impedirem que os arquivos sejam salvos, o `IVsQueryEditQuerySave2::QuerySaveFiles` método deverá informar ao editor para cancelar o salvamento. Assim como no `IVsQueryEditQuerySave2::QueryEditFiles` método, é possível que o chamador especifique um modo de invocação. No modo "silencioso", esse método executará uma ação somente se não fizer com que nenhuma interface do usuário apareça. Se a interface do usuário for inevitável, um sinalizador deverá ser retornado para indicar o problema.

 Esse método deve se comportar de forma transacional; ou seja, se o salvamento for cancelado em um único arquivo, o salvamento será cancelado para todos os arquivos. Por outro lado, se o salvamento for permitido, ele deverá ser permitido para todos os arquivos. Assim como acontece com o `IVsQueryEditQuerySave2::QueryEditFiles` método, os casos a serem considerados na implementação do `IVsQueryEditQuerySave2::QuerySaveFiles` método incluem vários arquivos, arquivos especiais, cancelamento do usuário e edições na memória.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
