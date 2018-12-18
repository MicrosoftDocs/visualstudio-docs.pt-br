---
title: Eventos de Buffer de texto na API herdada | Microsoft Docs
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
- editors [Visual Studio SDK], legacy - text buffer events
ms.assetid: 9be49e9f-1864-41c2-8a3c-f66895881341
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 677824142f2e7e497888627041cfe7a82487d342
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51735509"
---
# <a name="text-buffer-events-in-the-legacy-api"></a>Eventos de Buffer de texto na API herdada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O objeto de buffer de texto emite vários eventos diferentes que permitem que você responda às situações diferentes.  
  
 Quando você estiver usando a API herdada, você deve implementar as seguintes interfaces para receber a notificação de alterações para o buffer de texto. Expõe as interfaces para o buffer de texto usando o `IConnectionPointContainer` modificações na interface do buffer de texto para receber notificação da linha do buffer. Para obter mais informações, consulte [como: se registrar para eventos de Buffer de texto com a API herdada](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md). No caso de `IVsTextStreamEvents` ou `IVsTextLinesEvents` interfaces, as alterações são retornadas em qualquer um ou bidimensional coordenadas, respectivamente.  
  
## <a name="text-buffer-interfaces"></a>Interfaces de Buffer de texto  
 A seguir estão as interfaces implementadas pelo objeto de buffer de texto.  
  
|Interface|Descrição|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|Permite a criação de ações compostas (ou seja, ações que são agrupadas em uma unidade de desfazer/refazer único).|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|Habilita a persistência de dados do documento gerenciados pelo buffer de texto.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|Fornece serviços básicos; usado por muitos clientes.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|Fornece ler e gravar recursos usando as coordenadas bidimensionais. Herda de `IVsTextBuffer`.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|Rápido e fornece acesso sequencial orientada por fluxo para o texto no buffer.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|Fornece ler e gravar recursos usando coordenadas unidimensionais. Herda de `IVsTextBuffer`.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|Fornece acesso a uma coleção genérica de propriedades. A propriedade mais importante é o nome ou o moniker do buffer. Você pode armazenar seus próprios dados aleatórios em buffer com essa interface criando um GUID e usá-lo como uma chave.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|Dá suporte a pontos de conexão para eventos.|  
  
## <a name="text-buffer-event-interfaces"></a>Interfaces de evento do Buffer de texto  
 A seguir estão as interfaces para notificação de eventos do buffer de texto.  
  
|Interface|Descrição|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferEvents>|Notifica os clientes quando um novo serviço de linguagem está associado um buffer de texto.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferDataEvents>|Notifica os clientes quando um buffer de texto é inicializado e quando são feitas alterações aos dados no buffer de texto.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamEvents>|Notifica os clientes de alterações para o buffer de texto subjacente em coordenadas unidimensionais.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents>|Notifica os clientes de alterações para o buffer de texto subjacente em coordenadas bidimensionais.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserDataEvents>|Notifica os clientes de alterações aos dados do usuário.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsPreliminaryTextChangeCommitEvents>|Notifica os clientes do gesto última confirmação para disparar o evento e fornece uma gama de alteração de texto. O `IVsPreliminaryTextChangeCommitEvents` interface não é acionado em resposta a desfazer ou refazer comandos. Eventos acionados apenas para os buffers que tenham um Gerenciador de desfazer. `IVsPreliminaryTextChangeCommitEvents` é acionado antes de outros eventos, como uma lista muito, para garantir que os outros eventos não alteram o texto antes que as alterações sejam confirmadas. O VSPackage deverá monitorar qualquer uma de `IVsPreliminaryTextChangeCommitEvents` interface ou o `IVsFinalTextChangeCommitEvents` interface, mas não ambos.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFinalTextChangeCommitEvents>|Notifica os clientes do gesto última confirmação para disparar o evento e fornece uma gama de alteração de texto. O `IVsFinalTextChangeCommitEvents` interface não é acionado em resposta a desfazer ou refazer comandos. Eventos acionados apenas para os buffers que tenham um Gerenciador de desfazer. `IVsFinalTextChangeCommitEvents` destina para uso apenas por serviços de linguagem ou outros objetos que têm controle total sobre a edição. O VSPackage deverá monitorar qualquer uma de `IVsPreliminaryTextChangeCommitEvents` interface ou o `IVsFinalTextChangeCommitEvents` interface, mas não ambos.|  
  
## <a name="see-also"></a>Consulte também  
 [Acessando o Buffer de texto usando a API herdada](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)   
 [Como registrar para eventos de buffer de texto com a API herdada](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)

