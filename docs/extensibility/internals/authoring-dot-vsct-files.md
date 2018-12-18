---
title: Criação de páginas. Arquivos de VSCT | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, manual authoring
ms.assetid: e9f715dc-12b7-439b-bdf3-f3dc75e62f1c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 26a5353531d997ad40b913b5ee223614d6517c55
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49917800"
---
# <a name="author-vsct-files"></a>Arquivos. VSCT de autor
Este documento mostra como criar uma *VSCT* arquivo para adicionar itens de menu, barras de ferramentas e outros elementos de (UI) de interface do usuário ao ambiente de desenvolvimento integrado (IDE) do Visual Studio. Use estas etapas quando você adiciona elementos de interface do usuário a um pacote do Visual Studio (VSPackage) que ainda não tem um *VSCT* arquivo.  
  
 Para novos projetos, é recomendável que você use o modelo de pacote do Visual Studio porque ele gera uma *VSCT* arquivo que, dependendo de suas seleções, já tem os elementos necessários para um comando de menu, uma janela de ferramentas ou um editor personalizado . Você pode modificar essa *VSCT* arquivo para atender aos requisitos de seu VSPackage. Para obter mais informações sobre como modificar um *VSCT* arquivos, consulte os exemplos [estendem os menus e comandos](../../extensibility/extending-menus-and-commands.md).  
  
## <a name="author-the-file"></a>Crie o arquivo  
 Autor de um *VSCT* arquivo nessas fases: criar a estrutura de arquivos e recursos, declarar os elementos da interface do usuário, colocar os elementos de interface do usuário no IDE e adicione todos os comportamentos especializados.  
  
### <a name="file-structure"></a>Estrutura de arquivos  
 A estrutura básica de um *VSCT* arquivo é um [CommandTable](../../extensibility/commandtable-element.md) elemento raiz que contém um [comandos](../../extensibility/commands-element.md) elemento e um [símbolos](../../extensibility/symbols-element.md) elemento.  
  
#### <a name="to-create-the-file-structure"></a>Para criar a estrutura de arquivo  
  
1.  Adicionar um *VSCT* ao seu projeto seguindo as etapas em [como: criar um arquivo. VSCT](../../extensibility/internals/how-to-create-a-dot-vsct-file.md).  
  
2. Adicione os namespaces necessários para o `CommandTable` elemento, conforme mostrado no exemplo a seguir:  
  
    ```xml  
    <CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable"   
        xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  
    ```  
  
3.  No `CommandTable` elemento, adicionar um `Commands` elemento para hospedar todos os seus menus personalizados, barras de ferramentas, grupos de comando e comandos. Para que podem carregar seus elementos de interface do usuário personalizados, o `Commands` elemento deve ter seu `Package` atributo definido como o nome do pacote.  
  
     Após o `Commands` elemento, adicionar um `Symbols` elemento para definir os GUIDs para o pacote e os nomes e IDs de comando para elementos de interface do usuário.  
  
### <a name="include-visual-studio-resources"></a>Incluir recursos do Visual Studio  
 Use o [Extern](../../extensibility/extern-element.md) elemento para acessar os arquivos que definem os comandos do Visual Studio e os menus que são necessárias para colocar os elementos de interface do usuário no IDE. Se você usar comandos definidos fora do seu pacote, use o [UsedCommands](../../extensibility/usedcommands-element.md) elemento para informar ao Visual Studio.  
  
#### <a name="to-include-visual-studio-resources"></a>Para incluir recursos do Visual Studio  
  
1. Na parte superior da `CommandTable` elemento, adicione uma `Extern` elemento para cada arquivo externo a ser referenciada e definir o `href` de atributo para o nome do arquivo. Você pode referenciar os seguintes arquivos de cabeçalho para acessar os recursos do Visual Studio:  
  
   -   *Stdidcmd.h*: define o IDs para todos os comandos expostos pelo Visual Studio.  
  
   -   *Vsshlids.h*: contém as IDs de comando para menus do Visual Studio.  
  
2. Se o pacote chamar todos os comandos que são definidos pelo Visual Studio ou por outros pacotes, adicione uma `UsedCommands` elemento após o `Commands` elemento. Preencher esse elemento com um [UsedCommand](../../extensibility/usedcommand-element.md) elemento para cada comando, ou seja, você chama não faz parte do seu pacote. Defina as `guid` e `id` atributos do `UsedCommand` elementos para os valores GUID e ID dos comandos para chamar. 

   Para obter mais informações sobre como localizar os comandos de GUIDs e IDs do Visual Studio, consulte [comandos GUIDs e IDs do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md). Para chamar comandos de outros pacotes, use o GUID e a ID do comando conforme definido na *VSCT* arquivo para esses pacotes.
  
### <a name="declare-ui-elements"></a>Declarar elementos de interface do usuário  
 Declarar todos os novos elementos de interface do usuário na `Symbols` seção o *VSCT* arquivo.  
  
#### <a name="to-declare-ui-elements"></a>Para declarar os elementos de interface do usuário  
  
1.  No `Symbols` elemento, adicione três [GuidSymbol](../../extensibility/guidsymbol-element.md) elementos. Cada `GuidSymbol` elemento tem um `name` atributo e um `value` atributo. Defina o `name` para que ele reflita o propósito do elemento de atributo. O `value` atributo utiliza um GUID. (Para gerar um GUID, o **ferramentas** menu, selecione **criar GUID**e, em seguida, selecione **formato de registro**.)  
  
     A primeira `GuidSymbol` elemento representa seu pacote e geralmente não tem filhos. O segundo `GuidSymbol` element representa o comando definido e irá conter todos os símbolos que definem seus menus, grupos e comandos. O terceiro `GuidSymbol` elemento representa seu repositório de imagens e contém símbolos para todos os ícones para seus comandos. Se você não tiver nenhum comando que usam ícones, você pode omitir o terceiro `GuidSymbol` elemento.  
  
2.  No `GuidSymbol` elemento que representa o conjunto de comandos, adicione um ou mais [IDSymbol](../../extensibility/idsymbol-element.md) elementos. Cada um deles representa um menu, barra de ferramentas, grupo ou comando que você está adicionando à interface do usuário.  
  
     Para cada `IDSymbol` elemento, defina a `name` do atributo para o nome que você usará para se referir ao comando, grupo ou menu correspondente e, em seguida, defina o `value` elemento em um número hexadecimal que representarão seu ID de comando. Não existem dois `IDSymbol` elementos que têm o mesmo pai podem ter o mesmo valor.  
  
3.  Se qualquer um de seus elementos de interface do usuário exigir ícones, adicione uma `IDSymbol` elemento para cada ícone para o `GuidSymbol` elemento que representa o repositório de imagens.  
  
### <a name="put-ui-elements-in-the-ide"></a>Colocar os elementos de interface do usuário no IDE  
 O [Menus](../../extensibility/menus-element.md), [grupos](../../extensibility/groups-element.md), e [botões](../../extensibility/buttons-element.md) elementos contêm as definições para todos os menus, grupos e comandos que são definidos em seu pacote. Coloque esses menus, grupos e comandos no IDE usando um [pai](../../extensibility/parent-element.md) elemento, que é parte da definição de elemento de interface do usuário, ou usando uma [CommandPlacement](../../extensibility/commandplacement-element.md) elemento que é definida em outro lugar.  
  
 Cada `Menu`, `Group`, e `Button` elemento tem um `guid` atributo e um `id` atributo. Sempre definido o `guid` atributo para corresponder ao nome da `GuidSymbol` elemento que representa o comando definido e defina o `id` atributo com o nome do `IDSymbol` elemento que representa o menu, grupo ou comando em que o `Symbols`seção.  
  
#### <a name="to-define-ui-elements"></a>Para definir os elementos de interface do usuário  
  
1. Se você estiver definindo quaisquer novos menus, submenus, menus de atalho ou barras de ferramentas, adicione uma `Menus` elemento para o `Commands` elemento. Em seguida, para cada menu a ser criado, adicione uma [menus](../../extensibility/menu-element.md) elemento para o `Menus` elemento.  
  
    Defina a `guid` e `id` atributos da `Menu` elemento e, em seguida, defina o `type` de atributo para o tipo de menu que você deseja. Você também pode definir o `priority` atributo para estabelecer a posição relativa do menu do grupo pai.  
  
   > [!NOTE]
   >  O `priority` atributo não é aplicável a barras de ferramentas e menus de contexto.  
  
2. Todos os comandos no IDE do Visual Studio devem ser hospedados por grupos de comando, que são filhos diretos de menus e barras de ferramentas. Se você estiver adicionando novos menus ou barras de ferramentas ao IDE, eles devem contêm novos grupos de comando. Você também pode adicionar grupos de comando para menus e barras de ferramentas existentes, você pode agrupar visualmente seus comandos.  
  
    Quando você adiciona novos grupos de comando, você deve primeiro criar uma `Groups` elemento e, em seguida, adicione a ela um [grupo](../../extensibility/group-element.md) elemento para cada grupo de comando.  
  
    Defina as `guid` e `id` atributos de cada `Group` elemento e, em seguida, defina o `priority` atributo para estabelecer a posição relativa do grupo no menu pai. Para obter mais informações, consulte [criar grupos reutilizáveis de botões](../../extensibility/creating-reusable-groups-of-buttons.md).  
  
3. Se você estiver adicionando novos comandos ao IDE, adicione uma `Buttons` elemento para o `Commands` elemento. Em seguida, para cada comando, adicione uma [botão](../../extensibility/button-element.md) elemento para o `Buttons` elemento.  
  
   1.  Defina a `guid` e `id` atributos de cada `Button` elemento e, em seguida, defina o `type` de atributo para o tipo de botão desejado. Você também pode definir o `priority` atributo para estabelecer a posição relativa do comando no grupo pai.  
  
       > [!NOTE]
       >  Use `type="button"` para comandos de menu padrão e os botões em barras de ferramentas.  
  
   2.  No `Button` elemento, adicione uma [cadeias de caracteres](../../extensibility/strings-element.md) elemento que contém um [ButtonText](../../extensibility/buttontext-element.md) elemento e uma [CommandName](../../extensibility/commandname-element.md) elemento. O `ButtonText` elemento fornece o rótulo de texto para um item de menu ou a dica de ferramenta para um botão de barra de ferramentas. O `CommandName` elemento fornece o nome do comando para usar o comando também.  
  
   3.  Se o comando terá um ícone, crie uma [ícone](../../extensibility/icon-element.md) elemento na `Button` elemento e o conjunto de seus `guid` e `id` atributos para o `Bitmap` elemento para o ícone.  
  
       > [!NOTE]
       >  Botões da barra de ferramentas devem ter ícones.  
  
   Para obter mais informações, consulte [MenuCommands vs. OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md).  
  
4. Se qualquer um dos seus comandos exigem ícones, adicione uma [Bitmaps](../../extensibility/bitmaps-element.md) elemento para o `Commands` elemento. Em seguida, para cada ícone, adicione uma [Bitmap](../../extensibility/bitmap-element.md) elemento para o `Bitmaps` elemento. Isso é onde você pode especificar o local do recurso de bitmap. Para obter mais informações, consulte [adicionar ícones a comandos de menu](../../extensibility/adding-icons-to-menu-commands.md).  
  
   Você pode contar com a estrutura de gerenciamento do domínio pai para posicionar corretamente a maioria dos menus, grupos e comandos. Para conjuntos de comando muito grandes, ou quando um menu, o grupo ou o comando deve aparecer em vários locais, recomendamos que você especifique o posicionamento do comando.  
  
#### <a name="to-rely-on-parenting-to-place-ui-elements-in-the-ide"></a>Contar paternidade para colocar elementos de interface do usuário no IDE  
  
1. Para paternidade típica, crie uma `Parent` elemento em cada `Menu`, `Group`, e `Command` elemento que é definido em seu pacote.  
  
    O destino do `Parent` elemento é o menu ou grupo que contém o menu, grupo ou comando.  
  
   1.  Defina a `guid` de atributo para o nome da `GuidSymbol` elemento que define o conjunto de comandos. Se o elemento de destino não é parte do seu pacote, use o guid para esse conjunto de comandos, conforme definido em correspondente *VSCT* arquivo.  
  
   2.  Defina a `id` atributo para corresponder a `id` atributo do grupo ou menu de destino. Para obter uma listagem dos menus e grupos que são expostos pelo Visual Studio, consulte [menus GUIDs e IDs do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md) ou [barras de ferramentas GUIDs e IDs do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md).  
  
   Se você tiver um grande número de elementos de interface do usuário para colocar no IDE, ou se você tiver elementos que devem aparecer em vários lugares, defina seus posicionamentos na [CommandPlacements](../../extensibility/commandplacements-element.md) elemento, conforme mostrado nas etapas a seguir.  
  
#### <a name="to-use-command-placement-to-place-ui-elements-in-the-ide"></a>Para usar o posicionamento de comando para colocar elementos de interface do usuário no IDE  
  
1. Após o `Commands` elemento, adicionar um `CommandPlacements` elemento.  
  
2. No `CommandPlacements` elemento, adicionar um `CommandPlacement` elemento para cada menu, um grupo ou um comando para colocar.  
  
    Cada `CommandPlacement` elemento ou `Parent` elemento coloca um menu, grupo ou comando em um local de IDE. Um elemento de interface do usuário pode ter apenas um pai, mas pode ter vários posicionamentos de comandos. Para colocar um elemento de interface do usuário em vários locais, adicione um `CommandPlacement` elemento para cada local.  
  
3. Defina as `guid` e `id` atributos de cada `CommandPlacement` elemento para o menu de hospedagem ou grupo, assim como você faria para um `Parent` elemento. Você também pode definir o `priority` atributo para estabelecer a posição relativa do elemento de interface do usuário.  
  
   Você pode misturar posicionamento por paternidade e posicionamento do comando. No entanto, para conjuntos de comando muito grandes, é recomendável que você use somente o posicionamento de comando.  
  
### <a name="add-specialized-behaviors"></a>Adicionar comportamentos especializados  
 Você pode usar o [CommandFlag](../../extensibility/command-flag-element.md) elemento para modificar o comportamento de menus e comandos, por exemplo, para alterar sua aparência e a visibilidade. Você também pode afetar quando um comando estiver visível, usando o [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) elemento, ou adicionar atalhos de teclado usando o [KeyBindings](../../extensibility/keybindings-element.md) elemento. Determinados tipos de menus e comandos já tem especializadas comportamentos internos.  
  
#### <a name="to-add-specialized-behaviors"></a>Para adicionar comportamentos especializados  
  
1. Para tornar um elemento de interface do usuário visível apenas em determinados contextos de interface do usuário, por exemplo, quando uma solução é carregada, use restrições de visibilidade.  
  
   1.  Após o `Commands` elemento, adicionar um `VisibilityConstraints` elemento.  
  
   2.  Para cada item de interface do usuário restringir, adicione uma [VisibilityItem](../../extensibility/visibilityitem-element.md) elemento.  
  
   3.  Para cada `VisibilityItem` elemento, defina a `guid` e `id` atributos para o menu, grupo, ou comando e defina o `context` atributo para o contexto de interface do usuário desejado, conforme definido no <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> classe.   
  
2. Para definir a visibilidade ou a disponibilidade de um item de interface do usuário no código, use um ou mais dos seguintes sinalizadores de comando:  
  
   -   `DefaultDisabled`
  
   -   `DefaultInvisible`
  
   -   `DynamicItemStart` 
  
   -   `DynamicVisibility`
  
   -   `NoShowOnMenuController`
  
   -   `NotInTBList`
  
   Para obter mais informações, consulte o [CommandFlag](../../extensibility/command-flag-element.md) elemento.  
  
3. Para alterar como um elemento aparece ou alterar sua aparência dinamicamente, use um ou mais dos seguintes sinalizadores de comando:  
  
   -   `AlwaysCreate`  
  
   -   `CommandWellOnly`  
  
   -   `DefaultDocked`  
  
   -   `DontCache`  
  
   -   `DynamicItemStart`  
  
   -   `FixMenuController`  
  
   -   `IconAndText`  
  
   -   `Pict`  
  
   -   `StretchHorizontally`  
  
   -   `TextMenuUseButton`  
  
   -   `TextChanges`  
  
   -   `TextOnly`  
  
   Para obter mais informações, consulte o [CommandFlag](../../extensibility/command-flag-element.md) elemento.  
  
4. Para alterar o modo como um elemento reage quando ele recebe comandos, use um ou mais dos seguintes sinalizadores de comando:  
  
   -   `AllowParams`  
  
   -   `CaseSensitive`  
  
   -   `CommandWellOnly`  
  
   -   `FilterKeys`  
  
   -   `NoAutoComplete`  
  
   -   `NoButtonCustomize`  
  
   -   `NoKeyCustomize`  
  
   -   `NoToolbarClose`  
  
   -   `PostExec`  
  
   -   `RouteToDocs`  
  
   -   `TextIsAnchorCommand`  
  
   Para obter mais informações, consulte o [CommandFlag](../../extensibility/command-flag-element.md) elemento.  
  
5. Para anexar um atalho de teclado dependente de menu a um menu ou um item em um menu, adicione um caractere e comercial (&) no `ButtonText` elemento para o menu ou item de menu. O caractere que segue o e comercial é o atalho de teclado ativo quando o menu pai é aberto.  
  
6. Para anexar um atalho de teclado do menu independente a um comando, use o [KeyBindings](../../extensibility/keybindings-element.md) elemento. Para obter mais informações, consulte o [KeyBinding](../../extensibility/keybinding-element.md) elemento.  
  
7. Para localizar o texto de menu, use o `LocCanonicalName` elemento. Para obter mais informações, consulte o [cadeias de caracteres](../../extensibility/strings-element.md) elemento.  
  
   Alguns tipos de menu e botão incluem comportamentos especializados. A lista a seguir descreve alguns menu especializada e tipos de botão. Para outros tipos, consulte a `types` descrições de atributo o [Menu](../../extensibility/menu-element.md), [botão](../../extensibility/button-element.md), e [combinação](../../extensibility/combo-element.md) elementos.  
  
   - Caixa de combinação:  
   Uma caixa de combinação é uma lista suspensa que pode ser usada em uma barra de ferramentas. Para adicionar caixas de combinação na interface do usuário, crie uma [Combos](../../extensibility/combos-element.md) elemento o `Commands` elemento. Em seguida, adicione para o `Combos` elemento um `Combo` elemento para cada caixa de combinação adicionar. `Combo` elementos têm os mesmos atributos e filhos como `Button` elementos e também ter `DefaultWidth` e `idCommandList` atributos. O `DefaultWidth` atributo define a largura em pixels e o `idCommandList` pontos do atributo a uma ID de comando que é usada para preencher a caixa de combinação. 
  
   - Controlador de menu:  
   Um controlador de menu é um botão que tem uma seta ao lado dele. Clique na seta abre uma lista. Para adicionar um controlador de menu na interface do usuário, crie uma `Menu` elemento e o conjunto de seus `type` atributo `MenuController` ou `MenuControllerLatched`, dependendo do comportamento desejado. Para popular um controlador de menu, defina-a como o pai de um `Group` elemento. O controlador de menu exibirá todos os filhos desse grupo em sua lista suspensa.  
  
## <a name="see-also"></a>Consulte também  
 [Ampliar menus e comandos](../../extensibility/extending-menus-and-commands.md)   
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Referência de esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md)