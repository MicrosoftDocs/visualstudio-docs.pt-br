---
title: 'Como: Use o designer de esquema XML com literais XML'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: b515092087ab213db5d3002f00c56753c2e3de14
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814636"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>Como: usar o designer de esquema XML com literais XML

Este tópico descreve como exibir um esquema associado com um literal XML em um projeto Visual Basic.

## <a name="create-a-new-visual-basic-project"></a>Criar um novo projeto de Visual Basic

1. Abra o Visual Studio.

2. Crie um novo projeto de **aplicativo de Console** Visual Basic chamado **xmlliterais**.

     O novo projeto contém um arquivo de origem Visual Basic, *Module1. vb*.

## <a name="add-an-existing-xsd-file"></a>Adicionar um arquivo XSD existente

1. Abra um novo arquivo de texto no bloco de notas. Copie o código de exemplo do esquema XML do [esquema da ordem de compra](../xml-tools/sample-xsd-file-simple-schema.md) e cole-o no arquivo.

2. Salve o arquivo em algum local com o nome *PurchaseOrderSchema. xsd*.

3. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nome do projeto, selecione **Adicionar**e, em seguida, selecione **Item existente**. A caixa de diálogo de **Item Addexisting** é exibida. Navegue até o arquivo *PurchaseOrderSchema. xsd* , selecione-o e clique em **Adicionar**.

     O projeto xmlliterais agora contém dois arquivos: *Module1. vb* e *PurchaseOrderSchema. xsd*.

## <a name="add-code"></a>Incluir código

Para adicionar Visual Basic código com um literal XML, com base no arquivo XSD incluído no projeto:

1. Substitua o código no arquivo *Module1. vb* pelo seguinte código:

   ```vb
   Imports <xmlns:ns="http://tempuri.org/PurchaseOrderSchema.xsd">

   Module Module1
      Sub Main()

          Dim XMLLiteral = <ns:PurchaseOrder OrderDate="1900-01-01">
                               <ns:ShipTo country="US">
                                   <ns:name>name1</ns:name>
                                   <ns:street>street1</ns:street>
                                   <ns:city>city1</ns:city>
                                   <ns:state>state1</ns:state>
                                   <ns:zip>1</ns:zip>
                               </ns:ShipTo>
                               <ns:BillTo country="US">
                                   <ns:name>name1</ns:name>
                                   <ns:street>street1</ns:street>
                                   <ns:city>city1</ns:city>
                                   <ns:state>state1</ns:state>
                                   <ns:zip>1</ns:zip>
                               </ns:BillTo>
                           </ns:PurchaseOrder>

      End Sub
   End Module
   ```

2. Clique com o botão direito do mouse em qualquer nó XML em um literal XML ou em uma importação de namespace XML e selecione **Mostrar no Gerenciador de esquema**.

   O **XML Schema Explorer** é exibido lado a lado com um arquivo Visual Basic que tem o literal XML associado ao conjunto de esquema XML.
