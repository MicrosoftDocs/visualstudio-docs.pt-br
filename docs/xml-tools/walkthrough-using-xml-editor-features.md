---
title: 'Walkthrough: usando recursos do editor de XML'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ea8dc357-2e66-455a-aec2-7ccaccfc9adf
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1cebf6f7621fb5fada37b8e4592efd429bdc85e6
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817392"
---
# <a name="walkthrough-use-xml-editor-features"></a>Walkthrough: usar recursos do editor de XML

As etapas nessa explicação passo a passo mostram como criar um novo documento XML. O passo a passo também usa alguns dos recursos do editor de XML que o tornam valioso para a criação de XML.

> [!NOTE]
> Antes de iniciar o passo a passo, salve o arquivo *HireDate. xsd* (incluído abaixo neste tópico) em seu computador local.

## <a name="to-create-a-new-xml-file-and-associate-it-with-an-xml-schema"></a>Para criar um novo arquivo XML e associá-lo a um esquema XML

1. No menu **arquivo** , aponte para **novo**e clique em **arquivo**.

2. Selecione **arquivo XML** no painel **modelos** e clique em **abrir**.

     Um novo arquivo é aberto no editor. O arquivo contém uma declaração XML padrão, `<?xml version="1.0" encoding="utf-8">`.

3. Na janela Propriedades do documento, clique no botão procurar (**...**) no campo **esquemas** .

     A caixa de diálogo **esquemas XSD** é exibida.

4. Clique em **Adicionar**.

     A caixa de diálogo **abrir esquema XSD** é exibida.

5. Selecione o arquivo *HireDate. xsd* e clique em **abrir**.

6. Clique em **OK**.

     O esquema XML agora está associado com o documento XML. O esquema XML é usado para validar o documento. Também é usado pelo IntelliSense para preencher a lista de membros de elementos válidos.

## <a name="to-add-data"></a>Para adicionar dados

1. Tipo `<` no painel do editor.

     A lista de membros exibe os itens possíveis:

    - **!--** adicionar um comentário.

    - **! DOCTYPE** para adicionar um tipo de documento.

    - **?** para adicionar uma instrução de processamento.

    - **funcionário** para adicionar o elemento raiz.

2. Selecione ** &lt; !--** para adicionar um nó de comentário e pressione **Enter**.

     O editor insere uma marca de fim do comentário e colocar o cursor entre o início e marcas de comentário final.

3. Digite o **arquivo XML de teste**.

4. Em uma nova linha, digite `<` e selecione **funcionário** na lista de membros.

     O editor adiciona o início de um elemento XML, `<employee`. Neste momento você pode adicionar atributos para o elemento ou você pode fechar a tag de início digitando `>`.

5. Tipo `>` para a marca de fechamento.

6. O editor adiciona a marca de fim. A marca de fim é adicionada com um a linha subescrita ondulada que indica um erro de validação. A **dica de ferramenta** exibe a mensagem: **o elemento ' Employee ' tem conteúdo incompleto. ' ID ' esperado**.

7. Digite `<` e selecione **ID** na lista de membros. Digite `>`.

     O editor adicione o elemento XML, `<ID></ID>`, e posicionar o cursor após a marca de início de identificação.

8. Digite **ABC**.

     O texto **ABC** tem um sublinhado ondulado. A **dica de ferramenta** exibe a mensagem: **o elemento ' ID ' tem um valor inválido de acordo com seu tipo de dados**.

9. Clique com o botão direito do mouse no elemento ID e selecione **ir para definição**.

     O editor abre o arquivo *HireDate. xsd* em uma nova janela de documento e posiciona o cursor sobre a definição do elemento de esquema de ID.

10. Retorne ao arquivo XML e substitua o texto **ABC** por **123**.

     O sublinhado ondulado e a **dica de ferramenta** são apagados sob o valor do elemento ID. A **dica de ferramenta** para a marca de fim de funcionário agora exibe a mensagem: **o elemento ' Employee ' tem conteúdo incompleto. ' Data de contratação ' esperado**.

11. Coloque o cursor após a marca de fim de ID, digite em `<` , selecione **contratação-Data** na lista de membros e digite `>` .

     O editor adicione o elemento XML, `<hire-date></hire-date>`, e posicionar o cursor após a marca de início da data de admissão.

12. Digite **2003-01-10** para o valor de data de contratação.

## <a name="to-format-the-xml-document"></a>Para formatar o documento XML

- Selecione o botão **Formatar documento** na barra de ferramentas do editor de XML ou pressione **Ctrl** + **E**,**D**.

   ![Botão Formatar documento XML no Visual Studio](media/format-xml-document.png)

   O documento XML é reformatado.

## <a name="to-save-the-xml-document"></a>Para salvar o documento XML

1. No menu **arquivo**, selecione **Salvar como**.

     A caixa de diálogo **salvar arquivo como** é exibida. O nome de arquivo padrão é *' xmlarquivo1 '*.

2. Insira o nome do arquivo e o local para o documento XML e clique em **salvar**.

## <a name="hiredatexsd-file"></a>arquivo. xsd contratado

O seguinte arquivo de esquema é usado neste passo a passos:

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

## <a name="see-also"></a>Veja também

- [Editor de XML](../xml-tools/xml-editor.md)
