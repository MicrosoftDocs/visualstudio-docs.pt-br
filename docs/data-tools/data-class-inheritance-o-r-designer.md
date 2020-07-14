---
title: Herança de classe de dados (Designer Relacional de Objetos)
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: af32653c-f4e6-4217-8c5a-e32b322b4918
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 7172c868780aec61de8688614fbb93627dc23bf5
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462389"
---
# <a name="data-class-inheritance-or-designer"></a>Herança de classe de dados (Designer Relacional de Objetos)

Assim como outros objetos, LINQ to SQL classes podem usar a herança e serem derivadas de outras classes. Em código, você pode especificar relações de herança entre objetos declarando uma classe que herda de outra. Em uma base de dados, as relações de herança são criadas de várias maneiras. O **Object Relational Designer** (**o/R Designer**) dá suporte ao conceito de herança de tabela única, pois ela geralmente é implementada em sistemas relacionais.

A herança de tabela única, há uma única tabela de base de dados que contém colunas para ambos base e classes derivadas. Com dados relacionais, uma coluna de discriminador contém o valor que determina qual classe qualquer determinado registro pertence. Por exemplo, considere uma `Persons` tabela que contém todos os empregados por uma empresa. Algumas pessoas são funcionários e algumas pessoas são gerentes. A `Persons` tabela contém uma coluna denominada `Type` que tem um valor de 1 para gerentes e um valor de 2 para funcionários. A `Type` coluna é a coluna discriminadora. Nesse cenário, você pode criar uma subclasse de Employees e preencher a classe somente com registros com um `Type` valor de 2.

Quando você configura a herança na classe entidade usando [!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)], arraste a única tabela que contém os dados de herança no designer duas vezes: uma vez para cada classe na hierarquia de herança. Após adicionar tabelas ao designer, conectar-las com um item de herança da caixa de ferramentas de **Object Relational Designer** e então defina as quatro propriedades de herança na janela **Propriedades**.

## <a name="inheritance-properties"></a>Propriedades de herança

A seguinte tabela lista as propriedades de herança e suas descrições:

|Propriedade|Descrição|
|--------------|-----------------|
|**Propriedade Discriminatória**|A propriedade (mapeado para a coluna) que determina qual classe ao registro atual pertence.|
|**Valor Discriminador de Classe Base**|O valor (na coluna designada como a **Propriedade discriminadora**) que determina que um registro é da classe base.|
|**Valor Discriminatório da Classe Derivada**|O valor (na propriedade designada como a **Propriedade discriminadora**) que determina que um registro é da classe derivada.|
|**Padrão de Herança**|A classe que é populada quando o valor na propriedade designada como a **Propriedade discriminadora** não corresponde ao **valor discriminador da classe base** ou ao **valor discriminador da classe derivada**.|

Criar um modelo de objeto que usar herança e corresponde a dados relacionais pode ser um pouco confuso. Este tópico fornece informações sobre os conceitos básicos e as propriedades individuais que são necessários configurando a herança. Os tópicos a seguir fornecem uma explicação mais clara de como configurar a herança com o o **/R Designer**.

|Tópico|Descrição|
|-----------|-----------------|
|[Como configurar a herança usando o Designer Relacional de Objetos](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)|Descreve como configurar classes de entidade que usam herança de tabela única usando o o **/R Designer**.|
|[Walkthrough: Criando classes de LINQ to SQL usando herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)|Fornece instruções passo a passo sobre como configurar classes de entidade que usam herança de tabela única usando o o **/R Designer**.|

## <a name="see-also"></a>Veja também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Passo a passo: criando classes LINQ to SQL (Designer Relacional de Objetos)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [Walkthrough: Criando classes de LINQ to SQL usando herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [Guia de Introdução](/dotnet/framework/data/adonet/sql/linq/getting-started)