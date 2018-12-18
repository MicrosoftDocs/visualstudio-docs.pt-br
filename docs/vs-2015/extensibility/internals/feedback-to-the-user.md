---
title: Comentários para o usuário | Microsoft Docs
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
- user model feedback
- environment, context
- IDE, context
- IDE, user feedback
ms.assetid: 2d472a24-3813-4f5f-9783-b491ad8a71ad
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 509dffa0d2a474059277dbb3df2ba984fa35fe42
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51751165"
---
# <a name="feedback-to-the-user"></a>Comentários para o usuário
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente de desenvolvimento integrado (IDE), comentários visuais sobre funcionalidade disponível é com base na seleção atual do usuário e o contexto de seleção global. A tabela a seguir lista a funcionalidade que está disponível em contextos diferentes de seleção.  
  
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
  
- Se a janela for alterado em seu contexto de seleção, comentários da seleção está indicado claramente na janela e a janela Ajuda dinâmica, se exibido, é atualizada para refletir o contexto atual.  
  
- Se a janela altera o contexto de seleção global, todos os menus de contexto específico, a janela hierarquia do Active Directory e a barra de título do aplicativo são atualizados para refletir o contexto atual.  
  
- A janela deve revelar as propriedades para a seleção atual na **propriedades** janela e, opcionalmente, se exibido, o **páginas de propriedade** caixa de diálogo.  
  
- Se não, a janela Propriedades de superfície ou alterar o contexto de seleção global, comentários da seleção não devem permanecer na janela quando ela não é mais a janela ativa no IDE.  
  
- Todas as janelas de ferramenta específica do documento continuamente devem refletir o documento ativo.  
  
- Menus, barras de ferramentas e a barra de título do aplicativo devem refletir a janela do cliente de nível mais alto MDI (interface MDI).  
  
  Por exemplo, quando o modo de exibição HTML de um formulário da Web dentro de um projeto de aplicativo Web do Visual Basic é aberto e o usuário seleciona um `<td>` marca, os comentários são fornecidos da seguinte maneira:  
  
- Seleção é indicada na janela ativa e refletida na **propriedades** janela.  
  
- Específicos do documento **caixa de ferramentas** é atualizada para refletir o documento ativo.  
  
- O **Editor** barra de ferramentas e **tabela** menu são exibidas e a barra de título seja atualizada para refletir a janela do formulário da Web.  
  
- A janela de hierarquia do Active Directory, que é normalmente **Gerenciador de soluções**e sua atualização de barra de título para refletir o contexto atual e o contextual **projeto** comandos de menu agora se aplicam à Web ativa Projeto de aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)   
 [Objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md)   
 [Seleção e hierarquias](../../extensibility/internals/hierarchies-and-selection.md)

