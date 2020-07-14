---
title: Modificar comando de menu padrão em DSL
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- .vsct files, adding commands to a domain-specific language
- Domain-Specific Language, adding custom commands
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a7236c074bda17023c989c744042db2de4046558
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532490"
---
# <a name="how-to-modify-a-standard-menu-command-in-a-domain-specific-language"></a>Como modificar um comando de menu padrão em uma linguagem específica do domínio

É possível modificar o comportamento de alguns dos comandos padrão que são definidos automaticamente na DSL. Por exemplo, você pode modificar **recortar** para que ele exclua informações confidenciais. Para isso, substitua métodos em uma classe de conjunto de comandos. Essas classes são definidas no arquivo CommandSet.cs, no projeto DslPackage e são derivadas de <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>.

> [!NOTE]
> Se você quiser criar seus próprios comandos de menu, consulte [como adicionar um comando ao menu de atalho](../modeling/how-to-add-a-command-to-the-shortcut-menu.md).

## <a name="what-commands-can-you-modify"></a>Quais comandos podem ser modificados?

### <a name="to-discover-what-commands-you-can-modify"></a>Para descobrir quais comandos podem ser modificados

1. No projeto `DslPackage`, abra `GeneratedCode\CommandSet.cs`. Esse arquivo C# pode ser encontrado em Gerenciador de Soluções como uma subsidiária do `CommandSet.tt` .

2. Localizar classes neste arquivo cujos nomes terminam com " `CommandSet` ", por exemplo, `Language1CommandSet` e `Language1ClipboardCommandSet` .

3. Em cada classe de conjunto de comandos, digite "`override`" seguido por um espaço. O IntelliSense mostrará uma lista dos métodos que podem ser substituídos. Cada comando contém um par de métodos cujos nomes começam com "`ProcessOnStatus`" e "`ProcessOnMenu`".

4. Observe qual das classes de conjunto de comandos contém o comando que deseja modificar.

5. Feche o arquivo sem salvar as edições.

    > [!NOTE]
    > Normalmente, é aconselhável não editar arquivos que foram gerados. Qualquer edição será perdida na próxima vez em que os arquivos forem gerados.

## <a name="extend-the-appropriate-command-set-class"></a>Estenda a classe de conjunto de comandos adequada

Crie um novo arquivo que contenha uma declaração parcial da classe de conjunto de comandos.

### <a name="to-extend-the-command-set-class"></a>Estender a classe de Conjunto de Comandos

1. No Gerenciador de Soluções, no projeto DslPackage, abra a pasta GeneratedCode e procure sob CommandSet.tt e abra o arquivo gerado CommandSet.cs. Observe o namespace e o nome da primeira classe que está definida lá. Por exemplo, é possível ver:

     `namespace Company.Language1`

     `{ ...  internal partial class Language1CommandSet : ...`

2. Em **DslPackage**, crie uma pasta chamada **código personalizado**. Nessa pasta, crie um novo arquivo de classe chamado `CommandSet.cs` .

3. No novo arquivo, grave uma declaração parcial que contenha o mesmo namespace e o nome que a classe parcial gerada. Por exemplo:

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Design;
    namespace Company.Language1 /* Make sure this is correct */
    { internal partial class Language1CommandSet { ...
    ```

    > [!NOTE]
    > Se você usou o modelo de arquivo de classe para criar o novo arquivo, deverá corrigir o namespace e o nome da classe.

## <a name="override-the-command-methods"></a>Substitua os métodos de comando

A maioria dos comandos tem dois métodos associados: o método com um nome como `ProcessOnStatus` ... Determina se o comando deve ser visível e habilitado. É chamado sempre que o usuário clicar com o botão direito do mouse no diagrama e deve ser executado rapidamente e não realizar alterações. `ProcessOnMenu`... é chamado quando o usuário clica no comando e deve executar a função do comando. É possível substituir qualquer um dos métodos ou os dois.

### <a name="to-change-when-the-command-appears-on-a-menu"></a>Para alterar quando o comando é exibido em um menu

Substituir o ProcessOnStatus... forma. Esse método deve definir as propriedades Visível e Habilitado de seu parâmetro MenuCommand. Geralmente, o comando examina this.CurrentSelection para determinar se o comando é aplicável aos elementos selecionados e também poderá examinar suas propriedades para determinar se o comando pode ser aplicado em seu estado atual.

Como guia geral, a propriedade Visível deve ser determinada por quais elementos estão selecionados. A propriedade Habilitado, que determina se o comando é exibido em preto ou cinza no menu, deve depender do estado atual da seleção.

O exemplo a seguir desabilita o item de menu Excluir quando o usuário selecionar mais de uma forma.

> [!NOTE]
> Esse método não afeta se o comando está disponível através de um pressionamento de tecla. Por exemplo, desabilitar o item de menu Excluir não impede a invocação do comando através da tecla Delete.

```csharp
/// <summary>
/// Called when user right-clicks on the diagram or clicks the Edit menu.
/// </summary>
/// <param name="command">Set Visible and Enabled properties.</param>
protected override void ProcessOnStatusDeleteCommand (MenuCommand command)
{
  // Default settings from the base method.
  base.ProcessOnStatusDeleteCommand(command);
  if (this.CurrentSelection.Count > 1)
  {
    // If user has selected more than one item, Delete is greyed out.
    command.Enabled = false;
  }
}
```

É uma boa prática chamar primeiro o método base, para lidar com todos os casos e as configurações pelos quais não houver interesse.

O método ProcessOnStatus não deve criar, excluir ou atualizar elementos no Armazenamento.

### <a name="to-change-the-behavior-of-the-command"></a>Para alterar o comportamento do comando

Substituir o ProcessOnMenu... forma. O exemplo a seguir impede o usuário de excluir mais de um elemento de cada vez, mesmo usando a tecla Delete.

```csharp
/// <summary>
/// Called when user presses Delete key
/// or clicks the Delete command on a menu.
/// </summary>
protected override void ProcessOnMenuDeleteCommand()
{
  // Allow users to delete only one thing at a time.
  if (this.CurrentSelection.Count <= 1)
  {
    base.ProcessOnMenuDeleteCommand();
  }
}
```

Se o código fizer alterações ao Armazenamento, como criar, excluir ou atualizar elementos ou links, será necessário fazer isso dentro de uma transação. Para obter mais informações, consulte [como criar e atualizar elementos de modelo](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).

### <a name="write-the-code-of-the-methods"></a>Escreva o código dos métodos

Os seguintes fragmentos são úteis com frequência dentro desses métodos:

- `this.CurrentSelection`. A forma que o usuário clicou com o botão direito sempre é incluída nessa lista de formas e conectores. Se o usuário clicar em uma parte em branco do diagrama, o Diagrama será o único membro da lista.

- `this.IsDiagramSelected()` - `true`Se o usuário clicou em uma parte em branco do diagrama.

- `this.IsCurrentDiagramEmpty()`

- `this.IsSingleSelection()`-o usuário não selecionou várias formas

- `this.SingleSelection`-a forma ou o diagrama em que o usuário clicou com o botão direito

- `shape.ModelElement as MyLanguageElement`-o elemento de modelo representado por uma forma.

Para obter mais informações sobre como navegar de elemento para elemento e sobre como criar objetos e links, consulte [navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

## <a name="see-also"></a>Confira também

- <xref:System.ComponentModel.Design.MenuCommand>
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Como adicionar um comando ao menu de atalho](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)
- [Como os VSPackages adicionam elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Arquivos .Vsct (Visual Studio Command Table)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Referência do esquema XML do VSCT](../extensibility/vsct-xml-schema-reference.md)
- [VMSDK-exemplo de diagramas de circuito. Ampla personalização de DSL](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)
