---
title: Examinar nós usando a exibição de modelo de conteúdo no designer de esquema XML
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c42ddac8-b0e3-48d6-9832-112a19d6c104
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 81bf6294aeac9a23168bf9cf9aaec26efbfc6c1f
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815975"
---
# <a name="how-to-examine-the-content-model-of-nodes-using-the-content-model-view"></a>Como examinar o modelo de conteúdo de nós usando a exibição do modelo de conteúdo

Este tópico descreve como explorar seus nós usando a [exibição de modelo de conteúdo](../xml-tools/content-model-view.md).

## <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>Para criar um novo arquivo XSD e exibir o elemento raiz no modo do modelo de conteúdo

1. Crie um novo arquivo de esquema XML.

2. Clique em **usar editor de XML para exibir e editar o arquivo de esquema XML subjacente** na exibição iniciar.

3. Copie o código de exemplo do esquema XML do [esquema XML de exemplo: ordem de compra esquema](../xml-tools/sample-xsd-file-purchase-order-schema.md) e cole-o para substituir o código que foi adicionado ao novo arquivo XSD por padrão.

4. Selecione o `purchaseOrder` elemento no Gerenciador de esquema clicando com o botão direito do mouse no `purchaseOrder` elemento no editor de XML e selecionando **Mostrar no Gerenciador de XML**.

5. Clique com o botão direito do mouse no `purchaseOrder` no Gerenciador de XML e selecione **Mostrar no modo de exibição de modelo de conteúdo**.

     A exibição do modelo de conteúdo exibe o elemento de `purchaseOrder` na superfície de design.

6. Expanda `shipTo`, `billTo`, e nós de `items` clicando duas vezes em cada nó ou double clicando na seta à direita de cada nó.

     Os nós de elemento de `purchaseOrder` são expandidos e agora você pode ver o modelo de conteúdo do elemento.

7. Clique em qualquer nó no elemento de `purchaseOrder` e examine a barra de rastreamento para ver onde o esquema define o nó selecionado for encontrado.

8. Clique no botão **Mostrar documentação** na barra de ferramentas XSD para alternar a documentação. Você também pode clicar com o botão direito do mouse na superfície de design para ativar /desativar a documentação.

9. Clique com o botão direito do mouse no `purchaseOrder` nó e selecione **gerar XML de exemplo** para ver o documento de instância XML.
