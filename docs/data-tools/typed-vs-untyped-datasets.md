---
title: Conjuntos de dados tipados versus. não tipados
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: d817938a7611d7390e400cfbf69c6836b9256f3b
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37117219"
---
# <a name="typed-vs-untyped-datasets"></a>Conjuntos de dados tipados versus. não tipados
Um dataset tipado é um conjunto de dados pela primeira vez é derivado da base <xref:System.Data.DataSet> de classe e, em seguida, usa as informações do **Dataset Designer**, que é armazenado em um arquivo. xsd, para gerar um novo, fortemente tipadas classe dataset. Informações do esquema (tabelas, colunas e assim por diante) são geradas e compiladas essa nova classe de conjunto de dados como um conjunto de objetos de primeira classe e propriedades. Como um conjunto de dados tipado herda da base <xref:System.Data.DataSet> classe, a classe tipada pressupõe que todas as funcionalidades do <xref:System.Data.DataSet> classe e pode ser usado com métodos que usam uma instância de um <xref:System.Data.DataSet> classe como um parâmetro.

 Um conjunto de dados não tipado, por outro lado, não tem nenhum esquema interna correspondente. Como em um dataset tipado, um conjunto de dados não tipado contém tabelas, colunas e assim por diante —, mas esses são expostos apenas como coleções. (No entanto, depois que você cria manualmente as tabelas e outros elementos de dados em um conjunto de dados não tipado, você pode exportar estrutura do conjunto de dados como um esquema usando o conjunto de dados <xref:System.Data.DataSet.WriteXmlSchema%2A> método.)

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>Acesso a dados em conjuntos de dados tipados e contraste
 A classe para um dataset tipado tem um modelo de objeto no qual suas propriedades assumir os nomes reais das tabelas e colunas. Por exemplo, se você estiver trabalhando com um dataset tipado, você pode fazer referência a uma coluna usando código como o seguinte:

 [!code-csharp[VbRaddataDatasets#4](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_1.cs)]
 [!code-vb[VbRaddataDatasets#4](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_1.vb)]

 Por outro lado, se você estiver trabalhando com um conjunto de dados não tipado, o código equivalente é:

 [!code-csharp[VbRaddataDatasets#5](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_2.cs)]
 [!code-vb[VbRaddataDatasets#5](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_2.vb)]

 Acesso de tipo não é apenas mais fácil de ler, mas também com suporte completo pelo IntelliSense no Visual Studio **Editor de códigos**. Além de ser mais fácil trabalhar com, a sintaxe para o conjunto de dados tipado fornece verificação de tipo em tempo de compilação, reduzindo significativamente a possibilidade de erros em atribuir valores aos membros do conjunto de dados. Se você alterar o nome de uma coluna em sua <xref:System.Data.DataSet> de classe e, em seguida, compile o aplicativo, você receberá um erro de compilação. Clicando duas vezes no erro na compilação a **lista de tarefas**, você pode ir diretamente para a linha ou linhas de código que faça referência ao nome de coluna antiga. Acesso a tabelas e colunas em um conjunto de dados também é ligeiramente mais rápido em tempo de execução porque o acesso é determinado em tempo de compilação, não por meio de coleções em tempo de execução.

 Embora os conjuntos de dados tipados têm muitas vantagens, um conjunto de dados não tipado é útil em uma variedade de circunstâncias. O cenário mais óbvio é quando nenhum esquema está disponível para o conjunto de dados. Isso pode ocorrer, por exemplo, se seu aplicativo está interagindo com um componente que retorna um conjunto de dados, mas você não souber de antemão qual é sua estrutura. Da mesma forma, há vezes quando você estiver trabalhando com dados que não tem uma estrutura estática e previsível. Nesse caso, é impraticável para usar um dataset tipado, porque você precisará regenerar a classe de conjunto de dados tipado com cada alteração na estrutura de dados.

 De modo geral, há muitas vezes quando você pode criar um conjunto de dados dinamicamente sem a necessidade de um esquema estão disponíveis. Nesse caso, o conjunto de dados é simplesmente uma estrutura conveniente no qual você pode manter informações, desde que os dados podem ser representados de forma relacional. Ao mesmo tempo, você pode tirar proveito dos recursos do conjunto de dados, como a capacidade de serializar as informações para passar para outro processo ou para gravar um arquivo XML.

## <a name="see-also"></a>Consulte também

- [Ferramentas do conjunto de dados](../data-tools/dataset-tools-in-visual-studio.md)