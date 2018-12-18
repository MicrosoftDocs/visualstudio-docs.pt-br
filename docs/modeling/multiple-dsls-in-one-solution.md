---
title: Várias DSLs em uma mesma solução
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: f73fd8170c91fe51692c9ec5b5b39e7c36570dd2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949364"
---
# <a name="multiple-dsls-in-one-solution"></a>Várias DSLs em uma mesma solução
É possível empacotar diversas DSLs como parte de uma única solução para serem instaladas juntas.

 É possível usar diversas técnicas para integrar múltiplas DSLs. Para obter mais informações, consulte [integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md) e [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md) e [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md).

### <a name="to-build-more-than-one-dsl-in-the-same-solution"></a>Compilar mais de uma DSL na mesma solução

1. Crie duas ou mais soluções DSL e um projeto VSIX e adicione todos os projetos a uma única solução.

   -   Para criar um novo projeto VSIX: na **novo projeto** caixa de diálogo, selecione **Visual c#**, **extensibilidade**, **projeto VSIX**.

   -   Crie duas ou mais soluções DSL no diretório da solução VSIX.

        Abra uma nova instância do Visual Studio para cada DSL. Crie a nova DSL e especifique a mesma pasta da solução que a solução VSIX.

        Certifique-se de criar cada DSL com uma extensão de nome de arquivo diferente.

   -   Alterar os nomes da **Dsl** e **DslPackage** projetos para que eles estejam todos diferentes. Por exemplo: `Dsl1`, `DslPackage1`, `Dsl2`, `DslPackage2`.

   -   Em cada **DslPackage\*\source.extension.tt**, atualize essa linha para o nome do projeto Dsl correto:

        `string dslProjectName = "Dsl2";`

   -   Na solução VSIX, adicione o Dsl * e DslPackage\* projetos.

        É aconselhável colocar cada par em sua própria pasta da solução.

2. Combine os manifestos VSIX das DSLs:

   1.  Abra _YourVsixProject_**\source.extension.manifest**.

   2.  Para cada DSL, escolha **adicionar conteúdo** e adicione:

       -   `Dsl*` um projeto como um **componente MEF**

       -   `DslPackage*` um projeto como um **componente MEF**

       -   `DslPackage*` um projeto como um **VS Package**

3. Compile a solução.

   O VSIX resultante instalará as duas DSLs. Você pode testá-las usando F5 ou implantar _YourVsixProject_**\bin\Debug\\\*. VSIX**.

## <a name="see-also"></a>Consulte também

- [Integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [Como adicionar um manipulador de evento do tipo "arrastar e soltar"](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md)