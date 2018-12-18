---
title: Modelos do Visual Studio para projetos e arquivos
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- templates [Visual Studio], project
- templates [Visual Studio], item
- item templates [Visual Studio]
- project templates [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 62e51a5a03011874acc723eaf159e3f7130d1340
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34573252"
---
# <a name="project-and-item-templates"></a>Modelos de projeto e de item

Os modelos de projeto e de item fornecem stubs reutilizáveis que oferecem aos usuários uma estrutura e um código básico que eles podem personalizar para suas próprias finalidades.

## <a name="visual-studio-templates"></a>modelos do Visual Studio

Vários modelos de itens e de projetos predefinidos são instalados com o Visual Studio. Por exemplo, os modelos **Aplicativo do Windows Forms** e **Biblioteca de Classes** do Visual Basic e do C# que são mostrados na caixa de diálogo **Novo Projeto** são modelos de projeto. Os modelos de item são mostrados na caixa de diálogo **Adicionar Novo Item** e incluem itens como arquivos de código, arquivos XML, páginas HTML e folhas de estilo.

Esses modelos fornecem um ponto de partida para os usuários começarem a criar projetos ou expandir projetos existentes. Os modelos de projeto fornecem os arquivos que são necessários para um tipo de projeto específico, incluem referências de assembly padrão e definem opções de compilador e propriedades de projeto padrão. Os modelos de item podem variar em complexidade desde apenas um arquivo vazio com uma determinada extensão de arquivo até vários arquivos de código-fonte com código de stub, arquivos de informações de designer e recursos inseridos.

É possível usar modelos instalados nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item**, criar seus próprios modelos ou baixar e usar modelos criados pela comunidade. Para obter mais informações, consulte [Como criar modelos de projeto](../ide/how-to-create-project-templates.md) e [Como criar modelos de item](../ide/how-to-create-item-templates.md).

## <a name="contents-of-a-template"></a>Conteúdo de um modelo

Todos os modelos de projeto e de item, sejam eles instalados com o Visual Studio ou criados por você, funcionam usando os mesmos princípios e têm conteúdo semelhante. Todos os modelos contêm os seguintes itens:

- Os arquivos a serem criados quando o modelo é usado. Eles incluem arquivos de código-fonte, recursos inseridos, arquivos de projeto e assim por diante.

- Um arquivo *.vstemplate*, contendo os metadados necessários para exibir o modelo nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item** e para criar um projeto ou um item do modelo. Para obter mais informações sobre arquivos *.vstemplate*, consulte [Parâmetros de modelo](../ide/template-parameters.md).

Quando esses arquivos são compactados em um arquivo *.zip* e colocados na pasta correta, o Visual Studio os exibe automaticamente nos seguintes locais:

- Os modelos de projeto aparecem na caixa de diálogo **Novo Projeto**.

- Os modelos de item aparecem na caixa de diálogo **Adicionar Novo Item**.

Para obter mais informações sobre pastas de modelo, consulte [Como localizar e organizar modelos](../ide/how-to-locate-and-organize-project-and-item-templates.md).

## <a name="see-also"></a>Consulte também

- [Como criar modelos de projeto](../ide/how-to-create-project-templates.md)
- [Como criar modelos de item](../ide/how-to-create-item-templates.md)
- [Parâmetros de modelo](../ide/template-parameters.md)
- [Personalizar modelos](../ide/customizing-project-and-item-templates.md)
- [Pacotes do NuGet em modelos do Visual Studio](/nuget/visual-studio-extensibility/visual-studio-templates)