---
title: 'Como: criar um documento XML com base em um esquema XSD | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 193b195f-e918-4c79-a1a1-8096a1433bde
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: bbecacc0729c936489c05d3bb59260341a08d314
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49884219"
---
# <a name="how-to-create-an-xml-document-based-on-an-xsd-schema"></a>Como criar um documento XML baseado em um esquema XSD
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O **gerar XML de exemplo** recurso gera um arquivo XML de exemplo com base em seu arquivo de esquema XML (XSD).  
  
 Você pode usar esta opção para os seguintes situações:  
  
- Para entender o uso de várias construções no seu esquema.  
  
- Para confirmar que o esquema faz o que é esperado dele.  
  
  O **gerar XML de exemplo** recurso só está disponível nos elementos globais e requer um conjunto de esquema XML válido.  
  
  Esse recurso normalmente gera documentos XML válidos. No entanto, se o esquema contiver um ou mais dos seguintes, o exemplo poderá não ser válido:  
  
- As restrições de identidade `xs:key`, `xs:keyref` e `xs:unique`.  
  
- `xs:pattern` facetas.  
  
- Enumerações do tipo `xs:QName`.  
  
- Tipos `xs:ENTITY`, `xs:ENTITIES` e `xs:NOTATION`.  
  
  Além disso, observe que o conteúdo de `xs:base64Binary` será gerado apenas se as enumerações ocorrerem no esquema para esse tipo.  
  
### <a name="to-generate-an-xml-instance-document-based-on-the-xsd-file"></a>Para gerar um documento de instância XML baseado no arquivo XSD  
  
1.  Siga as etapas em [como: criar e editar um arquivo de esquema XSD](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md).  
  
2.  No [XML Schema Explorer](../xml-tools/xml-schema-explorer.md), clique com botão direito do `PurchaseOrder` elemento global. Selecione **gerar XML de exemplo**.  
  
     Quando você selecionar essa opção, o arquivo PurchaseOrder.xml com o conteúdo XML de exemplo a seguir será gerado e aberto no Editor de XML:  
  
    ```  
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
 [Trabalhando com os dados XML](../xml-tools/working-with-xml-data.md)



