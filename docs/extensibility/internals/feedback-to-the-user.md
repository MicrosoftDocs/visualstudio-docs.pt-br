---
title: Comentários para o usuário | Microsoft Docs
description: Saiba como fornecer comentários visuais ao usuário sobre a funcionalidade disponível no IDE (ambiente de desenvolvimento integrado) do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user model feedback
- environment, context
- IDE, context
- IDE, user feedback
ms.assetid: 2d472a24-3813-4f5f-9783-b491ad8a71ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4d40ca34ea8d579e85ee56170f621b98a10b89f2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069628"
---
# <a name="feedback-to-the-user"></a>Comentários para o usuário
No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado), os comentários visuais relacionados à funcionalidade disponível baseiam-se na seleção atual do usuário e no contexto de seleção global. A tabela a seguir lista a funcionalidade que está disponível em contextos de seleção diferentes.

|Contexto de seleção|Funcionalidade disponível|
|-----------------------|-----------------------------|
|IDE|Global|
|Conjunto de produtos atual|Específico do produto|
|Hierarquia ativa|Tipo de hierarquia específico|
|Item de hierarquia ativa|Tipo de item de hierarquia específico|
|Documento ativo|Tipo de documento específico|
|Janela MDI (interface de vários documentos) superior|Específico do tipo de janela|
|Contexto de seleção atual|Contexto de seleção específico|

 Se você só Surface a funcionalidade de que os usuários precisam e fornece continuamente comentários de contexto de ambiente e seleção consistente, reduza a complexidade no IDE. As regras a seguir se aplicam sempre que uma janela é aberta no IDE:

- Se a janela alterar seu contexto de seleção, os comentários de seleção serão indicados claramente na janela e a janela de **Ajuda dinâmica** , se mostrada, será atualizada para refletir o contexto atual.

- Se a janela alterar o contexto de seleção global, todos os menus específicos de contexto, a janela de hierarquia ativa e a barra de título do aplicativo serão atualizados para refletir o contexto atual.

- A janela deve trazer as propriedades de superfície para a seleção atual na janela **Propriedades** e, opcionalmente, se mostrado, a caixa de diálogo **páginas de propriedades** .

- Se a janela não Surface Propriedades ou alterar o contexto de seleção global, os comentários de seleção não deverão permanecer na janela quando ela não for mais a janela ativa no IDE.

- Todas as janelas de ferramentas específicas do documento devem refletir continuamente o documento ativo.

- Menus, barras de ferramentas e a barra de título do aplicativo devem refletir a janela de cliente MDI (interface de vários documentos) superior.

  Por exemplo, quando o modo de exibição HTML de um **formulário da Web** dentro de um Visual Basic projeto de aplicativo Web é aberto e o usuário seleciona uma `<td>` marca, os comentários são fornecidos da seguinte maneira:

- A seleção é indicada na janela ativa e refletida na janela **Propriedades** .

- A **caixa de ferramentas** específica do documento é atualizada para refletir o documento ativo.

- A barra de ferramentas do **Editor** e o menu **tabela** são exibidos e a barra de título é atualizada para refletir a janela do Web Form.

- A janela de hierarquia ativa, que normalmente é **Gerenciador de soluções** e sua atualização da barra de título para refletir o contexto atual e os comandos do menu de **projeto** sensível ao contexto agora se aplicam ao projeto de aplicativo Web ativo.

## <a name="see-also"></a>Confira também
- [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [Objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md)
- [Hierarquias e seleção](../../extensibility/internals/hierarchies-and-selection.md)
