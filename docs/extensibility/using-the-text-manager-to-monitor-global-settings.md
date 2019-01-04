---
title: Usando o Gerenciador de texto para monitorar as configurações globais | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - monitor global settings
- editors [Visual Studio SDK], legacy - text manager
ms.assetid: 023e7671-cf65-419c-9bc1-3c4ee92aa436
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 43b4f1c2de4862b30dd5822931b02292b942c50f
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53877543"
---
# <a name="use-the-text-manager-to-monitor-global-settings"></a>Use o Gerenciador de texto para monitorar as configurações globais
Se você implementar um editor de núcleo, você deve monitorar as alterações feitas às configurações globais, porque essas alterações podem afetar sua instância do editor. Você pode acompanhar as alterações através da escuta para eventos gerados pelo Gerenciador de texto. Por exemplo, quando você especifica uma preferência global para a aparência ou o comportamento de um componente no editor de núcleo, como seu objeto de dados de documento, o Gerenciador de texto armazena essas informações e comunica-se a todos os clientes afetados.  
  
## <a name="text-manager-functions"></a>Funções do Gerenciador de texto  
 O Gerenciador de texto aciona eventos para um número de configurações, incluindo o seguinte:  
  
- Se um buffer está sob controle do código-fonte  
  
- Como se registrar para notificações de alteração de arquivo  
  
- Como manter o controle de quais modos de exibição estão associados com determinados buffers  
  
- Preferências de colorização do texto  
  
- Guia versus preferências de espaço  
  
  As preferências que são exclusivas para um determinado idioma não são gerenciadas pelo Gerenciador de texto. Essas configurações devem ser gerenciadas por cada serviço de linguagem.  
  
  Notificação de eventos para o Gerenciador de texto é fornecida pelo <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents> interface. Implementar essa interface em seu cliente de objeto para manipular eventos gerou o Gerenciador de texto. Você pode registrar esses eventos usando o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> interface no Gerenciador de texto.  
  
## <a name="see-also"></a>Consulte também  
 [Dentro do editor de núcleo](../extensibility/inside-the-core-editor.md)   
 [Recursos do Editor](https://msdn.microsoft.com/library/bdac940d-1f14-4019-a01f-fd0bb3dc7198)