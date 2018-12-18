---
title: Como compilar várias configurações simultaneamente | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba830937-3317-4674-8cc2-c0cd565603c5
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: aa16c4c02f92f71d3288896d56b94a6d570c7dd4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49930408"
---
# <a name="how-to-build-multiple-configurations-simultaneously"></a>Como compilar várias configurações simultaneamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível compilar a maioria dos tipos de projetos com várias, ou até mesmo todas, as configurações de build ao mesmo tempo usando a caixa de diálogo **Build em Lotes**. No entanto, não é possível compilar os seguintes tipos de projetos em várias configurações de build ao mesmo tempo:  
  
1. Aplicativos [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] criados para Windows usando JavaScript.  
  
2. Todos os projetos do Visual Basic.  
  
   Para obter mais informações sobre configurações de build, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md).  
  
### <a name="to-build-a-project-in-multiple-build-configurations"></a>Para compilar um projeto em várias configurações de build  
  
1.  Na barra de menus, escolha **Build**, **Build em Lotes**.  
  
2.  Na coluna **Build**, marque as caixas de seleção para as configurações com as quais você deseja compilar um projeto.  
  
    > [!TIP]
    >  Para editar ou compilar uma configuração de build para uma solução, escolha **Compilar**, **Configuration Manager** na barra de menus para abrir a caixa de diálogo **Configuration Manager**. Depois de editar uma configuração de build para uma solução, escolha o botão **Recompilar** na caixa de diálogo **Build em Lotes** para atualizar todas as configurações de build dos projetos na solução.  
  
3.  Escolha os botões **Build** ou **Recompilar** para compilar o projeto com as configurações especificadas.  
  
## <a name="see-also"></a>Consulte também  
 [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md)   
 [Noções sobre configurações de build](../ide/understanding-build-configurations.md)   
 [Compilando Vários Projetos Paralelamente](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)



