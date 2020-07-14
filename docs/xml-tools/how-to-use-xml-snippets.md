---
title: Como usar trechos XML
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 3a27375b-81cc-48f6-a884-e1cb8c4f78f5
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e72c5ef5d5c33c46a9f09eb604d0a2e40cf9a6e7
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815910"
---
# <a name="how-to-use-xml-snippets"></a>Como: usar trechos XML

Você pode invocar trechos XML usando os dois comandos a seguir no menu de atalho do editor de XML. O comando **Insert Snippet** insere o trecho XML na posição do cursor. O comando **surround with** encapsula o trecho XML em torno do texto selecionado. Cada snippets XML designou tipos de snippets. Os tipos de trecho determinam se o trecho de código está disponível com o comando **Insert Snippet** , o comando **surround with** ou ambos.

Depois que o snippet XML foi adicionado ao editor, todos os campos editáveis no snippet estão realçados em amarelo, e o cursor está localizado no primeiro campo editável.

## <a name="insert-snippet"></a>Inserir Snippet

Os procedimentos a seguir descrevem como acessar o comando **Insert Snippet** .

> [!NOTE]
> O comando **Inserir trecho de código** também está disponível por meio do atalho de teclado (**Ctrl** + **K**e **Ctrl** + **X**).

### <a name="to-insert-snippets-from-the-shortcut-menu"></a>Para inserir snippets do menu de atalho

1. Posicionar o cursor onde você deseja inserir o snippet XML.

2. Clique com o botão direito do mouse e selecione **Inserir trecho**.

   Uma lista de snippets disponíveis XML é exibida.

3. Selecione um trecho da lista usando o mouse ou digitando o nome do trecho de código e pressionando **Tab** ou **Enter**.

### <a name="to-insert-snippets-using-the-intellisense-menu"></a>Para inserir snippets usando o menu do IntelliSense

1. Posicionar o cursor onde você deseja inserir o snippet XML.

2. No menu **Editar** , aponte para **IntelliSense**e, em seguida, selecione **Inserir trecho de código**.

   Uma lista de snippets disponíveis XML é exibida.

3. Selecione um trecho da lista usando o mouse ou digitando o nome do trecho de código e pressionando **Tab** ou **Enter**.

### <a name="to-insert-snippets-through-the-intellisense-complete-word-list"></a>Para inserir trechos por meio da lista de palavras do IntelliSense Complete

1. Posicionar o cursor onde você deseja inserir o snippet XML.

2. Comece a digitar o snippet XML que você deseja adicionar ao seu arquivo. Se o preenchimento automático é ativada, a lista de palavras completo do IntelliSense é exibida. Se não aparecer, pressione **Ctrl** + **espaço** para ativá-lo.

3. Selecione o snippet XML da lista de palavras completo.

4. Pressione **Tab**e **Tab** para invocar o trecho XML.

> [!NOTE]
> Pode haver casos quando o snippet XML não é chamado. Por exemplo, se você tentar inserir um elemento de `xs:complexType` dentro de um nó de `xs:element` , o editor não gerencia um snippet XML. Quando um elemento de `xs:complexType` é usado dentro de um nó de `xs:element` , não houver nenhum atributo ou subelements necessário, o editor não tem nenhum dados para inserir.

### <a name="to-insert-snippets-using-the-shortcut-name"></a>Para inserir snippets usando o nome do atalho

1. Posicionar o cursor onde você deseja inserir o snippet XML.

2. Tipo `<` no painel do editor.

3. Pressione **ESC** para fechar a lista de palavras concluídas do IntelliSense.

4. Digite o nome do atalho do trecho e pressione **Tab** para invocar o trecho XML.

## <a name="surround-with"></a>Envolver com

Os procedimentos a seguir descrevem como acessar o comando **surround with** .

> [!NOTE]
> O comando **surround with** também está disponível por meio do atalho de teclado (**Ctrl** + **K**, depois **Ctrl** + **S**).

### <a name="to-use-surround-with-from-the-context-menu"></a>Para usar surround with no menu de contexto

1. Selecione o texto a ser circundado no editor de XML.

2. Clique com o botão direito do mouse e selecione **Circundar com**.

   Uma lista de bordadura disponíveis com snippets XML é exibida.

3. Selecione um trecho da lista usando o mouse ou digitando o nome do trecho de código e pressionando **Tab** ou **Enter**.

### <a name="to-use-surround-with-from-the-intellisense-menu"></a>Para usar o surround com no menu do IntelliSense

1. Selecione o texto a ser circundado no editor de XML.

2. No menu **Editar** , aponte para **IntelliSense**e, em seguida, selecione **surround com**.

   Uma lista de bordadura disponíveis com snippets XML é exibida.

3. Selecione um trecho da lista usando o mouse ou digitando o nome do trecho de código e pressionando **Tab** ou **Enter**.

## <a name="use-xml-snippets"></a>Usar snippets XML

Uma vez que você escolher um snippet XML, o texto de snippet de código é inserido automaticamente a posição do cursor. Todos os campos editáveis no snippet são realçadas, e o primeiro campo editável é automaticamente selecionado. O campo selecionado é convertido.

Quando um campo é selecionado, você pode digitar um novo valor para o campo. Pressionar **Tab** percorre os campos editáveis do trecho de código; pressionar **Shift** + **Tab** percorre os ciclos na ordem inversa. Clicando em um campo colocar o cursor no campo, e clique duas vezes em um campo selecioná-lo. Quando um campo é realçado, uma dica de ferramenta pode ser exibido, oferecendo uma descrição do campo.

Somente a primeira instância de um campo dado é editável. Quando esse campo é realçado, as outras instâncias do campo são descritas. Quando você altera o valor de um campo editável, o campo ele alterado everywhere é usado no snippet.

Pressionar **Enter** ou **ESC** cancela a edição de campo e retorna o editor para normal.

As cores padrão para campos de trecho de código editável podem ser alteradas modificando a configuração do **campo de trecho de código** no painel **fontes e cores** da caixa de diálogo **Opções** . Para obter mais informações, consulte [como alterar fontes e cores no editor](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md).

## <a name="see-also"></a>Veja também

- [Snippets XML](../xml-tools/xml-snippets.md)
- [Como gerar um trecho XML a partir de um esquema XML](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)
- [Como: criar trechos XML](../xml-tools/how-to-create-xml-snippets.md)
