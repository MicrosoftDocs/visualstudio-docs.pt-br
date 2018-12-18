---
title: Trechos XML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 348dbf64-3f09-4fff-b47a-a7ecdf3221cc
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 07ddb1dd64e5d972c23a032cb1eb752515d92ab6
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34693845"
---
# <a name="xml-snippets"></a>Trechos XML

O Editor de XML oferece um recurso chamado *trechos XML*, que permite que você crie arquivos XML mais rapidamente. Você pode reutilizar XML inserindo trechos nos seus arquivos. Você também pode gerar os dados XML com base no esquema de linguagem de definição de esquema XML (XSD).

## <a name="reusable-xml-snippets"></a>Trechos de código XML reutilizáveis

O editor XML inclui muitos trechos que abrangem algumas tarefas comuns. Isso permite que você crie arquivos XML mais facilmente. Por exemplo, se você estivesse criando um esquema XML, usando o elemento de sequência tipo complexo” e “os trechos do elemento tipo simples” inserir o seguinte texto XML para o arquivo. Você alteraria o valor de `name` para atender às suas necessidades.

```xml
<xs:element name="name">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="name">
        <xs:simpleType>
          <xs:restriction base="xs:string"></xs:restriction>
        </xs:simpleType>
      </xs:element>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

 Você pode inserir trechos de duas maneiras. O **Inserir trecho** comando insere o trecho XML na posição do cursor. O **Surround With** comando encapsula o trecho de código XML ao redor do texto selecionado. Os dois comandos estão disponíveis ou do **IntelliSense** submenu a **editar** menu, ou no menu de atalho do editor.

 Para obter mais informações, consulte [como: fragmentos XML de uso](../xml-tools/how-to-use-xml-snippets.md).

## <a name="schema-generated-xml-snippets"></a>Trechos de código gerado pelo esquema XML
 O editor XML também tem a capacidade de gerar um trecho de um esquema XML. Esse recurso permite que você popule um elemento com elementos XML gerados de informações de esquema para esse elemento.

 Para obter mais informações, consulte [como: gerar um fragmento de XML de um esquema XML](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md).

## <a name="create-new-xml-snippets"></a>Criar novos trechos XML
 Além de trechos de código que estão incluídos com [!INCLUDE[msCoName](../xml-tools/includes/msconame_md.md)] Visual Studio, por padrão, você também pode criar e usar seus próprios trechos de código XML.

 Para obter mais informações, consulte [como: fragmentos XML criar](../xml-tools/how-to-create-xml-snippets.md).

## <a name="see-also"></a>Consulte também

- [Editor de XML](../xml-tools/xml-editor.md)