---
title: Como configurar a herança usando o Designer Relacional de Objetos
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e31e5e78d5c72167f9d1c1eaab974155a4c369f3
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282235"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>Como configurar a herança usando o Designer Relacional de Objetos
O **Object Relational Designer** (**o/R Designer**) dá suporte ao conceito de herança de tabela única, pois ela geralmente é implementada em sistemas relacionais. Na herança de tabela única, há uma única tabela de banco de dados que contém campos para informações pai e informações filho. Com os dados relacionais, uma coluna de discriminador contém o valor que determina qual classe qualquer registro pertence.

Por exemplo, considere uma `Persons` tabela que contém todos os empregados por uma empresa. Algumas pessoas são funcionários e algumas pessoas são gerentes. A `Persons` tabela contém uma coluna denominada `EmployeeType` que tem um valor de 1 para gerentes e um valor de 2 para funcionários; esta é a coluna discriminadora. Nesse cenário, você pode criar uma subclasse de funcionários e preencher a classe com apenas os registros que têm um valor de `EmployeeType` de 2. Você pode também remover colunas que não se aplicam de cada uma das classes.

Criar um modelo de objeto que usar herança (e corresponde a dados relacionais) pode ser um pouco confuso. O procedimento a seguir descreve as etapas necessárias para configurar a herança com o o **/R Designer**. As etapas genéricas a seguir sem referir-se a uma tabela e colunas existentes podem ser difíceis, portanto, um passo a passos que usa dados é fornecido. Para instruções passo a passo detalhadas para configurar a herança usando o **Relational Designer**, consulte [passo a passo: Criando o LINQ to SQL classes por meio de herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md).

## <a name="to-create-inherited-data-classes"></a>Para criar classes de dados herdadas

1. Abra o o **/R Designer** adicionando um item de **classes de LINQ to SQL** a um projeto existente Visual Basic ou C#.

2. Arraste a tabela que você deseja usar como a classe base para o o **/R Designer**.

3. Arraste uma segunda cópia da tabela para o o **/R Designer** e renomeie-a. Esta é a classe derivada, ou subclasse.

4. Clique na guia **Herança** no **Object Relational Designer** da **Caixa de Ferramentas** e em seguida, clique na subclasse (a tabela que você renomeou) e conecta-se a classe base.

    > [!NOTE]
    > Clique no item de **Herança** em **Caixa de Ferramentas** e solte o botão do mouse, clique na segunda cópia de classe que você criou na etapa 3 e depois clique na primeira classe que você criou na etapa 2. A seta na linha de herança aponta para a primeira classe.

5. Em cada classe, excluir todas as propriedades do objeto que você não deseja que apareça e que não são usadas para associações. Você receberá um erro se tentar excluir as propriedades de objeto usadas para associações: [a propriedade \<property name> não pode ser excluída porque está participando \<association name> da Associação ](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md).

    > [!NOTE]
    > Como uma classe derivada herda as propriedades definidas na sua classe base, as mesmas colunas não podem ser definidas em cada classe. (As colunas são implementadas como propriedades.) Você pode habilitar a criação de colunas na classe derivada definindo o modificador de herança na propriedade na classe base. Para obter mais informações, consulte [noções básicas de herança (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics).

6. Selecione a linha de herança no **designer o/R**.

7. Na janela **Propriedades** , defina a **Propriedade discriminador** como o nome da coluna que distingue os registros em suas classes.

8. Defina a propriedade **Valor Discriminatório da Classe Derivada** para o valor no banco de dados que designa o registro como o tipo herdado. (Esse é o valor que é armazenado na coluna discriminador e é usado para designar a classe herdada.)

9. Defina a propriedade **valor do discriminador de classe base** como o valor que designa o registro como um tipo base. (Esse é o valor que é armazenado na coluna discriminador e é usado para designar a classe base.)

10. Opcionalmente, você pode também definir a propriedade de **Padrão de Herança** para designar um tipo em uma hierarquia de herança que é usada para carregar as linhas que não correspondem nenhum código de herança definido. Em outras palavras, se um registro tiver um valor em sua coluna discriminadora que não corresponda ao valor no **valor discriminador da classe derivada** ou nas propriedades do **valor discriminador da classe base** , o registro será carregado no tipo designado como **padrão de herança**.

## <a name="see-also"></a>Veja também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Passo a passo: criando classes LINQ to SQL (Designer Relacional de Objetos)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Walkthrough: Criando classes de LINQ to SQL usando herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [Noções básicas de herança (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [Herança](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
