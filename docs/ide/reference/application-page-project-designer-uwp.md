---
title: Página de propriedades do aplicativo para aplicativos UWP
ms.date: 01/23/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- AppPackage.Properties.Application
helpviewer_keywords:
- Application page [UWP project]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 206c856eb87243fd6021c4ff8bb9f6890b8eaf25
ms.sourcegitcommit: 4708f0ba09b540424efcc344f8438f25432e3d51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2018
ms.locfileid: "44384208"
---
# <a name="application-property-page-uwp-projects"></a>Página de propriedades do aplicativo (projetos UWP)

Use a página de projetos do **Aplicativo** para especificar informações de assembly e pacote do projeto UWP (Plataforma Universal do Windows) e a versão de destino do Windows 10.

![Página de propriedades do aplicativo](media/application-page-uwp.png)

Para acessar a página **Aplicativo**, escolha um nó do projeto **Gerenciador de Soluções**. Em seguida, escolha **Projeto** > **Propriedades** na barra de menus. As páginas de propriedades são abertas na guia **Aplicativo**.

## <a name="general-section"></a>Seção geral

**Nome do assembly**&mdash;Especifica o nome do arquivo de saída que guardará o manifesto do assembly.

Para acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.AssemblyName%2A>.

**Namespace padrão**&mdash;Especifica o namespace base para arquivos adicionados ao projeto. Para saber mais sobre namespaces, confira [Namespaces (guia programação em C#)](/dotnet/csharp/programming-guide/namespaces/), [Namespaces (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/namespaces) ou [Namespaces (C++)](/cpp/cpp/namespaces-cpp).

Para acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.RootNamespace%2A>.

**Informações do Assembly**&mdash;Este botão exibe a [caixa de diálogo Informações do Assembly](../../ide/reference/assembly-information-dialog-box.md).

**Manifesto do Pacote**&mdash;Este botão abre o designer de manifesto. O designer de manifesto também pode ser acessado escolhendo o arquivo _Package.appxmanifest_ no **Gerenciador de Soluções**. Para saber mais, confira [Configurar um pacote com o designer de manifesto](/windows/uwp/packaging/packaging-uwp-apps#configure-an-app-package).

## <a name="targeting-section"></a>Seção de direcionamento

Você pode definir a versão de destino e a versão mínima do Windows 10 para seu aplicativo usando as listas suspensas nesta seção. Recomendamos que você direcione para a versão mais recente do Windows 10, e se você estiver desenvolvendo um aplicativo empresarial, que também ofereça suporte a uma versão mínima mais antiga. Para saber mais sobre qual versão do Windows 10 escolher, confira [Escolher uma versão do UWP](/windows/uwp/updates-and-versions/choose-a-uwp-version).

Para obter informações sobre a plataforma de direcionamento no Visual Studio 2017, consulte [Direcionamento da plataforma](/visualstudio/productinfo/vs2017-compatibility-vs#platform-targeting).

## <a name="see-also"></a>Consulte também

- [Criar seu primeiro aplicativo UWP](/windows/uwp/get-started/your-first-app)
- [Escolher uma versão de UWP](/windows/uwp/updates-and-versions/choose-a-uwp-version)