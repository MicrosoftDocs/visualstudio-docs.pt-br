---
title: Seleção e moeda no IDE | Microsoft Docs
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
- currency, Visual Studio IDE
- IDE, selection
- selection, Visual Studio IDE
- IDE, currency
ms.assetid: 2f6f18d1-acd8-454d-a856-9a4d81155052
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 45fc57bf2d5763527f9f8c2c6d8d22ca1d6369f8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786737"
---
# <a name="selection-and-currency-in-the-ide"></a>Seleção e moeda no IDE
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente de desenvolvimento integrado (IDE) mantém informações sobre dos usuários objetos selecionados no momento usando a seleção *contexto*. Com o contexto de seleção, os VSPackages pode fazer parte de moeda de acompanhamento de duas maneiras:  
  
-   Propagando as informações de moeda sobre os VSPackages ao IDE.  
  
-   Monitorando seleções ativa no momento dentro do IDE.  
  
## <a name="selection-context"></a>Contexto de seleção  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE globalmente mantém o controle de moeda IDE no seu próprio objeto de contexto de seleção global. A tabela a seguir mostra os elementos que compõem o contexto da seleção.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Hierarquia atual|Normalmente, o projeto atual; uma hierarquia do atual NULL indica que a solução como um todo é atual.|  
|ItemID atual|O item selecionado dentro da hierarquia atual; Quando há várias seleções em uma janela do projeto, pode haver vários itens atuais.|  
|Atual `SelectionContainer`|Contém um ou mais objetos para o qual a janela Propriedades deveria exibir propriedades.|  
  
 Além disso, o ambiente mantém duas listas globais:  
  
-   Uma lista de identificadores de comando do Active Directory da interface do usuário  
  
-   Uma lista de tipos de elemento ativo no momento.  
  
### <a name="window-types-and-selection"></a>Seleção e tipos de janelas  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE organiza windows em dois tipos gerais:  
  
- Windows de tipo de hierarquia  
  
- Janelas de quadro, como janelas de ferramentas e documentos  
  
  O IDE rastreia moeda diferente para cada um desses tipos de janela.  
  
  A janela de tipo de projeto mais comum é o Gerenciador de soluções, que controla o IDE. Uma janela do tipo de projeto controla a hierarquia global e o ItemID do contexto da seleção global e a janela se baseia na seleção do usuário para determinar a hierarquia atual. Para o windows de tipo de projeto, o ambiente fornece o serviço global <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>por quais VSPackages pode monitorar os valores atuais para os elementos abertos. Propriedade de navegação no ambiente é orientada por este serviço global.  
  
  Janelas de quadro, por outro lado, usam o DocObject dentro da janela de quadro para enviar por push o valor de SelectionContext (o trio de hierarquia/ItemID/SelectionContainer). . Janelas com moldura de usam o serviço <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> para essa finalidade. O DocObject pode enviar por push somente os valores para o contêiner de seleção, deixando os valores de locais para a hierarquia e ItemID inalterados, como é típico para documentos de filho MDI.  
  
### <a name="events-and-currency"></a>Eventos e moeda  
 Dois tipos de eventos podem ocorrer que afetam a noção do ambiente de moeda:  
  
-   Eventos que são propagados para o nível global e alterar o contexto de seleção do quadro de janela. Exemplos desse tipo de evento incluem uma janela filho MDI que está sendo aberta, uma janela de ferramenta global que está sendo aberto ou uma janela de ferramentas do tipo de projeto que está sendo aberto.  
  
-   Eventos que alteram os elementos rastreados dentro do contexto de seleção do quadro de janela. Exemplos incluem alterar a seleção dentro DocObject ou alterar a seleção em uma janela do tipo de projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md)   
 [Comentários para o usuário](../../extensibility/internals/feedback-to-the-user.md)

