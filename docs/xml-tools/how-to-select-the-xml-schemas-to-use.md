---
title: 'Como: Selecione os esquemas XML para usar'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d6fda3ef-d465-4788-8514-2f2d528d658c
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 06f9de6927d616d6cf08995c076246c8a45ec014
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815962"
---
# <a name="how-to-select-the-xml-schemas-to-use"></a>Como: selecionar os esquemas XML a serem usados

O editor de XML fornece um cache de esquema localizado no diretório *%VSINSTALLDIR%\xml\Schemas* O cache de esquema inclui esquemas XML conhecidos que são usados para validação do IntelliSense e de documento XML.

Use a propriedade de documento **esquemas** para selecionar um ou mais esquemas de linguagem de definição de esquema XML (XSD). Você pode selecionar esquemas do cache de esquema ou em outro lugar.

Os esquemas que você especificar são salvos em um arquivo de opções de usuário da solução (oculta) (.* Suo*), juntamente com todas as outras propriedades de documento XML. Como resultado, você não precisará reinserir esses valores na próxima vez que abrir a solução.

> [!NOTE]
> O editor pode validar usando um esquema embutido ou um esquema referenciado pelo `xsd:schemaLocation` atributo. Para obter mais informações, consulte [validação de documento XML](../xml-tools/xml-document-validation.md).

## <a name="to-select-an-xml-schema-from-the-schema-cache"></a>Para selecionar um esquema XML do cache de esquema

1. Abrir um arquivo no editor XML.

2. Na janela Propriedades do documento, clique no campo **esquemas** . Quando o botão procurar (...) for exibido, clique nele.

   ![Propriedade schemas para um arquivo XML](media/properties-schemas.png)

   A [caixa de diálogo esquemas XML](xml-schemas-dialog-box.md) é aberta. A caixa de diálogo lista todos os esquemas com um. extensão *XSD* no cache de esquema (incluindo esquemas referenciados no arquivo *catalog.xml* ) e também qualquer esquema que esteja na solução atual, aberto no Visual Studio, referenciado em um `xsd:schemaLocation` atributo ou referenciado na propriedade **esquemas** .

3. Selecione os esquemas para usar a validação seguindo um destes procedimentos:

   - Selecione um esquema listado na caixa de diálogo **esquemas XML** , clique na coluna **usar** e, em seguida, selecione **usar este esquema**.

     -ou-

   - Selecione vários esquemas listados na caixa de diálogo **esquemas XML** e clique com o botão direito do mouse e selecione **usar este esquema**.

4. Selecione **OK**.

   A lista de esquemas selecionados é copiada de volta para a propriedade de documento **esquemas** .

## <a name="to-add-an-xml-schema-to-the-schema-cache"></a>Para adicionar um esquema XML ao cache de esquema

1. Na janela Propriedades do documento, clique no botão no campo **esquemas** .

2. Clique em **Adicionar**.

   A caixa de diálogo **abrir esquema XSD** é aberta.

3. Procurar e selecione os esquemas para adicionar ao cache de esquema.

4. Clique em **Abrir**.

   Os esquemas são adicionados ao cache de esquema e o valor de coluna de **uso** é definido para **usar esse esquema**.

## <a name="to-delete-an-xml-schema-from-the-schema-cache"></a>Para excluir um esquema XML do cache de esquema

1. Na janela Propriedades do documento, clique no botão no campo **esquemas** .

2. Selecione o esquema a ser removido e clique em **remover**.

   O esquema é removido do cache de memória do esquema, mas não é removido do sistema de arquivos.

   > [!NOTE]
   > Se você ainda tiver uma referência ao esquema por meio de um `schemaLocation` atributo ou se uma correspondência for `targetNamespace` **removida** , isso não funcionará nessa situação devido à associação automática. Nesse caso, é recomendável que você marque o esquema como **não usar esquemas selecionados** na coluna **usar** .

## <a name="see-also"></a>Veja também

- [Cache de esquema](../xml-tools/schema-cache.md)
- [Caixa de diálogo esquemas XML](../xml-tools/xml-schemas-dialog-box.md)
- [Editor de XML](../xml-tools/xml-editor.md)
