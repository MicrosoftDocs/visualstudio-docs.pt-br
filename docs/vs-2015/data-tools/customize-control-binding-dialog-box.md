---
title: Personalizar o controle de caixa de diálogo associação | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.datasource.datauicustomization
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- Customize Control Binding dialog box
ms.assetid: abcc0be3-a18e-4f47-b354-d6b0c618e087
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 8ca2da23040f3e7a57fe5da2ff8b87cc7fc38099
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49889685"
---
# <a name="customize-control-binding-dialog-box"></a>Caixa de diálogo Personalizar Associação de Controle
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use o **personalizar associação de controle** caixa de diálogo para especificar quais controles estão disponíveis para itens na [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992).  
  
 Cada item na **fontes de dados** janela tem uma lista associada de controles que podem ser associadas ao item. Os controles disponíveis para cada item são determinados pelo tipo de dados do item. Cada tipo de dados tem uma lista de controles associados válidos definidos nesta caixa de diálogo, incluindo um controle padrão.  
  
 Antes de arrastar um item para uma superfície de design para criar um controle associado a dados, você pode selecionar qual controle para criar. Se você arrastar um item a partir de **fontes de dados** janela na superfície de design sem selecionar um controle, o controle padrão para o tipo de dados do item selecionado é adicionado à superfície de design.  
  
 Para obter mais informações sobre como usar essa caixa de diálogo para personalizar a lista de controles para os itens a **fontes de dados** janela, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Tipo de dados**  
 Exibe uma lista de tipos que você associar controles:  
  
- Tabelas, entidades e objetos são representados como **[List]** tipos.  
  
- Colunas ou propriedades públicas dos objetos e entidades são representadas como o tipo de dados da coluna ou propriedade no armazenamento de dados subjacente.  
  
- Objetos com formas definidas pelo usuário são representados como **[Other]**. Por exemplo, se seu aplicativo tiver um controle personalizado que exibe dados de mais de uma propriedade de um objeto, selecione o **[Other]** tipo de dados para o seu controle.  
  
  **Controles associados**  
  Exibe uma lista de controles que você pode associar um tipo de dados específico. Se você deseja associar um controle específico com o tipo de dados selecionado na **tipo de dados** , selecione a caixa de seleção correspondente. Desmarque a caixa de seleção para remover uma associação. Verificado controles aparecem no menu de atalho apresentado pelo **fontes de dados** janela para um item do tipo de dados associado.  
  
  Você pode adicionar controles à lista adicionando controles que têm um dos vários atributos de associação de dados para o **caixa de ferramentas**. Para obter mais informações, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).  
  
  **Defina o valor padrão**  
  Atribui o tipo de controle selecionado para ser o padrão para itens do tipo de dados selecionado. O controle padrão aparece como a primeira seleção no menu de atalho apresentado pelo **fontes de dados** janela para um item. Tipo de apenas um controle pode ser atribuído como o padrão para um tipo de dados.  
  
  **Limpar padrão**  
  Remove a designação de um controle como o padrão para o tipo de dados selecionado. Se não houver nenhum padrão para o tipo de dados selecionada **[Nenhum]** aparece como a primeira seleção no menu de atalho apresentado pelo **fontes de dados** janela para um item do tipo associado.  
  
## <a name="see-also"></a>Consulte também  
 [Janela Fontes de Dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)   
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md)   
 [Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)