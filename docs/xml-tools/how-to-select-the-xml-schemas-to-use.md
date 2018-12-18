---
title: 'Como: Selecione os esquemas XML para usar'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: d6fda3ef-d465-4788-8514-2f2d528d658c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a04075c0625eb7b4dc899a4e183588b96eb7eadd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49872233"
---
# <a name="how-to-select-the-xml-schemas-to-use"></a>Como: selecione os esquemas XML para usar

O Editor XML fornece um cache de esquema localizado na *%InstallDir%\Xml\Schemas* directory. O cache de esquema inclui esquemas XML conhecidos que são usados para validação do IntelliSense e de documento XML.

O **esquemas** propriedade do documento é usada para selecionar um ou mais XML esquemas definição de esquema XSD (linguagem) para usar. Permite que você selecionar esquemas de cache do esquema, ou especifica um esquema que não está localizado no cache.

Os esquemas que você especifica são salvas no arquivo de opções de usuário de solução ocultado (. *suo*), juntamente com todos os outros XML propriedades do documento. Como resultado, você não tem que digitar novamente esses valores na próxima vez que você abrir a solução.

> [!NOTE]
> O editor pode validar usando um esquema embutido, ou um esquema referenciado pelo atributo de `xsd:schemaLocation` . Para obter mais informações, consulte [validação de documento XML](../xml-tools/xml-document-validation.md).

## <a name="to-select-an-xml-schema-from-the-schema-cache"></a>Para selecionar um esquema XML de cache de esquema

1. Abrir um arquivo no editor XML.

2. Na janela de propriedades do documento, clique no botão sobre a **esquemas** campo.

    O **esquemas XML** caixa de diálogo é exibida. A caixa de diálogo lista todos os esquemas com um. *xsd* extensão no cache de esquema (incluindo os Esquemas referenciados na *Catalog* arquivo) e também qualquer esquema que está na solução atual, aberta no Visual Studio, referenciada em um `xsd:schemaLocation` atributo ou referenciados na **esquemas** propriedade.

3. Selecione os esquemas para usar a validação seguindo um destes procedimentos:

   - Selecione um esquema listado na **esquemas XML** caixa de diálogo, clique o **uso** coluna e, em seguida, selecione **usar este esquema**.

     -ou-

   - Selecione vários esquemas listados na **esquemas XML** caixa de diálogo, o botão direito do mouse e selecione **usar este esquema**.

4. Clique em **OK**.

    A lista de esquemas selecionados será copiada para o **esquemas** propriedade de documento.

## <a name="to-add-an-xml-schema-to-the-schema-cache"></a>Para adicionar um esquema XML para o cache de esquema

1.  Na janela de propriedades do documento, clique no botão sobre a **esquemas** campo.

2.  Clique em **Adicionar**.

     Isso abre o **abrir esquema XSD** caixa de diálogo.

3.  Procurar e selecione os esquemas para adicionar ao cache de esquema.

4.  Clique em **aberto**.

     Os esquemas adicionados ao esquema armazenam em cache e é o **uso** o valor da coluna é definido como **usar este esquema**.

## <a name="to-delete-an-xml-schema-from-the-schema-cache"></a>Para excluir um esquema XML do cache de esquema

1.  Na janela de propriedades do documento, clique no botão sobre a **esquemas** campo.

2.  Selecione o esquema para remover e, em seguida, clique em **remover**.

     O esquema é removido do cache de memória do esquema, mas não é removido do sistema de arquivos.

    > [!NOTE]
    > Se você ainda terá uma referência para o esquema por meio de um `schemaLocation` atributo ou uma correspondência `targetNamespace` , em seguida, **remover** não funcionará nesta situação devido à associação automática. Nesse caso, é recomendável que você marca o esquema como **não use esquemas selecionados** na **usar** coluna.

## <a name="see-also"></a>Consulte também

- [Cache de esquema](../xml-tools/schema-cache.md)
- [Caixa de diálogo de esquemas XML](../xml-tools/xml-schemas-dialog-box.md)
- [Editor de XML](../xml-tools/xml-editor.md)