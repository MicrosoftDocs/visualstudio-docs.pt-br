---
title: Como criar herança entre tipos (Designer de Classe)
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.classdesigner.inheritanceline
helpviewer_keywords:
- inheritance, relationship defining
- relationships, defining inheritance
ms.assetid: 3786a21c-8022-4bf5-9d13-740fd354e93c
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1ffae72a3fe171b6bd16cfbc623a777f4d4d2e4
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770206"
---
# <a name="how-to-create-inheritance-between-types-in-class-designer"></a>Como criar herança entre tipos no Designer de Classe

Para criar uma relação de herança entre dois tipos em um diagrama de classe usando **Designer de classe**, conecte o tipo base com seu tipo ou tipos derivados. Você pode ter uma relação de herança entre duas classes, entre uma classe e uma interface ou entre duas interfaces.

## <a name="to-create-an-inheritance-between-types"></a>Para criar uma herança entre tipos

1. Em seu projeto no **Gerenciador de soluções**, abra um arquivo de diagrama de classe (. CD).

     Se você não possuir um diagrama de classes, crie um. Consulte [como: Adicionar diagramas de classe a projetos](how-to-add-class-diagrams-to-projects.md).

2. Na **Caixa de Ferramentas**, no **Designer de Classe**, clique em **Herança**.

3. No diagrama de classes, desenhe uma linha de herança entre os tipos que você deseja, começando de:

    - Uma classe derivada para uma classe base

    - Uma classe de implementação para uma interface implementada

    - Uma interface em extensão para uma interface estendida

4. Se desejar, quando você tiver um tipo derivado de um tipo genérico, clique na linha de herança. Na janela **Propriedades**, defina a propriedade **Argumentos de Tipo** para corresponder ao tipo que você deseja para o tipo genérico.

    > [!NOTE]
    > Se uma classe abstrata pai contiver pelo menos um membro abstrato, todos os membros abstratos serão implementados como classes de herança não abstratas.
    >
    >  Embora você possa visualizar os tipos genéricos existentes, não é possível criar novos tipos genéricos. Você também não pode alterar os parâmetros de tipos genéricos existentes.

## <a name="see-also"></a>Confira também

- [Herança](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
- [Noções básicas de herança](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [Como exibir herança entre tipos](how-to-view-inheritance-between-types.md)
- [Classes do Visual C++ no Designer de Classe](visual-cpp-classes.md)
