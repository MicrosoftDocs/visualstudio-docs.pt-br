---
title: Como criar um esquema XML de um documento XML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 1d6700a9-fd67-4794-8997-399589e99bec
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2f33fc5b48b9fd6b1cc08570e62e73f05fd19e70
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34548267"
---
# <a name="how-to-create-an-xml-schema-from-an-xml-document"></a>Como: criar um esquema XML de um documento XML

O Editor de XML permite que você crie uma linguagem XSD (definição de esquema XML) de um documento XML. O documento de instância XML determina como o esquema é gerado da seguinte maneira:

-   Se o documento XML não tiver nenhum esquema ou DTD (definição de tipo de documento) associado a ele, os dados no documento XML serão usados para inferir um novo esquema XML.

-   Se o documento XML contiver um DTD associado, o DTD externo e o subconjunto interno serão convertidos em um esquema XML correspondente.

-   Se o documento XML contiver dados internos com um esquema XDR reduzido de dados XML, o esquema XDR será convertido em um esquema XML correspondente.

Os esquemas que são criados são, em seguida, usados para fornecer o IntelliSense para o documento XML.

Para obter mais informações sobre o mecanismo de inferência de esquema, consulte [inferindo um esquema XML](/dotnet/standard/data/xml/inferring-an-xml-schema).

## <a name="to-create-an-xml-schema"></a>Para criar um esquema XML

1.  Carregue um documento de instância XML no Editor de XML.

2.  Clique o **Create Schema** botão do **barra de ferramentas**.

     Um documento de esquema XML é criado e aberto para cada namespace encontrado no documento de instância XML. Cada esquema é aberto como um arquivo variado temporário.

     Os esquemas podem ser salvos no disco, adicionados ao seu projeto ou descartados.

    > [!NOTE]
    >  O **Create Schema** comando também está disponível no menu de atalho do Editor de XML e, sob o **XML** menu.

## <a name="see-also"></a>Consulte também

- [Editor de XML](../xml-tools/xml-editor.md)