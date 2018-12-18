---
title: Acessando o theText exibição usando a API herdada | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text view
ms.assetid: 8f751f72-c972-4be3-84ee-19c281e02e25
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3fe57ab7ef5ac113f1248f89cd62ef5b9ec33ca3
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39081817"
---
# <a name="access-the-text-view-by-using-the-legacy-api"></a>Acessar a exibição de texto, usando a API herdada
Uma exibição de texto é uma apresentação do texto que é armazenado em um buffer de texto. Você pode acessar a exibição de texto usando a API herdada, conforme mostrado na seção a seguir.

## <a name="text-view-object"></a>Objeto de exibição de texto
 Cada modo de exibição está associado com o próprio buffer de texto e o modo de exibição é uma janela sobre os dados no buffer. O diagrama a seguir mostra as interfaces principais do objeto de exibição de texto, que é representado por <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>.

 ![Objeto de exibição de texto do Visual Studio](../extensibility/media/vstextview.gif "vstextview") objeto de exibição de texto

 O modo de exibição é uma maneira de apresentar o texto no buffer. Ele inclui recursos como quebra automática de linha e a estrutura de tópicos, para que o que você vê no modo de exibição não é uma representação exata do texto no buffer.

 Um modo de exibição permite que outros serviços ou processos para interceptar os comandos de entrada e agir sobre eles antes do modo de exibição age sobre eles. O serviço mais comuns para fazer isso é um serviço de linguagem. Um serviço de linguagem talvez seja necessário, por exemplo, interceptar o comando para a tecla ENTER fornecer dicas personalizadas de comportamento ou a ferramenta de recuo.

## <a name="add-functionality-to-the-text-view"></a>Adicionar funcionalidade para a exibição de texto
 Você pode personalizar o comportamento do modo de exibição de texto ao manipular os pressionamentos de teclas específicos. Para interceptar os pressionamentos de teclas, você deve implementar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> em seu objeto e fornecer um destino de comando (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) para monitorar e interceptar comandos.

 A exibição de texto usa arquitetura sequencial para os filtros de comando. Novos filtros de comando (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objetos) são adicionados à sequência chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método.

 Notificação de eventos para o modo de texto é fornecida usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEvents> interface. Implemente essa interface em seu objeto de cliente para receber uma notificação de alterações para a exibição de texto. Expor essa interface para a exibição de texto usando o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> interface na exibição de texto para receber a notificação de alterações do modo de exibição.

## <a name="see-also"></a>Consulte também

- [Alterar as configurações de exibição usando a API herdada](../extensibility/changing-view-settings-by-using-the-legacy-api.md)
- [Use o Gerenciador de texto para monitorar as configurações globais](../extensibility/using-the-text-manager-to-monitor-global-settings.md)