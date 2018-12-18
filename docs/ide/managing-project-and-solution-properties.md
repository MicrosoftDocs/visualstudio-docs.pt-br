---
title: Gerenciar propriedades do projeto e da solução
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 77ac77ca999ef627c0f3c9e763b7e5799b97d679
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349238"
---
# <a name="manage-project-and-solution-properties"></a>Gerenciar propriedades do projeto e da solução

Projetos têm propriedades que controlam muitos aspectos da compilação, da depuração, do teste e da implantação. Algumas propriedades são comuns entre todos os tipos de projeto, e algumas são exclusivas de linguagens ou plataformas específicas. Acesse as propriedades do projeto clicando com o botão direito do mouse no nó do projeto no **Gerenciador de Soluções** e escolhendo **Propriedades** ou digitando “propriedades” na caixa de pesquisa **Início Rápido** na barra de menus.

![Menu de contexto do projeto](../ide/media/vs2015_proj_prop_menu.gif)

Os projetos do .NET também podem ter um nó de propriedades na árvore do projeto em si.

![Nó de propriedades na árvore do Gerenciador de Soluções](../ide/media/vs2015_props_se.png)

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Gerenciando propriedades da solução e do projeto (Visual Studio para Mac)](/visualstudio/mac/managing-solutions-and-project-properties).

## <a name="project-properties"></a>Propriedades de projeto

As propriedades do projeto são organizadas em grupos e cada grupo tem sua própria página de propriedades. As páginas podem ser diferentes para idiomas e tipos de projeto distintos.

### <a name="c-visual-basic-and-f-projects"></a>Projetos em C#, Visual Basic e F#

Nos projetos em C#, Visual Basic e F#, as propriedades são expostas no **Designer de Projeto**. A ilustração a seguir mostra a página de propriedades **Build** para um projeto WPF em C#:

![Designer de Projeto do Visual Studio](../ide/media/vs2015_proppage_build.png)

Para obter informações sobre cada uma das páginas de propriedades no **Designer de Projeto**, confira [Referência de propriedades do projeto](../ide/reference/project-properties-reference.md).

> [!TIP]
> As soluções têm algumas propriedades, bem como os itens de projeto. Essas propriedades são acessadas na [janela Propriedades](../ide/reference/properties-window.md), não no **Designer de Projeto**.

### <a name="c-and-javascript-projects"></a>Projetos em C++ e JavaScript

Projetos em C++ e JavaScript têm uma interface do usuário diferente para gerenciar propriedades do projeto. Esta ilustração mostra uma página de propriedades de projeto em C++ (páginas em JavaScript são semelhantes):

![Propriedades de projeto do Visual C&#43;&#43;](../ide/media/vs2015_projprops_cpp.png)

Para obter informações sobre as propriedades do projeto C++, confira [Trabalhar com propriedades do projeto (C++)](/cpp/ide/working-with-project-properties). Para obter mais informações sobre as propriedades do JavaScript, confira [Páginas de propriedades, JavaScript](../ide/reference/property-pages-javascript.md).

## <a name="solution-properties"></a>Propriedades da solução

Para acessar propriedades na solução, clique com o botão direito do mouse no nó da solução no **Gerenciador de Soluções** e escolha **Propriedades**. Na caixa de diálogo, você pode definir as configurações do projeto para builds de **Depuração** ou **Versão** ou escolher quais projetos devem ser o projeto de inicialização quando **F5** é pressionado e definir as opções de análise de código.

## <a name="see-also"></a>Consulte também

- [Soluções e projetos no Visual Studio](../ide/solutions-and-projects-in-visual-studio.md)
- [Gerenciando propriedades da solução e do projeto (Visual Studio para Mac)](/visualstudio/mac/managing-solutions-and-project-properties)
