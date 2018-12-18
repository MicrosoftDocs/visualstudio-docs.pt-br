---
title: Estendendo a caixa de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tools [Visual Studio], Toolbox
- Toolbox [Visual Studio SDK]
ms.assetid: bb84a79e-cd4c-4a58-8871-2513e7119b6e
caps.latest.revision: 38
manager: douge
ms.openlocfilehash: 444cf6b27179408414cc7df55d634497683004a6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49230328"
---
# <a name="extending-the-toolbox"></a>Estendendo a caixa de ferramentas
O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **caixa de ferramentas** fornece uma coleção de objetos que fornecem funcionalidade para designers e editores por meio do mecanismo de arrastar e soltar do IDE.  
  
 Há duas maneiras básicas no qual um VSPackage funciona com o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **caixa de ferramentas**:  
  
-   Um VSPackage pode adicionar novos itens de dados e controles para o **caixa de ferramentas**.  
  
-   Um VSPackage pode ser um destino ou um consumidor de existentes **caixa de ferramentas** funcionalidade, que dão suporte a operações arrastar e soltar e configurar o **caixa de ferramentas**da aparência.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Como criar um controle de caixa de ferramentas que usa o Windows Forms](../misc/how-to-create-a-toolbox-control-that-uses-windows-forms.md)  
 Descreve o limite para criar um controle de caixa de ferramentas usando o modelo de controle de caixa de ferramentas do Windows Forms.  
  
 [Criar um controle de caixa de ferramentas do WPF](../extensibility/creating-a-wpf-toolbox-control.md)  
 Descreve o limite para criar um controle de caixa de ferramentas usando o modelo de controle de caixa de ferramentas do WPF.  
  
 [Gerenciando a caixa de ferramentas](../misc/managing-the-toolbox.md)  
 Descreve como um VSPackage pode gerenciar o conteúdo e a aparência do **caixa de ferramentas**.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Como gerenciar a janela Caixa de Ferramentas](http://msdn.microsoft.com/en-us/a022c3fe-298c-4a59-a48f-b050da90ebc2)  
 Descreve como trabalhar com o **caixa de ferramentas** no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE).  
  
 [Como: controle de caixa de ferramentas](http://msdn.microsoft.com/library/c9d8a18a-d2bc-43d4-a803-601bfc6a6599)  
 Descreve como gerenciar o **caixa de ferramentas** usando o modelo de programação de automação.  
  
 [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)  
 Explica como usar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] services para criar elementos de interface do usuário que correspondem ao restante do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].