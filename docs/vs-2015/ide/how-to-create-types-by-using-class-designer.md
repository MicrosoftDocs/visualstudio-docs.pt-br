---
title: Como criar tipos usando o Designer de Classe | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.Clr.ClrAttributesDialog
helpviewer_keywords:
- custom attributes, applying
- class diagrams, creating types
- classes [Visual Studio], creating with Class Designer
- Class Designer [Visual Studio], creating classes
- types [Visual Studio], class diagrams
- attributes [Visual Studio], applying custom
ms.assetid: 94458c31-28bc-40e2-9737-85868788a0e5
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d05b8a492768dfe9163d7ede55c2bf4aef084c26
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668021"
---
# <a name="how-to-create-types-by-using-class-designer"></a>Como criar tipos usando Designer de Classe
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para o design de novos tipos para projetos do Visual C# .NET and Visual Basic .NET, crie-os em um diagrama de classes. Para ver os tipos existentes, consulte [Como exibir tipos existentes (Designer de Classe)](../ide/how-to-view-existing-types-class-designer.md).

- [Criar um novo tipo](#CreateType)

- [Aplicar um atributo personalizado a um tipo](#CustAttributeType)

- [Aplicar um atributo personalizado a um membro de tipo](#CustAttributeMember)

## <a name="CreateType"></a> Criar um novo tipo

1. Na Caixa de Ferramentas, em Designer de Classe, arraste um dos itens abaixo para um diagrama de classes:

    - **Classe** ou **Classe Abstrata**

    - **Enum**

    - **Interface**

    - **Estrutura** (VB) ou **Struct** (C#)

    - **Delegado**

    - **Módulo** (apenas VB)

2. Dê um nome ao tipo. Selecione o nível de acesso.

3. Selecione o arquivo em que deseja adicionar o código inicial para o tipo:

    - Para criar um novo arquivo e adicioná-lo ao projeto atual, selecione **Criar novo arquivo** e dê um nome ao arquivo.

    - Para adicionar código a um arquivo existente, selecione **Adicionar a arquivo existente**.

         Se sua solução tiver um projeto que compartilha código entre vários aplicativos, você poderá adicionar um novo tipo a um diagrama de classes no projeto do aplicativo, mas somente se o arquivo de classe correspondente estiver no mesmo projeto de aplicativo ou no projeto compartilhado.

4. Agora adicione outros itens para definir o tipo:

    |||
    |-|-|
    |**Para**|**Adicionar**|
    |Classes, classes abstratas, estruturas ou structs|Métodos, propriedades, campos, eventos, construtores (método), destruidores (método) e constantes que definem o tipo|
    |Enums|Valores de campo que compõem a enumeração|
    |Interfaces|Métodos, propriedades e eventos que compõem a interface|
    |delegado|Parâmetros que definem o representante|
    |Módulo|Métodos, propriedades, campos, eventos, construtores (método) e constantes que definem o módulo|

     Consulte [Criando membros](../ide/creating-and-configuring-type-members-class-designer.md#CreateMembers).

## <a name="CustAttributeType"></a> Aplicar um atributo personalizado a um tipo

1. Clique na forma do tipo em um diagrama de classes.

2. Na janela Propriedades, ao lado da propriedade **Atributos Personalizados** do tipo, clique no botão de reticências (…).

3. Adicione um ou mais atributos personalizados, um por linha. Não os coloque entre colchetes.

     Quando terminar, os atributos personalizados são aplicados ao tipo.

## <a name="CustAttributeMember"></a> Aplicar um atributo personalizado a um membro de tipo

1. Clique no nome do membro na forma de seu tipo em um diagrama de classes ou em sua linha na janela Detalhes da Classe.

2. Na janela Propriedades, localize a propriedade **Atributos Personalizados** do membro.

3. Adicione um ou mais atributos personalizados, um por linha. Não os coloque entre colchetes.

     Quando terminar, os atributos personalizados são aplicados ao tipo.

## <a name="see-also"></a>Consulte também
 [Como: criar herança entre tipos (Designer de classe)](../ide/how-to-create-inheritance-between-types-class-designer.md) [como criar associações entre tipos (Designer de classe)](../ide/how-to-create-associations-between-types-class-designer.md) [criando e configurando membros de tipo (Designer de classe)](../ide/creating-and-configuring-type-members-class-designer.md) [trabalhando com diagramas de classe (Designer de classe)](../ide/working-with-class-diagrams-class-designer.md) [Criando classes e tipos (Designer de classe)](../ide/designing-classes-and-types-class-designer.md)
