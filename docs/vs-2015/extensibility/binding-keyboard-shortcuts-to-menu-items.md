---
title: Associando a atalhos de teclado a itens de Menu | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5fd5ab9b09956c41620947ad1bcf529550db4aca
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752900"
---
# <a name="binding-keyboard-shortcuts-to-menu-items"></a>Associando atalhos de teclado a itens de menu
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para associar um atalho de teclado a um comando de menu personalizado, adicione uma entrada para o arquivo. VSCT para o pacote. Este tópico explica como mapear um atalho de teclado para um botão personalizado, o item de menu ou o comando da barra de ferramentas e como aplicar o mapeamento de teclado no editor padrão ou limite-o a um editor personalizado.  
  
 Para atribuir atalhos de teclado para os itens de menu existentes do Visual Studio, consulte [identificando e personalizando atalhos de teclado](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md).  
  
## <a name="choosing-a-key-combination"></a>Escolher uma combinação de teclas  
 Muitos atalhos de teclado já são usados no Visual Studio. Você não deve atribuir o mesmo atalho para mais de um comando como ligações duplicadas são difíceis de detectar e também podem causar resultados imprevisíveis. Portanto, é uma boa ideia verificar a disponibilidade de um atalho antes de atribuí-lo.  
  
#### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>Para verificar a disponibilidade de um atalho de teclado  
  
1. No **Ferramentas / opções / ambiente** janela, selecione **teclado**.  
  
2. Certifique-se de que **usar novo atalho em** é definido como **Global**.  
  
3. No **pressionar teclas de atalho** , digite o atalho de teclado que você deseja usar.  
  
    Se o atalho já é usado no Visual Studio, o **atalho usado atualmente por** caixa mostrará o comando que o atalho chama no momento.  
  
4. Tente diferentes combinações de teclas até encontrar uma que não está mapeado.  
  
   > [!NOTE]
   >  Atalhos de teclado que usam ALT podem abrir um menu e não diretamente, executar um comando. Portanto, o **atalho usado atualmente por** caixa pode estar em branco quando você digita um atalho que inclui ALT. Você pode verificar o atalho não abre um menu ao fechar o **opções** caixa de diálogo e, em seguida, pressionando as teclas.  
  
   O procedimento a seguir pressupõe que você tenha um VSPackage existente com um comando de menu. Se você precisar de ajuda para fazer isso, dê uma olhada [criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
#### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>Para atribuir um atalho de teclado a um comando  
  
1. Abra o arquivo. VSCT para seu pacote.  
  
2. Criar vazio `<KeyBindings>` seção após o `<Commands>` se ele não ainda estiver presente.  
  
   > [!WARNING]
   >  Para obter mais informações sobre associações de teclas, consulte [Keybinding](../extensibility/keybinding-element.md).  
  
    No `<KeyBindings>` seção, crie um `<KeyBinding>` entrada.  
  
    Defina as `guid` e `id` atributos para os do comando que você deseja invocar.  
  
    Defina as `mod1` de atributo para **controle**, **Alt**, ou **Shift**.  
  
    A seção de associações de teclas deve ter esta aparência:  
  
   ```xml  
   <KeyBindings>  
       <KeyBinding guid="<name of command set>" id="<name of command id>"  
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>  
   </KeyBindings>  
  
   ```  
  
   Se o atalho de teclado exigir mais de duas chaves, defina as `mod2` e `key2` atributos.  
  
   Na maioria das situações, **Shift** não deve ser usado sem um modificador segundo porque pressioná-lo já faz com que a maioria das teclas alfanuméricos digitar uma letra maiuscula ou um símbolo.  
  
   Códigos de tecla virtual permite que você acesse chaves especiais que não têm um caractere associado a eles, por exemplo, as teclas de função e o **BACKSPACE** chave. Para obter mais informações, consulte [códigos de tecla Virtual](http://go.microsoft.com/fwlink/?LinkID=105932).  
  
   Para tornar o comando disponível no Visual Studio editor, defina as `editor` atributo `guidVSStd97`.  
  
   Para tornar o comando disponível somente em um editor personalizado, defina as `editor` de atributo para o nome do editor personalizado que foi gerado pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] modelo de pacote quando você criou o VSPackage que inclui o editor personalizado. Para localizar o valor do nome, procure na `<Symbols>` seção para uma `<GuidSymbol>` nó cujo `name` atributo termina em "`editorfactory`." Esse é o nome do editor personalizado.  
  
## <a name="example"></a>Exemplo  
 Este exemplo associa o atalho de teclado CTRL + ALT + C para um comando chamado `cmdidMyCommand` em um pacote chamado `MyPackage`.  
  
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
  
## <a name="example"></a>Exemplo  
 Este exemplo associa o atalho de teclado CTL + B para um comando chamado `cmdidBold` em um projeto chamado `TestEditor`. O comando está disponível apenas no editor personalizado e não em outros editores.  
  
```xml  
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Ampliar menus e comandos](../extensibility/extending-menus-and-commands.md)

