---
title: Conjuntos de dados tipados versus. não tipados
description: Entenda a diferença entre conjuntos de valores digitados e não tipados. Contraste o acesso a dados em datasets digitados e não tipados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: daf4f722eb51a08e7a6ddb287e5b54956ecdfe73
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216014"
---
# <a name="typed-vs-untyped-datasets"></a>Conjuntos de dados tipados versus. não tipados
Um conjunto de dados tipado é um conjunto de dados que é derivado primeiro da <xref:System.Data.DataSet> classe base e, em seguida, usa informações do **Designer de conjunto de dados**, que é armazenado em um arquivo. xsd, para gerar uma nova classe de conjunto de dados com rigidez de tipos. As informações do esquema (tabelas, colunas e assim por diante) são geradas e compiladas nessa nova classe de conjunto de dados como um conjunto de objetos e propriedades de primeira classe. Como um conjunto de dados tipado herda da <xref:System.Data.DataSet> classe base, a classe tipada assume toda a funcionalidade da <xref:System.Data.DataSet> classe e pode ser usada com métodos que usam uma instância de uma <xref:System.Data.DataSet> classe como um parâmetro.

Um conjunto de um DataSet não tipado, por outro lado, não tem nenhum esquema interno correspondente. Como em um dataset tipado, um conjunto de um DataSet não tipado contém tabelas, colunas e assim por diante — mas eles são expostos apenas como coleções. (No entanto, depois que você criar manualmente as tabelas e outros elementos de dados em um DataSet não tipado, você poderá exportar a estrutura do DataSet como um esquema usando o método do conjunto de dados <xref:System.Data.DataSet.WriteXmlSchema%2A> .)

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>Contraste o acesso a dados em datasets digitados e não tipados
A classe de um conjunto de dados tipado tem um modelo de objeto no qual suas propriedades assumem os nomes reais das tabelas e colunas. Por exemplo, se você estiver trabalhando com um dataset tipado, poderá fazer referência a uma coluna usando um código como o seguinte:

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet4":::

Por outro lado, se você estiver trabalhando com um conjunto de um DataSet não tipado, o código equivalente será:

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet5":::

O acesso digitado não é apenas mais fácil de ler, mas também tem suporte completo do IntelliSense no **Editor de código** do Visual Studio. Além de ser mais fácil de trabalhar com, a sintaxe para o dataset tipado fornece verificação de tipo em tempo de compilação, reduzindo significativamente a possibilidade de erros na atribuição de valores a membros de conjuntos de de DataSet. Se você alterar o nome de uma coluna em sua <xref:System.Data.DataSet> classe e, em seguida, compilar seu aplicativo, receberá um erro de compilação. Ao clicar duas vezes no erro de compilação na **lista de tarefas**, você pode ir diretamente para a linha ou linhas de código que referenciam o nome de coluna antigo. O acesso a tabelas e colunas em um dataset tipado também é ligeiramente mais rápido no tempo de execução porque o acesso é determinado em tempo de compilação, não através de coleções em tempo de execução.

Mesmo que os conjuntos de linhas de texto tenham muitas vantagens, um conjunto de um DataSet não tipado é útil em várias circunstâncias. O cenário mais óbvio é quando nenhum esquema está disponível para o conjunto de um. Isso pode ocorrer, por exemplo, se seu aplicativo estiver interagindo com um componente que retorna um conjunto de dados, mas você não sabe com antecedência o que é sua estrutura. Da mesma forma, há ocasiões em que você está trabalhando com dados que não têm uma estrutura estática e previsível. Nesse caso, é impraticável usar um conjunto de dados tipado, pois você precisaria regenerar a classe DataSet tipada com cada alteração na estrutura de dado.

Em geral, há muitas vezes em que você pode criar um conjunto de um DataSet dinamicamente sem ter um esquema disponível. Nesse caso, o conjunto de dados é simplesmente uma estrutura conveniente na qual você pode manter informações, contanto que eles possam ser representados de forma relacional. Ao mesmo tempo, você pode aproveitar os recursos do conjunto de dados, como a capacidade de serializar as informações a serem passadas para outro processo ou para gravar um arquivo XML.

## <a name="see-also"></a>Confira também

- [Ferramentas de DataSet](../data-tools/dataset-tools-in-visual-studio.md)
