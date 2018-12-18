---
title: 'Como: configurar a herança usando o Object Relational Designer'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: bb0be89627f5e7e95d7d45ebfb938bca3e4a982b
ms.sourcegitcommit: e9d1018a01af62c3dc5aeb6b325faba7e20bd496
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37089258"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>Como: configurar a herança usando o Designer relacional de objetos
O **Object Relational Designer** (**Relational Designer**) suporta o conceito de herança de tabela única como geralmente é implementado em sistemas relacionais. Herança de tabela única, há uma tabela de banco de dados individual que contém campos para informações pai e informações de filho. Com dados relacionais, uma coluna de discriminador contém o valor que determina qual classe qualquer registro pertence.

Por exemplo, considere um `Persons` tabela que contém todos empregado por uma empresa. Algumas pessoas são funcionários e algumas pessoas são gerentes. O `Persons` tabela contém uma coluna denominada `EmployeeType` que tem um valor de 1 para gerentes e um valor de 2 para funcionários; esta é a coluna de discriminador. Nesse cenário, você pode criar uma subclasse de funcionários e preencher a classe com apenas os registros que têm um valor de `EmployeeType` de 2. Você pode também remover colunas que não se aplicam de cada uma das classes.

Criar um modelo de objeto que usar herança (e corresponde a dados relacionais) pode ser um pouco confuso. O procedimento a seguir descreve as etapas necessárias para configurar a herança com o **Relational Designer**. As seguintes etapas genéricas sem se referir a uma tabela existente e colunas podem ser difícil, portanto, um passo a passo que usa dados é fornecida. Para instruções passo a passo detalhadas para configurar a herança usando o **Relational Designer**, consulte [passo a passo: Criando o LINQ to SQL classes por meio de herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md).

## <a name="to-create-inherited-data-classes"></a>Para criar classes de dados herdadas

1.  Abra o **Relational Designer** adicionando um **Classes LINQ to SQL** item a um projeto existente do Visual Basic ou c#.

2.  Arraste a tabela que você deseja usar como a classe base para o **Relational Designer**.

3.  Arraste uma segunda cópia da tabela para o **Relational Designer** e renomeá-lo. Esta é a classe derivada, ou subclasse.

4.  Clique em **herança** no **Object Relational Designer** guia o **caixa de ferramentas**e, em seguida, clique na subclasse (a tabela que você renomeou) e conectá-lo para a classe base.

    > [!NOTE]
    >  Clique o **herança** item o **caixa de ferramentas** e solte o botão do mouse, clique na segunda cópia da classe que você criou na etapa 3 e, em seguida, clique na primeira classe que você criou na etapa 2. A seta na linha de herança aponta para a primeira classe.

5.  Em cada classe, excluir todas as propriedades do objeto que você não deseja que apareça e que não são usadas para associações. Você receberá um erro se você tentar excluir as propriedades do objeto usadas para associações: [a propriedade \<nome da propriedade > não pode ser excluída porque participa da associação \<nome da associação >](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md).

    > [!NOTE]
    >  Como uma classe derivada herda as propriedades definidas na sua classe base, as mesmas colunas não podem ser definidas em cada classe. (As colunas são implementadas como propriedades.) Você pode habilitar a criação de colunas na classe derivada, definindo o modificador de herança na propriedade na classe base. Para obter mais informações, consulte [Noções básicas de herança (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics).

6.  Selecione a linha de herança na **Relational Designer**.

7.  No **propriedades** janela, defina as **propriedade discriminatória** ao nome da coluna que distingue os registros em suas classes.

8.  Defina as **valor Discriminatório da classe derivada** propriedade para o valor no banco de dados que designa o registro como o tipo herdado. (Esse é o valor que é armazenado na coluna de discriminador e é usado para designar a classe herdada.)

9. Defina as **valor Discriminatório da classe Base** propriedade para o valor que designa o registro como um tipo base. (Esse é o valor que é armazenado na coluna de discriminador e é usado para designar a classe base.)

10. Opcionalmente, você também pode definir as **padrão de herança** propriedade para designar um tipo em uma hierarquia de herança usado ao carregar as linhas que não correspondam a qualquer código de herança definido. Em outras palavras, se um registro tem um valor na coluna de discriminador que não coincide com o valor em qualquer um de **valor Discriminatório da classe derivada** ou **valor Discriminatório da classe Base** propriedades, o registro carrega no tipo designado como o **padrão de herança**.

## <a name="see-also"></a>Consulte também

- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Passo a passo: Criando o LINQ para SQL classes (Object Relational Designer)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Passo a passo: Criando o LINQ para classes SQL usando a herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [Noções básicas de herança (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [Herança](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)