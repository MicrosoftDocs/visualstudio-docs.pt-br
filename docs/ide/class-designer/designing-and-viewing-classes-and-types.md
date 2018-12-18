---
title: Usar o Designer de Classe
ms.date: 05/08/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.diagram
helpviewer_keywords:
- Class Designer [Visual Studio]
- Class Designer, about Class Designer
- types [Visual Studio], viewing
- classes [Visual Studio], viewing
- class designer
ms.assetid: 40ed2c9d-0ce0-4b95-ad78-5dec2065ccea
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c4e4cf8e21f3f053783b1f7b70dcc51f2fd4ef2a
ms.sourcegitcommit: 1466ac0f49ebf7448ea4507ae3f79acb25d51d3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34447954"
---
# <a name="design-and-view-classes-and-types-with-class-designer"></a>Criar e exibir classes e tipos com o Designer de Classe

Crie, visualize e refatore classes e outros tipos no código com o **Designer de Classe** no Visual Studio. Use diagramas de classe para criar e editar classes em seu projeto C#, Visual Basic ou C++. Você também pode usar diagramas de classe para entender melhor a estrutura do projeto ou reorganizar o código.

## <a name="what-you-can-do-with-class-diagrams"></a>O que você pode fazer com diagramas de classe

- **Criar**: edite o código do projeto editando o diagrama de classe. Adicione novos elementos e exclua os que não deseja mais. As alterações serão refletidas no código.

- **Visualizar**: entenda a estrutura do projeto exibindo as classes do projeto em um diagrama. Personalize o diagrama para que você possa se concentrar nos detalhes do projeto mais importantes para você. Salve o diagrama para usar posteriormente na demonstração ou documentação.

- **Refatorar**: substitua métodos, renomeie identificadores, refatore parâmetros e implemente interfaces e classes abstratas.

## <a name="view-types-and-relationships"></a>Exibir tipos e relações

Os diagramas de classe mostram os detalhes de tipos, por exemplo, seus membros constituintes e as relações entre eles. A visualização dessas entidades é uma exibição dinâmica do código. Isso significa que é possível editar tipos no designer e, em seguida, ver as edições refletidas no código-fonte da entidade. Da mesma forma, o diagrama de classe é mantido sincronizado com as alterações feitas nos arquivos de código.

> [!NOTE]
> Se o projeto contiver um diagrama de classe e referenciar um tipo localizado em outro projeto, o diagrama de classe só mostrará o tipo referenciado quando o projeto for criado para esse tipo. Da mesma forma, o diagrama só exibirá as alterações no código da entidade externa quando o projeto for recompilado para essa entidade.

## <a name="class-diagram-workflow"></a>Fluxo de trabalho do diagrama de classe

Os diagramas de classe podem ajudar você a entender a estrutura de classe dos projetos. Esses projetos podem ter sido criados por outros desenvolvedores ou você apenas precisa de uma atualização em um projeto que você mesmo criou. Você pode usar diagramas de classe para personalizar, compartilhar e apresentar informações sobre o projeto para outras pessoas.

A primeira etapa na apresentação de informações do projeto é criar um diagrama de classe que exibe o que você deseja mostrar. Para obter mais informações, consulte [Add a class diagram](how-to-add-class-diagrams-to-projects.md) (Adicionar um diagrama de classe). Você pode criar vários diagramas de classe para um projeto que pode ser usado para exibir uma exibição distinta do projeto, um subconjunto escolhido dos tipos do projeto ou um subconjunto escolhido dos membros de tipos.

Além de definir o que cada diagrama de classe mostra, você também pode alterar a maneira como as informações são apresentadas. Para obter mais informações, consulte [Como personalizar diagramas de classe](how-to-customize-class-diagrams.md).

Depois de ajustar um ou mais diagramas de classe, copie-os em documentos do Microsoft Office e imprima ou exporte-os como arquivos de imagem. Para obter mais informações, consulte [Como copiar elementos de diagrama de classe para um documento do Microsoft Office](how-to-copy-class-diagram-elements-to-a-microsoft-office-document.md), [Como imprimir diagramas de classe](how-to-print-class-diagrams.md) e [Como exportar diagramas de classe como imagens](how-to-export-class-diagrams-as-images.md).

> [!NOTE]
> O Designer de Classe não controla o local dos arquivos de origem, por isso quando você altera a estrutura do projeto ou move os arquivos de origem no projeto, o Designer de Classe pode perder o controle do tipo, especialmente o tipo de origem de um typedef, classes base ou tipos de associação. Você pode receber um erro, como **O Designer de Classe não pode exibir esse tipo**. Se você fizer isso, arraste o código-fonte realocado ou modificado para o diagrama de classe, para exibi-lo novamente.

## <a name="see-also"></a>Consulte também

- [Recursos do Editor de Códigos](../writing-code-in-the-code-and-text-editor.md)
- [Mapear as dependências nas soluções](../../modeling/map-dependencies-across-your-solutions.md)