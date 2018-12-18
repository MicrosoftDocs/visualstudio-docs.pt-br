---
title: Gerenciar recursos do aplicativo (.NET)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- msvse_resedit.dlg.SetCustomTool
- msvse_settingsdesigner.err.formatvalue
- msvse_resedit.err.nameblank
- msvse_resedit.err.duplicatename
helpviewer_keywords:
- Resource Designer
- resources [Visual Studio]
- Resources page in Project Designer
- application resources [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b9a80a84276648f8a0f0d5a94992b5f58cbcfefa
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51348106"
---
# <a name="manage-application-resources-net"></a>Gerenciar recursos do aplicativo (.NET)

Arquivos de recurso são arquivos que fazem parte de um aplicativo, mas não são compilados, por exemplo, arquivos de ícone ou arquivos de áudio. Como esses arquivos não fazem parte do processo de compilação, você pode alterá-los sem precisar recompilar os binários. Se estiver planejando localizar seu aplicativo, você deverá usar arquivos de recurso para todas as cadeias de caracteres e outros recursos que precisam ser alterados ao localizar o aplicativo.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Gerenciando recursos de aplicativo (Visual Studio para Mac)](/visualstudio/mac/managing-app-resources).

Para obter mais informações sobre recursos em aplicativos de área de trabalho do .NET, confira [Recursos em aplicativos de área de trabalho](/dotnet/framework/resources/index).

## <a name="work-with-resources"></a>Trabalhar com recursos

Em um projeto de código gerenciado, abra a janela de propriedades do projeto. Você pode abrir a janela Propriedades das seguintes maneiras:

- Clicando com o botão direito do mouse no nó do projeto, no **Gerenciador de Soluções**, e selecionar **Propriedades**
- Digitando "propriedades do projeto" na janela do **Início Rápido**
- Escolhendo **Alt**+**Enter** no **Gerenciador de Soluções**

Selecione a guia **Recursos**. Você poderá adicionar um arquivo *.resx* se o projeto ainda não contiver um, adicionar e excluir diferentes tipos de recursos e modificar os recursos existentes.

## <a name="resources-in-other-project-types"></a>Recursos em outros tipos de projeto

Recursos são gerenciados de forma diferente em projetos do .NET que em outros tipos de projeto. Para obter mais informações sobre os recursos em:

- Aplicativos UWP (Plataforma Universal do Windows), consulte [Recursos do aplicativo e o Sistema de Gerenciamento de Recursos](/windows/uwp/app-resources/)
- Projetos C++, confira [trabalhar com arquivos de recurso](/cpp/windows/working-with-resource-files) e [Como criar um recurso](/cpp/windows/how-to-create-a-resource)

## <a name="see-also"></a>Consulte também

- [Recursos em aplicativos de área de trabalho (.NET Framework)](/dotnet/framework/resources/index)
- [Gerenciando recursos de aplicativo (Visual Studio para Mac)](/visualstudio/mac/managing-app-resources)
