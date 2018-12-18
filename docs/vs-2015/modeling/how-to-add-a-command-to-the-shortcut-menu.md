---
title: 'Como: adicionar um comando ao Menu de atalho | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
ms.assetid: cd550399-05fc-4dbf-be4c-f5094bb752ce
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: e7d15c1991ee70a0b1a163c8968e42fe450b7919
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49833506"
---
# <a name="how-to-add-a-command-to-the-shortcut-menu"></a>Como adicionar um comando ao menu de atalho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível adicionar comandos de menu à linguagem específica do domínio (DSL) para que seus usuários possam executar tarefas que são específicas de sua DSL. Os comandos aparecem no menu de contexto (atalho) quando os usuários clicam com o botão direito do mouse no diagrama. Você pode definir um comando para aparecer no menu apenas em circunstâncias específicas. Por exemplo, você pode tornar o comando visível apenas quando o usuário clicar em tipos específicos de elementos ou em elementos em estados específicos.  
  
 Um resumo das etapas executadas no projeto DslPackage são apresentadas abaixo:  
  
1. [Declarar o comando em Commands. VSCT](#VSCT)  
  
2. [Atualizar o número de versão do pacote em Package.tt](#version). Você precisará fazer isso sempre que alterar o Commands.vsct  
  
3. [Escrever métodos na classe Commandset&lt;1](#CommandSet) para tornar o comando visível e definir o que você deseja que o comando para fazer.  
  
   Para obter exemplos, consulte o [site do SDK de visualização e modelagem](http://go.microsoft.com/fwlink/?LinkID=185579).  
  
> [!NOTE]
>  Também é possível modificar o comportamento de alguns comandos existentes, tais como Recortar, Colar, Selecionar Tudo e Imprimir substituindo métodos em CommandSet.cs. Para obter mais informações, consulte [como: modificar um comando de Menu padrão](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).  
  
## <a name="defining-a-command-using-mef"></a>Definindo um Comando usando MEF  
 O Managed Extensibility Framework (MEF) fornece um método alternativo de definição de comandos de menu no menu do diagrama. Sua finalidade principal é permitir que uma DSL seja estendida por você ou por outras partes. Os usuários podem optar por instalar apenas a DSL ou podem instalar a DSL e as extensões. No entanto, o MEF também reduz o trabalho na definição de comandos de menu de atalho, após o trabalho inicial de permitir o MEF na DSL.  
  
 Use o método neste tópico se:  
  
1. Desejar definir comandos de menu nos menus que não sejam os de atalho com clique direito do mouse.  
  
2. Desejar definir agrupamentos específicos de comandos no menu.  
  
3. Não desejar permitir que outros estendam a DSL com comandos próprios.  
  
4. Desejar definir apenas um comando.  
  
   Caso contrário, considere o uso do método MEF para definir os comandos. Para obter mais informações, consulte [estender a DSL usando MEF](../modeling/extend-your-dsl-by-using-mef.md).  
  
##  <a name="VSCT"></a> Declarar o comando em Commands. VSCT  
 Os comandos de menu são declarados em DslPackage\Commands.vsct. Essas definições especificam os rótulos dos itens de menu e onde eles aparecem nos menus.  
  
 O arquivo que você edita, Commands. VSCT, importa definições de vários arquivos. h, que estão localizados no diretório *caminho de instalação do SDK do Visual Studio*\visualstudiointegration\common\inc. Ele inclui também o GeneratedVsct.vsct, que é gerado a partir de sua definição de DSL.  
  
 Para obter mais informações sobre arquivos. VSCT, consulte [tabela de comando do Visual Studio (. VSCT) arquivos](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
#### <a name="to-add-the-command"></a>Para adicionar o comando  
  
1.  Na **Gerenciador de soluções**, sob o **DslPackage** projeto, abra Commands. VSCT.  
  
2.  No elemento `Commands`, defina um ou mais botões e um grupo. Um *botão* é um item no menu. Um *grupo* é uma seção no menu. Para definir esses itens, adicione os seguintes elementos:  
  
    ```  
    <!-- Define a group - a section in the menu -->  
    <Groups>  
      <Group guid="guidCustomMenuCmdSet" id="grpidMyMenuGroup" priority="0x0100">  
        <!-- These symbols are defined in GeneratedVSCT.vsct -->  
        <Parent guid="guidCmdSet" id="menuidContext" />  
      </Group>  
    </Groups>  
    <!-- Define a button - a menu item - inside the Group -->  
    <Buttons>  
      <Button guid="guidCustomMenuCmdSet" id="cmdidMyContextMenuCommand"  
        priority="0x0100" type="Button">  
        <Parent guid="guidCustomMenuCmdSet" id="grpidMyMenuGroup"/>  
        <!-- If you do not want to place the command in your own Group,   
             use Parent guid="guidCmdSet" id="grpidContextMain".  
             These symbols are defined in GeneratedVSCT.vsct -->  
        <CommandFlag>DynamicVisibility</CommandFlag>  
        <Strings>  
          <ButtonText>My Context Menu Command</ButtonText>  
        </Strings>  
      </Button>  
    </Buttons>  
    ```  
  
    > [!NOTE]
    >  Cada botão ou grupo é identificado por um GUID e um ID do número inteiro. Você pode criar vários grupos e botões com o mesmo GUID. No entanto, eles devem ter IDs diferentes. Os nomes do GUID e ID são convertidos em GUIDs reais e IDs numéricos no `<Symbols>` nó.  
  
3.  Adicione uma restrição de visibilidade ao comando para que ele seja carregado apenas no contexto de sua linguagem específica do domínio. Para obter mais informações, consulte [Element Visibilityconstraints](../extensibility/visibilityconstraints-element.md).  
  
     Para fazer isso, adicione os seguintes elementos no elemento `CommandTable` após o elemento `Commands`.  
  
    ```  
    <VisibilityConstraints>  
      <!-- Ensures the command is only loaded for this DSL -->  
      <VisibilityItem guid="guidCustomMenuCmdSet" id="cmdidMyContextMenuCommand"  
        context="guidEditor"/>  
    </VisibilityConstraints>  
    ```  
  
4.  Defina os nomes que você usou para os GUIDs e os IDs. Para fazer isso, adicione um elemento `Symbols` no elemento `CommandTable` após o elemento `Commands`.  
  
    ```  
    <Symbols>  
      <!-- Substitute a unique GUID for the placeholder: -->  
      <GuidSymbol name="guidCustomMenuCmdSet"  
        value="{00000000-0000-0000-0000-000000000000}" >  
        <IDSymbol name="grpidMyMenuGroup" value="0x01001"/>  
        <IDSymbol name="cmdidMyContextMenuCommand" value="0x00001"/>  
      </GuidSymbol>  
    </Symbols>  
    ```  
  
5.  Substitua `{000...000}` por um GUID que identifica seus grupos e itens de menu. Para obter um novo GUID, use o **criar GUID** ferramenta sobre o **ferramentas** menu.  
  
    > [!NOTE]
    >  Se você adicionar mais grupos ou itens de menu, poderá usar o mesmo GUID. No entanto, você deve usar novos valores para o `IDSymbols`.  
  
6.  No código copiado deste procedimento, substitua toda ocorrência das seguintes cadeias de caracteres por suas próprias cadeias de caracteres:  
  
    -   `grpidMyMenuGroup`  
  
    -   `cmdidMyContextMenuCommand`  
  
    -   `guidCustomMenuCmdSet`  
  
    -   `My Context Menu Command`  
  
##  <a name="version"></a> Atualizar a versão do pacote em Package.tt  
 Sempre que você adicionar ou alterar um comando, atualize o parâmetro `version` de <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> que é aplicado à classe de pacotes antes de liberar a nova versão de sua linguagem específica do domínio.  
  
 Como a classe de pacotes é definida em um arquivo gerado, atualize o atributo no arquivo de modelo de texto que gera o arquivo Package.cs.  
  
#### <a name="to-update-the-packagett-file"></a>Para atualizar o arquivo Package.tt  
  
1.  Na **Gerenciador de soluções**, no **DslPackage** projeto, o **GeneratedCode** pasta, abra o arquivo Package.tt.  
  
2.  Localize o atributo `ProvideMenuResource`.  
  
3.  Incremente o parâmetro `version` do atributo, que é o segundo parâmetro. Se desejar, você pode escrever o nome do parâmetro explicitamente para lembrá-lo de sua finalidade. Por exemplo:  
  
     `[VSShell::ProvideMenuResource("1000.ctmenu", version: 2 )]`  
  
##  <a name="CommandSet"></a> Definir o comportamento do comando  
 Sua DSL já possui alguns comandos que são implantados em uma classe parcial que é declarada em DslPackage\GeneratedCode\CommandSet.cs. Para adicionar novos comandos, você deve estender essa classe criando um novo arquivo que contém uma declaração parcial da mesma classe. O nome da classe é normalmente  *\<YourDslName >*`CommandSet`. O mais prático é começar ao verificar o nome da classe e inspecionar o seu conteúdo.  
  
 A classe do conjunto de comandos é derivada de <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>.  
  
#### <a name="to-extend-the-commandset-class"></a>Para estender a classe CommandSet  
  
1.  No Gerenciador de Soluções, no projeto DslPackage, abra a pasta GeneratedCode e procure sob CommandSet.tt e abra o arquivo gerado CommandSet.cs. Observe o namespace e o nome da primeira classe que está definida lá. Por exemplo, é possível ver:  
  
     `namespace Company.Language1`  
  
     `{ ...  internal partial class Language1CommandSet : ...`  
  
2.  Na **DslPackage**, crie uma pasta chamada **código personalizado**. Nessa pasta, crie um novo arquivo de classe chamado `CommandSet.cs`.  
  
3.  No novo arquivo, grave uma declaração parcial que contenha o mesmo namespace e o nome que a classe parcial gerada. Por exemplo:  
  
     `namespace Company.Language1 /* Make sure this is correct */`  
  
     `{ internal partial class Language1CommandSet { ...`  
  
     **Observação** se você usou o modelo de classe para criar o novo arquivo, você deve corrigir o namespace e o nome da classe.  
  
### <a name="extend-the-command-set-class"></a>Estender a classe Conjunto de Comandos  
 Seu código do conjunto de comandos geralmente precisará importar os seguintes namespaces:  
  
```  
using System;  
using System.Collections.Generic;  
using System.ComponentModel.Design;   
using System.Linq;  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
using Microsoft.VisualStudio.Modeling.Shell;  
```  
  
 Ajuste o namespace e o nome da classe para corresponder aos encontrados no CommandSet.cs gerado:  
  
```  
namespace Company.Language1 /* Make sure this is correct */  
{  
  // Same class as the generated class.  
  internal partial class Language1CommandSet   
  {  
```  
  
 Você precisa definir dois métodos, um para determinar quando o comando ficará visível no menu de contexto e outro para executar o comando. Esses métodos não são substituições, uma vez que você os registra em uma lista de comandos.  
  
### <a name="define-when-the-command-will-be-visible"></a>Defina quando o comando estará visível  
 Para cada comando, defina um método `OnStatus...` que determina se o comando aparecerá no menu ou não e se ele estará habilitado ou acinzentado. Defina as propriedades `Visible` e `Enabled` do `MenuCommand`, conforme mostrado no exemplo a seguir. Este método é chamado para construir o menu de atalho sempre que o usuário clicar com o botão direito do mouse no diagrama, portanto, é preciso que ele funcione com rapidez.  
  
 Neste exemplo, o comando estará visível apenas quando o usuário tiver selecionado um tipo específico de formato e estará habilitado apenas quando pelo menos um dos elementos selecionados estiver em um estado específico. O exemplo se baseia no modelo DSL do Diagrama de Classe, e ClassShape e ModelClass são tipos que são definidos na DSL:  
  
```  
private void OnStatusMyContextMenuCommand(object sender, EventArgs e)  
{  
  MenuCommand command = sender as MenuCommand;  
  command.Visible = command.Enabled = false;  
  foreach (object selectedObject in this.CurrentSelection)  
  {  
    ClassShape shape = selectedObject as ClassShape;  
    if (shape != null)  
    {  
      // Visibility depends on what is selected.  
      command.Visible = true;  
      ModelClass element = shape.ModelElement as ModelClass;  
      // Enabled depends on state of selection.  
      if (element != null && element.Comments.Count == 0)  
      {  
        command.Enabled = true;  
        return; // seen enough  
} } } }  
```  
  
 Os seguintes fragmentos são geralmente úteis nos métodos OnStatus:  
  
- `this.CurrentSelection`. O formato que o usuário clicou com o botão direito do mouse estará sempre incluído nesta lista. Se o usuário clicar em uma parte em branco do diagrama, o Diagrama será o único membro da lista.  
  
- `this.IsDiagramSelected()` - `true` Se o usuário clicou em uma parte em branco do diagrama.  
  
- `this.IsCurrentDiagramEmpty()`  
  
- `this.IsSingleSelection()` - o usuário não escolheu vários objetos  
  
- `this.SingleSelection` - a forma ou o diagrama que o usuário clicou com o botão direito  
  
- `shape.ModelElement as MyLanguageElement` - o elemento de modelo representado por uma forma.  
  
  Como diretriz geral, faça com que a propriedade `Visible` dependa do que foi selecionado e faça com que a propriedade `Enabled` dependa do estado dos elementos selecionados.  
  
  Um método OnStatus não deve alterar o estado do Armazenamento.  
  
### <a name="define-what-the-command-does"></a>Defina o que o comando faz  
 Para cada comando, defina um método `OnMenu...` que execute a ação necessária quando o usuário clica no comando de menu.  
  
 Se você fizer alterações nos elementos do modelo, deverá fazer isso dentro de uma transação. Para obter mais informações, consulte [como: modificar um comando de Menu padrão](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).  
  
 Neste exemplo, `ClassShape`, `ModelClass` e `Comment` são tipos definidos na DSL, que é derivada do modelo de DSL do Diagrama de Classe.  
  
```  
private void OnMenuMyContextMenuCommand(object sender, EventArgs e)  
{  
  MenuCommand command = sender as MenuCommand;  
  Store store = this.CurrentDocData.Store;  
  // Changes to elements and shapes must be performed in a Transaction.  
  using (Transaction transaction =  
       store.TransactionManager.BeginTransaction("My command"))  
  {  
    foreach (object selectedObject in this.CurrentSelection)  
    {  
      // ClassShape is defined in my DSL.  
      ClassShape shape = selectedObject as ClassShape;  
      if (shape != null)  
      {  
        // ModelClass is defined in my DSL.  
        ModelClass element = shape.ModelElement as ModelClass;  
        if (element != null)  
        {  
          // Do required action here - for example:  
  
          // Create a new element. Comment is defined in my DSL.  
          Comment newComment = new Comment(element.Partition);  
          // Every element must be the target of an embedding link.  
          element.ModelRoot.Comments.Add(newComment);  
          // Set properties of new element.  
          newComment.Text = "This is a comment";  
          // Create a reference link to existing object.  
          element.Comments.Add(newComment);  
        }  
      }  
    }  
    transaction.Commit(); // Don't forget this!  
  }  
}  
```  
  
 Para obter mais informações sobre como navegar de um objeto para outro no modelo e sobre como criar objetos e links, consulte [como: modificar um comando de Menu padrão](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).  
  
### <a name="register-the-command"></a>Registre o comando  
 Repita em C# as declarações dos valores de GUID e de ID criados na seção Símbolos de CommandSet.vsct:  
  
```  
private Guid guidCustomMenuCmdSet =   
    new Guid("00000000-0000-0000-0000-000000000000");  
private const int grpidMyMenuGroup = 0x01001;  
private const int cmdidMyContextMenuCommand = 1;  
```  
  
 Use o mesmo valor GUID que o inserido no **Commands. VSCT**.  
  
> [!NOTE]
>  Se você alterar a seção Símbolos do arquivo VSCT, deverá também alterar essas declarações para que correspondam. Você deve também incrementar o número de versão em Package.tt  
  
 Registre os comandos de menu como parte deste conjunto de comandos. `GetMenuCommands()` é chamado uma vez quando o diagrama é iniciado:  
  
```  
protected override IList<MenuCommand> GetMenuCommands()  
{  
  // Get the list of generated commands.  
  IList<MenuCommand> commands = base.GetMenuCommands();  
  // Add a custom command:  
  DynamicStatusMenuCommand myContextMenuCommand =  
    new DynamicStatusMenuCommand(  
      new EventHandler(OnStatusMyContextMenuCommand),  
      new EventHandler(OnMenuMyContextMenuCommand),  
      new CommandID(guidCustomMenuCmdSet, cmdidMyContextMenuCommand));  
  commands.Add(myContextMenuCommand);  
  // Add more commands here.  
  return commands;  
}   
```  
  
## <a name="test-the-command"></a>Testar o comando  
 Compile e execute a DSL em uma instância experimental do Visual Studio. O comando deve aparecer no menu de atalho nas situações especificadas.  
  
#### <a name="to-exercise-the-command"></a>Para exercitar o comando  
  
1.  Sobre o **Gerenciador de soluções** barra de ferramentas, clique em **transformar todos os modelos**.  
  
2.  Pressione **F5** para recompilar a solução e iniciar a depuração de linguagem específica de domínio na compilação experimental.  
  
3.  Na compilação experimental, abra o diagrama de amostra.  
  
4.  Clique com o botão direito do mouse em vários itens do diagrama para verificar se o comando está habilitado ou desabilitado corretamente e exibido ou oculto de maneira apropriada, dependendo do item escolhido.  
  
## <a name="troubleshooting"></a>Solução de problemas  
 **Comando não aparecer no menu:**  
  
- O comando aparecerá apenas nas instâncias de depuração do Visual Studio até você instalar o pacote DSL. Para obter mais informações, consulte [implantar soluções de linguagem específica do domínio](../modeling/deploying-domain-specific-language-solutions.md).  
  
- Verifique se a sua amostra experimental tem a extensão de nome de arquivo correta para esta DSL. Para verificar a extensão do nome do arquivo, abra DslDefinition.dsl na instância principal do Visual Studio. Em seguida, no Gerenciador de DSL, clique com o botão direito do mouse no nó Editor e clique em Propriedades. Na janela Propriedades, examine a propriedade FileExtension.  
  
- Você [incrementar o número de versão do pacote](#version)?  
  
- Defina um ponto de interrupção no início do método OnStatus. Ele deve ser interrompido quando você clicar com o botão direito do mouse em qualquer parte do diagrama.  
  
   **Método OnStatus não é chamado**:  
  
  -   Verifique se os GUIDs e IDs em seu código CommandSet correspondem aos presentes na seção Símbolos de Commands.vsct.  
  
  -   Em Commands.vsct, verifique se o GUID e o ID em cada nó pai identificam o grupo pai correto.  
  
  -   Em um prompt de comando do Visual Studio, digite devenv /rootsuffix exp /setup. Em seguida, reinicie a instância de depuração do Visual Studio.  
  
- Repasse o método OnStatus para verificar se command.Visible e command.Enabled estão definidos como true.  
  
  **Texto de menu incorreto é exibido ou o comando aparece no lugar errado**:  
  
- Certifique-se de que a combinação de GUID e ID seja exclusiva para este comando.  
  
- Certifique-se de que você tenha desinstalado as versões anteriores do pacote.  
  
## <a name="see-also"></a>Consulte também  
 [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)   
 [Como: modificar um comando de Menu padrão](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)   
 [Implantando soluções de linguagem específica do domínio](../modeling/deploying-domain-specific-language-solutions.md)   
 [Código de amostra: diagramas de circuito](http://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)



