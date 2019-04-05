---
title: Usando o Gerenciador de texto para monitorar as configurações globais | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - monitor global settings
- editors [Visual Studio SDK], legacy - text manager
ms.assetid: 023e7671-cf65-419c-9bc1-3c4ee92aa436
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 792c566eda53cb8a4703e8ab03982952c518d8e4
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58923487"
---
# <a name="using-the-text-manager-to-monitor-global-settings"></a>Usando o Gerenciador de texto para monitorar as configurações globais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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
 [Dentro do Editor de núcleo](../extensibility/inside-the-core-editor.md)   
 [Recursos do Editor](http://msdn.microsoft.com/bdac940d-1f14-4019-a01f-fd0bb3dc7198)
