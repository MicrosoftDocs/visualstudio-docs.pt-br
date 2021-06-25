---
title: Vinculando atalhos de teclado a itens de menu | Microsoft Docs
description: Saiba como mapear um atalho de teclado no Visual Studio para um botão personalizado, um item de menu ou um comando de barra de ferramentas para o editor padrão ou um editor personalizado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6a9591a7412b0bcaf506483a16a6660790df5f40
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900428"
---
# <a name="bind-keyboard-shortcuts-to-menu-items"></a>Associar atalhos de teclado a itens de menu
Para associar um atalho de teclado a um comando de menu personalizado, basta adicionar uma entrada ao arquivo *. vsct* do pacote. Este tópico explica como mapear um atalho de teclado para um botão personalizado, um item de menu ou um comando de barra de ferramentas e como aplicar o mapeamento de teclado no editor padrão ou limitá-lo a um editor personalizado.

 Para atribuir atalhos de teclado a itens de menu existentes do Visual Studio, consulte [identificar e personalizar atalhos de teclado](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md).

## <a name="choose-a-key-combination"></a>Escolha uma combinação de teclas
 Muitos atalhos de teclado já são usados no Visual Studio. Você não deve atribuir o mesmo atalho a mais de um comando porque associações duplicadas são difíceis de detectar e também podem causar resultados imprevisíveis. Portanto, é uma boa ideia verificar a disponibilidade de um atalho antes de atribuí-lo.

### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>Para verificar a disponibilidade de um atalho de teclado

1. Na   >  janela do ambiente **Opções** de ferramentas  >   , selecione **teclado**.

2. Certifique-se de que **usar o novo atalho no** esteja definido como **global**.

3. Na caixa **pressione teclas de atalho** , digite o atalho de teclado que você deseja usar.

    Se o atalho já estiver sendo usado no Visual Studio, o **atalho usado no momento pelo** Box mostrará o comando que o atalho chama atualmente.

4. Tente combinações diferentes de chaves até encontrar uma que não esteja mapeada.

   > [!NOTE]
   > Os atalhos de teclado que usam **ALT** podem abrir um menu e não executar diretamente um comando. Portanto, o **atalho usado atualmente pelo** box pode estar em branco quando você digita um atalho que inclui **ALT**. Você pode verificar se o atalho não abre um menu fechando a caixa de diálogo **Opções** e, em seguida, pressionando as teclas.

   O procedimento a seguir pressupõe que você tenha um VSPackage existente com um comando de menu. Se precisar de ajuda para fazer isso, dê uma olhada em [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>Para atribuir um atalho de teclado a um comando

1. Abra o arquivo *. vsct* para seu pacote.

2. Crie uma `<KeyBindings>` seção vazia após a `<Commands>` se ela ainda não estiver presente.

   > [!WARNING]
   > Para obter mais informações sobre associações de chave, consulte [KeyBinding](../extensibility/keybinding-element.md).

    Na `<KeyBindings>` seção, crie uma `<KeyBinding>` entrada.

    Defina os `guid`  `id` atributos e para aqueles do comando que você deseja invocar.

    Defina o `mod1` atributo como **Control**, **ALT** ou **Shift**.

    A seção keybindings deve ser semelhante a esta:

   ```xml
   <KeyBindings>
       <KeyBinding guid="<name of command set>" id="<name of command id>"
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>
   </KeyBindings>

   ```

   Se o atalho de teclado exigir mais de duas chaves, defina `mod2` os `key2` atributos e.

   Na maioria das situações, **Shift** não deve ser usada sem um segundo modificador, pois pressioná-la já faz com que a maioria das chaves alfanuméricas digite uma letra maiúscula ou um símbolo.

   Os códigos de chave virtual permitem que você acesse chaves especiais que não têm um caractere associado a elas, por exemplo, chaves de função e a tecla **Backspace** . Para obter mais informações, consulte [códigos-chave virtuais](/windows/desktop/inputdev/virtual-key-codes).

   Para disponibilizar o comando no editor do Visual Studio, defina o `editor` atributo como `guidVSStd97` .

   Para disponibilizar o comando somente em um editor personalizado, defina o `editor` atributo como o nome do editor personalizado que foi gerado pelo modelo de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] pacote quando você criou o VSPackage que inclui o editor personalizado. Para localizar o valor do nome, examine a `<Symbols>` seção para um `<GuidSymbol>` nó cujo `name` atributo termina em " `editorfactory` ." Este é o nome do editor personalizado.

## <a name="example-1"></a>Exemplo 1
 Este exemplo associa o atalho de teclado **Ctrl** + **ALT** + **C** a um comando chamado `cmdidMyCommand` em um pacote denominado `MyPackage` .

```
<CommandTable>
. . .
<Commands>
. . .
</Commands>
<KeyBindings>
  <KeyBinding guid="guidMyPackageCmdSet" id="cmdidMyCommand"
      key1="C" mod1="CONTROL" mod2="ALT" editor="guidVSStd97" />
</KeyBindings>
. . .
</CommandTable>
```

## <a name="example-2"></a>Exemplo 2
 Este exemplo associa o atalho de teclado **Ctrl** + **B** a um comando chamado `cmdidBold` em um projeto chamado `TestEditor` . O comando está disponível somente no editor personalizado e não em outros editores.

```xml
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />
```

## <a name="see-also"></a>Confira também
- [Estendendo menus e comandos](../extensibility/extending-menus-and-commands.md)
