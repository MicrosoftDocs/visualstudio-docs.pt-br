---
title: Compartilhando classes entre DSLs por meio de uma biblioteca de DSLs
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: ccfb4fa9de6513ecc36cad7156117d70879fca2e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49814904"
---
# <a name="sharing-classes-between-dsls-by-using-a-dsl-library"></a>Compartilhando classes entre DSLs por meio de uma biblioteca de DSLs
No SDK de modelagem e visualização do Visual Studio, você pode criar uma definição de DSL incompleta que você pode importar para outra DSL. Isso permite fatorar partes comuns dos modelos semelhantes.

## <a name="creating-and-using-dsl-libraries"></a>Criando e usando bibliotecas de DSL

#### <a name="to-create-a-dsl-library"></a>Para criar uma biblioteca de DSL

1.  Criar um novo projeto DSL e escolher o modelo de solução de biblioteca de DSL.

     Um único projeto DSL será criado com um modelo vazio.

2.  Você pode adicionar classes de domínio, relações, formas e assim por diante.

     Os elementos na biblioteca não é necessário que formar uma única árvore de incorporação.

     Para definir uma relação de importadores podem usar, crie duas classes de domínio e criar a relação entre eles.

     Considere definir a **modificador de herança** das classes de domínio para `Abstract`.

3.  Você pode adicionar elementos que você define no DSL Explorer, como construtores de Conexão.

4.  Você pode adicionar as personalizações que requerem código adicional, como restrições de validação.

5.  Clique em **transformar todos os modelos**.

6.  Compile o projeto.

7.  Quando você distribui a DSL para que outras pessoas usem, você deve fornecer o assembly compilado (DLL) e o arquivo `DslDefinition.dsl`. Você pode encontrar o assembly compilado em uma pasta sob `Dsl\bin\*`

#### <a name="to-import-a-dsl-library"></a>Para importar uma biblioteca de DSL

1. Em outra definição de DSL, em **Gerenciador de DSL**, clique com botão direito a classe raiz do DSL e, em seguida, clique em **adicionar uma nova importação de DslLibrary**.

2. Na janela Propriedades, defina as **caminho do arquivo** da biblioteca. Você pode usar um caminho absoluto ou relativo.

    A biblioteca importada aparece no Gerenciador de DSL, no modo somente leitura.

3. Você pode usar as classes importadas como classes base. Criar uma classe de domínio na importação DSL e nas propriedades da janela, defina **base de dados de classe** para uma classe importada.

4. Clique em transformar todos os modelos.

5. Para o projeto DSL, adicione uma referência ao assembly (DLL) que foi criado pelo projeto de biblioteca de DSL.

6. Compile a solução.

   Uma biblioteca de DSL podem importar outras bibliotecas. Quando você importa uma biblioteca, suas importações automaticamente também aparecem no Gerenciador de DSL.

## <a name="see-also"></a>Consulte também

- [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
