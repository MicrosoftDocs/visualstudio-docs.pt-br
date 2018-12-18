---
title: Herança de classe de dados (Object Relational Designer)
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: af32653c-f4e6-4217-8c5a-e32b322b4918
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 6c6b17ad38e9aae78975e43797931a326955712d
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36756731"
---
# <a name="data-class-inheritance-or-designer"></a>Herança de classe de dados (O/R Designer)

Como outros objetos, classes LINQ to SQL pode usar a herança e ser derivado de outras classes. Em código, você pode especificar relações de herança entre objetos declarando uma classe que herda de outra. Em uma base de dados, as relações de herança são criadas de várias maneiras. O **Object Relational Designer** (**Relational Designer**) suporta o conceito de herança de tabela única como geralmente é implementado em sistemas relacionais.

A herança de tabela única, há uma única tabela de base de dados que contém colunas para ambos base e classes derivadas. Com dados relacionais, uma coluna de discriminador contém o valor que determina qual classe qualquer determinado registro pertence. Por exemplo, considere um `Persons` tabela que contém todos empregado por uma empresa. Algumas pessoas são funcionários e algumas pessoas são gerentes. O `Persons` tabela contém uma coluna denominada `Type` que tem um valor de 1 para gerentes e um valor de 2 para funcionários. O `Type` coluna é a coluna de discriminador. Nesse cenário, você pode criar uma subclasse de funcionários e preencher a classe com apenas os registros que têm um `Type` valor 2.

Quando você configura a herança em classes de entidade usando o [!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)], arraste a única tabela que contém os dados de herança para o designer duas vezes: uma vez para cada classe na hierarquia de herança. Depois de adicionar as tabelas ao designer, conectá-los com um item de herança dos **Object Relational Designer** da caixa de ferramentas e, em seguida, defina as quatro propriedades de herança na **propriedades** janela.

## <a name="inheritance-properties"></a>Propriedades de herança

A seguinte tabela lista as propriedades de herança e suas descrições:

|Propriedade|Descrição|
|--------------|-----------------|
|**Propriedade discriminatória**|A propriedade (mapeado para a coluna) que determina qual classe ao registro atual pertence.|
|**Valor Discriminatório da classe base**|O valor (na coluna designada como o **propriedade discriminatória**) que determina que um registro é a classe base.|
|**Valor Discriminatório da classe derivada**|O valor (na propriedade designada como o **propriedade discriminatória**) que determina que um registro é da classe derivada.|
|**Padrão de herança**|A classe que é preenchida quando o valor na propriedade designada como o **propriedade discriminatória** não corresponder a **valor Discriminatório da classe Base** ou o **classe derivada Valor Discriminatório**.|

Criar um modelo de objeto que usar herança e corresponde a dados relacionais pode ser um pouco confuso. Este tópico fornece informações sobre os conceitos básicos e as propriedades individuais que são necessários configurando a herança. Os tópicos a seguir fornecem uma explicação mais claro de como configurar a herança com o **Relational Designer**.

|Tópico|Descrição|
|-----------|-----------------|
|[Como: configurar a herança usando o Designer relacional de objetos](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)|Descreve como configurar classes de entidade que usam herança de tabela única usando o **Relational Designer**.|
|[Passo a passo: Criando o LINQ para classes SQL usando a herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)|Fornece instruções passo a passo sobre como configurar classes de entidade que usam herança de tabela única usando o **Relational Designer**.|

## <a name="see-also"></a>Consulte também

- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Passo a passo: Criando o LINQ para SQL classes (Object Relational Designer)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [Passo a passo: Criando o LINQ para classes SQL usando a herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [Introdução](/dotnet/framework/data/adonet/sql/linq/getting-started)