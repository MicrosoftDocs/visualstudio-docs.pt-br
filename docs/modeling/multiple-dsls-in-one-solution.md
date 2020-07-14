---
title: Várias DSLs em uma mesma solução
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f2eef29db24da3be0a9376ea76a9a1a551af9e1a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542591"
---
# <a name="multiple-dsls-in-one-solution"></a>Várias DSLs em uma mesma solução

É possível empacotar diversas DSLs como parte de uma única solução para serem instaladas juntas.

É possível usar diversas técnicas para integrar múltiplas DSLs. Para obter mais informações, consulte [integrando modelos usando o Visual Studio ModelBus](../modeling/integrating-models-by-using-visual-studio-modelbus.md) e [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md) e [Personalizar o comportamento de cópia](../modeling/customizing-copy-behavior.md).

## <a name="build-more-than-one-dsl-in-the-same-solution"></a>Compilar mais de uma DSL na mesma solução

1. Crie um novo projeto de **projeto VSIX** .

2. Crie dois ou mais projetos DSL no diretório da solução VSIX.

   - Abra uma nova instância do Visual Studio para cada DSL. Crie a nova DSL e especifique a mesma pasta da solução que a solução VSIX.

   - Certifique-se de criar cada DSL com uma extensão de nome de arquivo diferente.

   - Altere os nomes dos projetos **DSL** e **DslPackage** para que eles sejam todos diferentes. Por exemplo: `Dsl1` , `DslPackage1` , `Dsl2` , `DslPackage2` .

   - Em cada **DslPackage \* \ Source.Extension.tt**, atualize essa linha para o nome do projeto DSL correto:

      `string dslProjectName = "Dsl2";`

   - Na solução VSIX, adicione os projetos DSL * e DslPackage \* . É aconselhável colocar cada par em sua própria pasta da solução.

2. Combine os manifestos VSIX das DSLs:

   1. Abra _YourVsixProject_**\Source.Extension.manifest**.

   2. Para cada DSL, escolha **adicionar conteúdo** e adicionar:

       - `Dsl*`projeto como um **componente do MEF**

       - `DslPackage*`projeto como um **componente do MEF**

       - `DslPackage*`projeto como um **pacote do vs**

3. Compile a solução.

   O VSIX resultante instalará as duas DSLs. Você pode testá-los usando F5 ou implantar _YourVsixProject_**\bin\Debug \\ \* . vsix**.

## <a name="see-also"></a>Confira também

- [Integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [Como adicionar um manipulador de evento do tipo "arrastar e soltar"](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md)