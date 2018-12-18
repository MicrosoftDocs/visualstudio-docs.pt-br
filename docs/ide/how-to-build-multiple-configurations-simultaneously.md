---
title: Como criar várias configurações simultaneamente
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-compile
ms.topic: conceptual
ms.assetid: ba830937-3317-4674-8cc2-c0cd565603c5
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3e3e5fb1eea1d8bf821bf55b50ccfc1db488249b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49910596"
---
# <a name="how-to-build-multiple-configurations-simultaneously"></a>Como criar várias configurações simultaneamente

É possível compilar a maioria dos tipos de projetos com várias, ou até mesmo todas, as configurações de build ao mesmo tempo usando a caixa de diálogo **Build em Lotes**. No entanto, não é possível compilar os seguintes tipos de projetos em várias configurações de build ao mesmo tempo:

1. Aplicativos [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] criados para Windows usando JavaScript.

2. Todos os projetos do Visual Basic.

   Para obter mais informações sobre configurações de build, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md).

## <a name="to-build-a-project-in-multiple-build-configurations"></a>Para compilar um projeto em várias configurações de build

1. Na barra de menus, escolha **Criar** > **Criação em Lotes**.

2. Na coluna **Build**, marque as caixas de seleção para as configurações com as quais você deseja compilar um projeto.

    > [!TIP]
    > Para editar ou criar uma configuração de build para uma solução, escolha **Compilar** > **Gerenciador de Configurações** na barra de menus para abrir a caixa de diálogo **Gerenciador de Configurações**. Depois de editar uma configuração de build para uma solução, escolha o botão **Recompilar** na caixa de diálogo **Build em Lotes** para atualizar todas as configurações de build dos projetos na solução.

3. Escolha os botões **Build** ou **Recompilar** para compilar o projeto com as configurações especificadas.

## <a name="see-also"></a>Consulte também

- [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md)
- [Compreender configurações de build](../ide/understanding-build-configurations.md)
- [Criar vários projetos paralelamente](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)