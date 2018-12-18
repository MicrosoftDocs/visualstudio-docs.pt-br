---
title: 'Como: Gerencia um trecho de um esquema XML'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 2c128d2a-aaa6-4814-aa95-e07056afe338
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0ac437bbbe876d81acc917f011a3051c9c264b6a
ms.sourcegitcommit: d1824ab926ebbc4a8057163e0edeaf35cec57433
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/24/2018
ms.locfileid: "34477672"
---
# <a name="how-to-generate-an-xml-snippet-from-an-xml-schema"></a>Como: gerar um fragmento de XML de um esquema XML

O editor XML tem a capacidade de gerar trechos de um esquema de linguagem de definição de esquema XML (XSD). Por exemplo, como criar um arquivo XML, enquanto posicionado ao lado do nome do elemento, você pode pressionar **guia** para preencher o elemento com dados XML gerados a partir das informações de esquema para esse elemento.

Este recurso está disponível somente nos elementos. As seguintes regras também se aplicam:

-   O elemento deve ter um tipo associado de esquema; isto é, o elemento deve ser válido de acordo com qualquer esquema associado. O tipo de esquema não pode ser abstract e o tipo deve conter os atributos necessários e/ou os elementos filho necessários.

-   O elemento atual no editor deve ser deixado sem atributos. Por exemplo, todos os seguintes são válidos

    -   `<Account`

    -   `<Account>`

    -   `<Account></Account>`

-   O cursor deve ser localizado imediatamente à direita do nome do elemento.

O trecho gerado contém todos os atributos e elementos necessários. Se `minOccurs` é maior de um, o número mínimo necessário de instâncias desse elemento é incluído no trecho de código, até um máximo de 100 instâncias. Todos os valores fixos encontrados no esquema levam a valores fixos no trecho. `xsd:any` e elementos de `xsd:anyAttribute` são ignorados e resultado nas compilações adicionais de trecho.

Os valores padrão são gerados e observados como valores editáveis. Se o esquema especifica um valor padrão, esse valor padrão é usado. Entretanto, se o valor padrão de esquema é uma cadeia de caracteres vazia, o editor gerencia os valores padrão da seguinte maneira:

-   Se o tipo de esquema contém quaisquer facetas de enumeração, direta ou indiretamente por meio de alguns dos membros de um tipo de união, o primeiro valor enumerado encontrado no modelo de objeto de esquema é usado como o padrão.

-   Se o tipo de esquema é um tipo atômico, o editor obtém o tipo atômico e insere o nome atômico de tipo. Para um tipo derivado simples usa o tipo simples base. Para um tipo de lista o tipo atômico é `itemType`. Para uma união atômico, o tipo é o tipo atômico de primeiro `memberType`.

## <a name="example"></a>Exemplo

 As etapas nesta seção mostram como usar o recurso de trecho de código do XML de esquema gerado do Editor de XML.

> [!NOTE]
> Antes de iniciar estes procedimentos, salve o arquivo de esquema para o seu computador local.

### <a name="to-create-a-new-xml-file-and-associate-it-with-an-xml-schema"></a>Para criar um novo arquivo XML e associá-lo a um esquema XML

1.  Sobre o **arquivo** , aponte para **novo**e clique em **arquivo**.

2.  Selecione **arquivo XML** no **modelos** painel e clique em **abrir**.

     Um novo arquivo é aberto no editor. O arquivo contém uma declaração XML padrão, `<?xml version="1.0" encoding="utf-8">`.

3.  Na janela de propriedades do documento, clique no botão Procurar (**...** ) sobre o **esquemas** campo.

     O **esquemas XSD** caixa de diálogo é exibida.

4.  Clique em **Adicionar**.

     O **esquema XSD aberto** caixa de diálogo é exibida.

5.  Selecione o arquivo de esquema e clique em **abrir**.

6.  Clique em **OK**.

     O esquema XML agora está associada ao documento XML.

### <a name="to-generate-an-xml-snippet"></a>Para gerar um trecho XML

1.  Tipo `<` no painel do editor.

2.  A lista de membros exibe os itens possíveis:

     **!-** para adicionar um comentário.

     **! DOCTYPE** para adicionar um tipo de documento.

     **?** Para adicionar uma instrução de processamento.

     **Entre em contato com** para adicionar o elemento raiz.

3.  Selecione **contato** na lista de membros e pressione **Enter**.

     O editor adiciona a tag de início `<Contact` e posicionar o cursor após o nome do elemento.

4.  Pressione **guia** para gerar dados XML para o `Contact` elemento com base em suas informações de esquema.

## <a name="input"></a>Entrada

 O seguinte arquivo de esquema é usado por passo a passo.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema elementFormDefault="qualified"
           xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:simpleType name="phoneType">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Voice"/>
      <xs:enumeration value="Fax"/>
      <xs:enumeration value="Pager"/>
    </xs:restriction>
  </xs:simpleType>
  <xs:element name="Contact">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Name">
          <xs:simpleType>
            <xs:restriction base="xs:string"></xs:restriction>
          </xs:simpleType>
        </xs:element>
        <xs:element name="Title"
                    type="xs:string" />
        <xs:element name="Phone"
                    minOccurs="1"
                    maxOccurs="unbounded">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="Number"
                          minOccurs="1">
                <xs:simpleType>
                  <xs:restriction base="xs:string"></xs:restriction>
                </xs:simpleType>
              </xs:element>
              <xs:element name="Type"
                          default="Voice"
                          minOccurs="1"
                          type="phoneType"/>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

### <a name="output"></a>Saída

 A seguir estão os dados XML que são gerados com base nas informações de esquema associada com o elemento de `Contact` . Os itens marcados como `bold` designar campos editáveis no trecho de XML.

```xml
<Contact>
  <Name>name</Name>
  <Title>title</Title>
  <Phone>
    <Number>number</Number>
    <Type>Voice</Type>
  </Phone>
</Contact>
```

## <a name="see-also"></a>Consulte também

- [Trechos XML](../xml-tools/xml-snippets.md)
- [Como: usar XML trechos de código](../xml-tools/how-to-use-xml-snippets.md)