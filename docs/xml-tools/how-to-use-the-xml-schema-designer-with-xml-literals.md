---
title: 'Como: Usar o designer de esquema XML com literais XML'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: 3883b4515ab304e2a247414f63c79db6314a654c
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54922072"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>Como: Use o Designer de esquema XML com literais XML

Este tópico descreve como exibir um esquema associado com um literal XML em um projeto Visual Basic.

## <a name="to-create-a-new-visual-basic-console-application-project"></a>Para criar um novo projeto de aplicativo de console do Visual Basic

1.  Inicie o Visual Studio.

2.  Dos **arquivo** menu, selecione **New**e, em seguida, selecione **projeto**. A caixa de diálogo **Novo Projeto** é exibida. Para **tipos de projeto**, selecione **outras linguagens,** e, em seguida, selecione **Visual Basic**. Para **modelos**, selecione o aplicativo de Console. Em seguida, digite `XMLLiterals` no **nome** campo e um local do projeto na **local** campo. Clique em **OK**.

     O novo poject é criado. O projeto de XMLLiterals contém um arquivo de origem do Visual Basic, *Module1.vb*.

## <a name="to-add-an-existing-xsd-file-to-the-project"></a>Para adicionar um arquivo XSD existente ao projeto

1.  Abra um novo arquivo de texto no bloco de notas. Copie o código de exemplo de esquema XML do [esquema de ordem de compra](../xml-tools/sample-xsd-file-simple-schema.md) e cole-a para o arquivo.

2.  Salve o arquivo em algum local com o nome *Purchaseorderschema*.

3.  Na **Gerenciador de soluções**, o nome do projeto com o botão direito, selecione **Add**e, em seguida, selecione **Item existente**. O **AddExisting Item** caixa de diálogo é exibida. Navegue até a *Purchaseorderschema* do arquivo, selecione-o e, em seguida, clique em **Add**.

     O projeto de XMLLiterals agora contém dois arquivos: *Module1.vb* e *Purchaseorderschema*.

## <a name="to-add-visual-basic-code-with-an-xml-literal-based-on-the-xsd-file-included-in-the-project"></a>Para adicionar código Visual Basic com uma literal XML, com base no arquivo XSD incluído no projeto

1. Substitua o código em *Module1.vb* arquivo pelo código a seguir:

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

2. Qualquer nó XML em um literal XML ou uma importação de namespace XML com o botão direito e selecione **Mostrar no Schema Explorer**.

    O **XML Schema Explorer** é exibido lado a lado com um arquivo de Visual Basic que possui o literal XML associado com o conjunto de esquema XML.