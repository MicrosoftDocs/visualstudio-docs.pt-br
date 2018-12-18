---
title: Comentários para o usuário | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- user model feedback
- environment, context
- IDE, context
- IDE, user feedback
ms.assetid: 2d472a24-3813-4f5f-9783-b491ad8a71ad
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 39ab61615ed00504259909339734ab7874a6dfc6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49860364"
---
# <a name="feedback-to-the-user"></a>Comentários para o usuário
No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE), comentários visuais sobre funcionalidade disponível é com base na seleção atual do usuário e o contexto de seleção global. A tabela a seguir lista a funcionalidade que está disponível em contextos diferentes de seleção.  
  
|Contexto de seleção|Funcionalidade disponível|  
|-----------------------|-----------------------------|  
|IDE|Global|  
|Conjunto de produtos atual|Específico do produto|  
|Hierarquia do Active Directory|Hierarquia de tipo específicas|  
|Item de hierarquia do Active Directory|Específicos de tipo de item de hierarquia|  
|Documento ativo|Específico do tipo de documento|  
|Janela de nível mais alto MDI (interface MDI)|Tipo de janela específicas|  
|Contexto da seleção atual|Contexto de seleção específico|  
  
 Se você apenas surgir a funcionalidade que os usuários precisam e fornecem continuamente seleção consistente e comentários de contexto do ambiente, você pode reduzir a complexidade no IDE. As seguintes regras se aplicam sempre que uma janela é aberta no IDE:  
  
- Se a janela for alterado em seu contexto de seleção, os comentários da seleção está indicado claramente na janela e o **ajuda dinâmica** janela, se exibido, é atualizada para refletir o contexto atual.  
  
- Se a janela altera o contexto de seleção global, todos os menus de contexto específico, a janela hierarquia do Active Directory e a barra de título do aplicativo são atualizados para refletir o contexto atual.  
  
- A janela deve revelar as propriedades para a seleção atual na **propriedades** janela e, opcionalmente, se exibido, o **páginas de propriedade** caixa de diálogo.  
  
- Se não, a janela Propriedades de superfície ou alterar o contexto de seleção global, comentários da seleção não devem permanecer na janela quando ela não é mais a janela ativa no IDE.  
  
- Todas as janelas de ferramenta específica do documento continuamente devem refletir o documento ativo.  
  
- Menus, barras de ferramentas e a barra de título do aplicativo devem refletir a janela do cliente de nível mais alto MDI (interface MDI).  
  
  Por exemplo, quando o HTML exibir de uma **Web Form** dentro de um aplicativo Web do Visual Basic o projeto é aberto e o usuário seleciona um `<td>` marca, os comentários são fornecidos da seguinte maneira:  
  
- Seleção é indicada na janela ativa e refletida na **propriedades** janela.  
  
- Específicos do documento **caixa de ferramentas** é atualizada para refletir o documento ativo.  
  
- O **Editor** barra de ferramentas e **tabela** menu são exibidas e a barra de título seja atualizada para refletir a janela do formulário da Web.  
  
- A janela de hierarquia do Active Directory, que é normalmente **Gerenciador de soluções**e sua atualização de barra de título para refletir o contexto atual e o contextual **projeto** comandos de menu agora se aplicam à Web ativa Projeto de aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)   
 [Objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md)   
 [Seleção e hierarquias](../../extensibility/internals/hierarchies-and-selection.md)