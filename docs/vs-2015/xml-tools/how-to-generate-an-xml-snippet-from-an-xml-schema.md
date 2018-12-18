---
title: 'Como: gerar um trecho XML a partir de um esquema XML | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2c128d2a-aaa6-4814-aa95-e07056afe338
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 6eb03fba400e20227155a2528b8aaf0b28f7761a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951464"
---
# <a name="how-to-generate-an-xml-snippet-from-an-xml-schema"></a>Como: Gerencia um snippet de um esquema XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O editor XML tem a capacidade de gerar snippets de um esquema de linguagem de definição de esquema XML (XSD). Por exemplo, porque você está criando um arquivo XML, quando posicionado próximo ao nome do elemento, você pode pressionar a tecla TAB para preencher o elemento com os dados XML gerados de informações de esquema para esse elemento.  
  
 Este recurso está disponível somente nos elementos. As seguintes regras também se aplicam:  
  
- O elemento deve ter um tipo associado de esquema; isto é, o elemento deve ser válido de acordo com qualquer esquema associado. O tipo de esquema não pode ser abstract e o tipo deve conter os atributos necessários e/ou os elementos filho necessários.  
  
- O elemento atual no editor deve ser deixado sem atributos. Por exemplo, todos os seguintes são válidos  
  
  -   `<Account`  
  
  -   `<Account>`  
  
  -   `<Account></Account>`  
  
- O cursor deve ser localizado imediatamente à direita do nome do elemento.  
  
  O snippet gerado contém todos os atributos e elementos necessários. Se `minOccurs` é maior de um, o número mínimo necessário de instâncias desse elemento é incluído no snippet, até um máximo de 100 instâncias. Todos os valores fixos encontrados no esquema levam a valores fixos no snippet. `xsd:any` e elementos de `xsd:anyAttribute` são ignorados e resultado nas compilações adicionais de trecho.  
  
  Os valores padrão são gerados e observados como valores editáveis. Se o esquema especifica um valor padrão, esse valor padrão é usado. Entretanto, se o valor padrão de esquema é uma cadeia de caracteres vazia, o editor gerencia os valores padrão da seguinte maneira:  
  
- Se o tipo de esquema contém quaisquer facetas de enumeração, direta ou indiretamente por meio de alguns dos membros de um tipo de união, o primeiro valor enumerado encontrado no modelo de objeto de esquema é usado como o padrão.  
  
- Se o tipo de esquema é um tipo atômico, o editor obtém o tipo atômico e insere o nome atômico de tipo. Para um tipo derivado simples usa o tipo simples base. Para um tipo de lista o tipo atômico é `itemType`. Para uma união atômico, o tipo é o tipo atômico de primeiro `memberType`.  
  
## <a name="example"></a>Exemplo  
 As etapas nesta seção mostrar como usar o recurso esquema- gerado de snippet XML do editor XML.  
  
> [!NOTE]
>  Antes de iniciar estes procedimentos, salve o arquivo de esquema para o seu computador local.  
  
#### <a name="to-create-a-new-xml-file-and-associate-it-with-an-xml-schema"></a>Para criar um novo arquivo XML e associá-la com um esquema XML  
  
1.  Sobre o **arquivo** , aponte para **New**e clique em **arquivo**.  
  
2.  Selecione **arquivo XML** na **modelos** painel e clique em **abrir**.  
  
     Um novo arquivo é aberto no editor. O arquivo contém uma declaração XML padrão, `<?xml version="1.0" encoding="utf-8">`.  
  
3.  Na janela de propriedades do documento, clique no botão Procurar (**...** ) sobre o **esquemas** campo.  
  
     O **esquemas XSD** caixa de diálogo é exibida.  
  
4.  Clique em **Adicionar**.  
  
     O **abrir esquema XSD** caixa de diálogo é exibida.  
  
5.  Selecione o arquivo de esquema e clique em **aberto**.  
  
6.  Clique em **OK**.  
  
     O esquema XML agora está associado com o documento XML.  
  
#### <a name="to-generate-an-xml-snippet"></a>Para gerar um snippet XML  
  
1.  Tipo `<` no painel do editor.  
  
2.  A lista de membros exibe os itens possíveis:  
  
     **! –** para adicionar um comentário.  
  
     **! DOCTYPE** para adicionar um tipo de documento.  
  
     **?** Para adicionar uma instrução de processamento.  
  
     **Entre em contato com** para adicionar o elemento raiz.  
  
3.  Selecione **entre em contato com** na lista de membros e pressione ENTER.  
  
     O editor adiciona a tag de início `<Contact` e posicionar o cursor após o nome do elemento.  
  
4.  Pressione a tecla TAB para gerar dados XML para o elemento de `Contact` com base em suas informações de esquema.  
  
### <a name="input"></a>Entrada  
 O seguinte arquivo de esquema é usado por passo a passo.  
  
```  
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
 A seguir estão os dados XML que são gerados com base nas informações de esquema associada com o elemento de `Contact` . Itens marcados como `bold` designar campos editáveis no trecho XML.  
  
```  
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
 [Trechos de código XML](../xml-tools/xml-snippets.md)   
 [Como usar snippets XML](../xml-tools/how-to-use-xml-snippets.md)



