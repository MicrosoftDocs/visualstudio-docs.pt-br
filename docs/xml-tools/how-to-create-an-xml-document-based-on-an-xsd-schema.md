---
title: Como criar um documento XML baseado em um esquema XSD
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 193b195f-e918-4c79-a1a1-8096a1433bde
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6d3da2e6b5b0c9ea2701524c0fb2fde1e1313687
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34549084"
---
# <a name="how-to-create-an-xml-document-based-on-an-xsd-schema"></a>Como: criar um documento XML com base em um esquema XSD

O **gerar XML de exemplo** recurso gera um arquivo XML de exemplo com base em seu arquivo de esquema XML (XSD).

 Você pode usar esta opção para os seguintes situações:

-   Para entender o uso de várias construções no seu esquema.

-   Para confirmar que o esquema faz o que é esperado dele.

O **gerar XML de exemplo** recurso está disponível somente em elementos globais e requer um conjunto de esquema XML válido.

Esse recurso normalmente gera documentos XML válidos. No entanto, se o esquema contiver um ou mais dos seguintes, o exemplo poderá não ser válido:

-   As restrições de identidade `xs:key`, `xs:keyref` e `xs:unique`.

-   `xs:pattern` facetas.

-   Enumerações do tipo `xs:QName`.

-   Tipos `xs:ENTITY`, `xs:ENTITIES` e `xs:NOTATION`.

Além disso, observe que o conteúdo de `xs:base64Binary` será gerado apenas se as enumerações ocorrerem no esquema para esse tipo.

## <a name="to-generate-an-xml-instance-document-based-on-the-xsd-file"></a>Para gerar um documento de instância XML baseado no arquivo XSD

1.  Siga as etapas em [como: criar e editar um arquivo de esquema XSD](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md).

2.  No [XML Schema Explorer](../xml-tools/xml-schema-explorer.md), com o botão direito do `PurchaseOrder` elemento global. Selecione **gerar XML de exemplo**.

     Quando você seleciona essa opção, PurchaseOrder. *xml* arquivo com o conteúdo XML de exemplo a seguir será gerado e aberto no Editor de XML:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <PurchaseOrder OrderDate="1900-01-01" xmlns="http://tempuri.org/PurchaseOrderSchema.xsd">
      <ShipTo country="US">
        <name>name1</name>
        <street>street1</street>
        <city>city1</city>
        <state>state1</state>
        <zip>1</zip>
      </ShipTo>
      <ShipTo country="US">
        <name>name2</name>
        <street>street2</street>
        <city>city2</city>
        <state>state2</state>
        <zip>-79228162514264337593543950335</zip>
      </ShipTo>
      <BillTo country="US">
        <name>name1</name>
        <street>street1</street>
        <city>city1</city>
        <state>state1</state>
        <zip>1</zip>
      </BillTo>
    </PurchaseOrder>
    ```

## <a name="see-also"></a>Consulte também

- [Trabalhando com dados XML](../xml-tools/working-with-xml-data.md)