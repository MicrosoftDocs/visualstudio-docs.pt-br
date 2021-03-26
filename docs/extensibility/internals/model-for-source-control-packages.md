---
title: Modelo para pacotes de controle do código-fonte | Microsoft Docs
description: Esse modelo representa uma implementação de controle do código-fonte. O artigo mostra os nomes das classes para facilitar a visualização de como o controle do código-fonte é executado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], model
ms.assetid: 6164b2d3-a622-4de8-bef3-a6de985e9ebd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e4e437afdfa0d3de03da6814e221840cbd0763fd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063195"
---
# <a name="model-for-source-control-packages"></a>Modelo de pacotes de controle do código-fonte
O modelo a seguir representa um exemplo de uma implementação de controle do código-fonte. No modelo, você vê as interfaces que você deve implementar e os serviços de ambiente que você deve chamar. Como todos os serviços, você realmente chama os métodos de uma interface específica que você obtém por meio do serviço. Os nomes das classes são identificados para facilitar a visualização de como o controle do código-fonte é executado.

 ![Exemplos do SCC&#95;scrip](../../extensibility/internals/media/scc_tup.gif "SCC_TUP") Exemplo de projeto de controle do código-fonte

## <a name="interfaces"></a>Interfaces
 Você pode implementar o controle do código-fonte para seus novos tipos de projeto no Visual Studio usando a lista de interfaces mostrada na tabela a seguir.

|Interface|Uso|
|---------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|Chamado por projetos e editores antes que eles salvem ou alterem arquivos (sujos). Essa interface é acessada usando o <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> serviço do.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|Chamado por projetos para solicitar permissão para adicionar, remover ou renomear um arquivo ou diretório. Essa interface também é chamada por projetos para informar o ambiente quando uma ação de adição, remoção ou renomeação aprovada for concluída. Ele é acessado usando o <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> serviço.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|Implementado por qualquer entidade que se registra para ser notificado quando os projetos adicionam, renomeam ou removem um arquivo ou diretório. Para se registrar para notificação de eventos, chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A> .|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|Chamado por projetos para registrar com o pacote de controle do código-fonte e obter informações sobre o status do controle do código-fonte. Essa interface é acessada usando o <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> serviço do.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|Implementado pelo projeto para responder às solicitações de controle do código-fonte de informações sobre arquivos e obter as configurações de controle do código-fonte necessárias para o arquivo de projeto.|

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- [Suporte para controle do código-fonte](../../extensibility/internals/supporting-source-control.md)
