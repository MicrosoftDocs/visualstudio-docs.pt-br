---
title: 'Como: Set Debug and Release Configurations | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.builds
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- configurations, release
- build configurations, release
- projects [Visual Studio], release configurations
- debugging [Visual Studio], release configurations
- release builds, changing settings
- debug builds
- debug builds, switching to release build
- debug builds, changing configuration settings
- debugging [Visual Studio], debug configurations
- projects [Visual Studio], debug configurations
- build configurations, debug
- debug configurations
- release builds, switching to debug build
- Visual Basic projects, debug and release builds
ms.assetid: 57b6bbb7-f2af-48f7-8773-127d75034ed2
caps.latest.revision: 48
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ba827fda69b1dc455df4efe9c9f6eb83687780f3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758491"
---
# <a name="how-to-set-debug-and-release-configurations"></a>Como definir configurações de depuração e versão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Projetos do Visual Studio tem a versão separada e configurações para o seu programa de depuração. Como os nomes já dizem, você compila a versão de depuração para depuração e a versão de lançamento para a distribuição da versão final.  
  
 A configuração de depuração do seu programa é compilada com informações de depuração simbólica e sem otimização. A otimização complica a depuração, porque a relação entre o código fonte e as instruções geradas é mais complexa.  
  
 A configuração de versão do seu programa não contém nenhuma informação de depuração simbólica e é totalmente otimizada. Informações de depuração podem ser geradas em Arquivos PDB, dependendo das opções do compilador que são usadas. Criar arquivos PDB pode ser muito útil se você posteriormente precisa depurar a versão de lançamento.  
  
 Para obter mais informações sobre configurações de build, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md).  
  
 Você pode alterar a configuração de compilação a **Build** menu, na barra de ferramentas ou nas páginas de propriedades do projeto. Páginas de propriedades do projeto são específicas do idioma. O procedimento a seguir mostra como alterar a configuração de build no menu e barra de ferramentas. Para obter mais informações sobre como alterar a configuração de build em projetos em linguagens diferentes, consulte a seção de tópicos relacionados abaixo.  
  
### <a name="to-change-the-build-configuration"></a>Para alterar a configuração de build  
  
1.  No menu Build: clique em **Build / Configuration Manager**, em seguida, selecione **Debug** ou **versão**.  
  
2.  Na barra de ferramentas, escolha **Debug** ou **Release** do **configurações da solução** caixa de listagem.  
  
     ![configuração de build da barra de ferramentas](../debugger/media/toolbarbuildconfiguration.png "ToolbarBuildConfiguration")  
  
     Essa barra de ferramentas não está disponível nas edições Express. Você pode usar o **solução de compilação F6** e **iniciar depuração F5** itens de menu para escolher a configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)   
 [Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [Configurações do projeto para configurações de depuração de C#](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Configurações do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md)   
 [Debug and Release Project Configurations](http://msdn.microsoft.com/en-us/0440b300-0614-4511-901a-105b771b236e) (Configurações de projeto de depuração e lançamento)



