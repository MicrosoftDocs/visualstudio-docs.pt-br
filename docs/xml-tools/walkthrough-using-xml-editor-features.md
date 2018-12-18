---
title: 'Passo a passo: Usando funcionalidades do editor XML'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: ea8dc357-2e66-455a-aec2-7ccaccfc9adf
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: afda2968ece2a18b7abdc2c4c35e4353206cbe42
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34693819"
---
# <a name="walkthrough-use-xml-editor-features"></a>Passo a passo: Usar recursos do editor de XML

As etapas nessa explicação passo a passo mostram como criar um novo documento XML. A explicação passo a passo também usa alguns dos recursos do editor XML que tornam valioso para criar XML.

> [!NOTE]
> Antes de iniciar o passo a passo, salve o *hireDate.xsd* arquivo (incluído abaixo neste tópico) para o computador local.

## <a name="to-create-a-new-xml-file-and-associate-it-with-an-xml-schema"></a>Para criar um novo arquivo XML e associá-lo a um esquema XML

1.  Sobre o **arquivo** , aponte para **novo**e clique em **arquivo**.

2.  Selecione **arquivo XML** no **modelos** painel e clique em **abrir**.

     Um novo arquivo é aberto no editor. O arquivo contém uma declaração XML padrão, `<?xml version="1.0" encoding="utf-8">`.

3.  Na janela de propriedades do documento, clique no botão Procurar (**...** ) sobre o **esquemas** campo.

     O **esquemas XSD** caixa de diálogo é exibida.

4.  Clique em **Adicionar**.

     O **esquema XSD aberto** caixa de diálogo é exibida.

5.  Selecione o *hireDate.xsd* de arquivo e clique em **abrir**.

6.  Clique em **OK**.

     O esquema XML agora está associado com o documento XML. O esquema XML é usado para validar o documento. Também é usado pelo IntelliSense para preencher a lista de membros de elementos válidos.

## <a name="to-add-data"></a>Para adicionar dados

1.  Tipo `<` no painel do editor.

     A lista de membros exibe os itens possíveis:

    -   **!-** para adicionar um comentário.

    -   **! DOCTYPE** para adicionar um tipo de documento.

    -   **?** Para adicionar uma instrução de processamento.

    -   **funcionário** para adicionar o elemento raiz.

2.  Selecione **<!-** para adicionar um nó de comentário e pressione **Enter**.

     O editor insere uma marca de fim do comentário e colocar o cursor entre o início e marcas de comentário final.

3.  Digite **arquivo XML de teste**.

4.  Em uma nova linha, digite `<`e selecione **funcionário** da lista de membros.

     O editor adiciona o início de um elemento XML, `<employee`. Neste momento você pode adicionar atributos para o elemento ou você pode fechar a tag de início digitando `>`.

5.  Tipo `>` para a marca de fechamento.

6.  O editor adiciona a marca de fim. A marca de fim é adicionada com um a linha subescrita ondulada que indica um erro de validação. O **dica de ferramenta** exibe a mensagem: **o elemento 'funcionário' apresenta conteúdo incompleto. Esperado 'ID'**.

7.  Tipo `<` e selecione **ID** da lista de membros. Digite `>`.

     O editor adicione o elemento XML, `<ID></ID>`, e posicionar o cursor após a marca de início de identificação.

8.  Tipo **abc**.

     O **abc** texto tiver um sublinhado ondulado. O **dica de ferramenta** exibe a mensagem: **o elemento 'ID' tem um valor inválido de acordo com seu tipo de dados**.

9. Clique no elemento de ID e selecione **ir para definição**.

     Abre o editor de *hireDate.xsd* arquivo em uma nova janela de documento e posiciona o cursor na definição de elemento de esquema de ID.

10. Retornar para o arquivo XML e substitua o **abc** texto com **123**.

     O sublinhado ondulado e **dica de ferramenta** são limpos com o valor do elemento de ID. O **dica de ferramenta** para o final do funcionário marca agora exibe a mensagem: **o elemento 'funcionário' apresenta conteúdo incompleto. Esperado 'Data de contratação'**.

11. Coloque o cursor após a marca de fim de ID, digite `<`, selecione **data de contratação** na lista de membros e, em seguida, digite `>`.

     O editor adicione o elemento XML, `<hire-date></hire-date>`, e posicionar o cursor após a marca de início da data de admissão.

12. Digite **2003-01-10** para o valor de data de contratação.

## <a name="to-format-the-xml-document"></a>Para formatar o documento XML

- Selecione o **documento** botão da barra de ferramentas do Editor de XML.

    O documento XML é reformatado.

## <a name="to-save-the-xml-document"></a>Para salvar o documento XML

1.  Do **arquivo** menu, selecione **Salvar como**.

     O **salvar arquivo como** caixa de diálogo é exibida. O nome de arquivo padrão é *'XMLFile1'*.

2.  Insira o nome do arquivo e o local para o documento XML e clique em **salvar**.

## <a name="hiredatexsd-file"></a>arquivo hireDate.xsd
 O seguinte arquivo de esquema é usado por passo a passo.

```xml
<?xml version="1.0"?>
<xs:schema attributeFormDefault="unqualified"
     elementFormDefault="qualified" targetNamespace="urn:empl-hire"
     xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="employee">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="ID" type="xs:unsignedShort" />
        <xs:element name="hire-date" type="xs:date" />
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

## <a name="see-also"></a>Consulte também

- [Editor de XML](../xml-tools/xml-editor.md)