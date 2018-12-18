---
title: GUIDs e IDs de comandos do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 35e2c354293679d9cb6044b0c5f21b77aadb7f52
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220154"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Comandos de GUIDs e IDs do Visual Studio
Os valores GUID e ID dos comandos incluídos no ambiente de desenvolvimento integrado (IDE) do Visual Studio são definidos em arquivos. VSCT que são instalados como parte do SDK do Visual Studio. Para obter mais informações, consulte [definidos pelo IDE comandos, menus e grupos](../../extensibility/internals/ide-defined-commands-menus-and-groups.md).  
  
 Para obter mais informações sobre como trabalhar com objetos IDE que são definidos no *VSCT* arquivos, consulte [estendem os menus e comandos](../../extensibility/extending-menus-and-commands.md).  
  
## <a name="find-a-command-definition"></a>Encontrar uma definição de comando  
 Como o Visual Studio define mais de 1000 comandos, não é prático para listá-los tudo aqui. Em vez disso, siga estas etapas para localizar a definição de um comando.  
  
### <a name="to-locate-a-command-definition"></a>Para localizar uma definição de comando  
  
1. No Visual Studio, abra os arquivos a seguir na *< caminho de instalação do SDK do Visual Studio\>\visualstudiointegration\common\inc.\\*  pasta: *SharedCmdDef.vsct*, *ShellCmdDef.vsct*, *VsDbgCmdUsed.vsct*, *Venusmenu.vsct*.  
  
    A maioria dos comandos do Visual Studio são definidos no *SharedCmdDef.vsct* e *ShellCmdDef.vsct*. *VsDbgCmdUsed.vsct* define os comandos que pertencem ao depurador, e *Venusmenu.vsct* define os comandos que são específicos para o desenvolvimento Web.  
  
2. Se o comando é um item de menu, observe o texto exato do item de menu. Se o comando é um botão em uma barra de ferramentas, observe o texto de dica de ferramenta que aparece quando você pausa nela.  
  
3. Pressione **Ctrl**+**F** para abrir o **localizar** caixa de diálogo.  
  
4. No **localizar** , digite o texto que você anotou na etapa 2.  
  
5. Verifique **todos os documentos abertos** é exibido na **examinar** caixa.  
  
6. Clique no **Localizar próxima** botão até que o texto é selecionado na `<Strings>` seção de uma [elemento Button](../../extensibility/button-element.md).  
  
    O `<Button>` elemento que o comando é exibido no é a definição de comando.  
  
   Depois de encontrar a definição de comando, você pode colocar uma cópia do comando em outro menu ou barra de ferramentas com a criação de um [elemento CommandPlacement](../../extensibility/commandplacement-element.md) que tem o mesmo `guid` e `id` valores como o comando. Para obter mais informações, consulte [criar grupos reutilizáveis de botões](../../extensibility/creating-reusable-groups-of-buttons.md).  
  
### <a name="special-cases"></a>Casos especiais  
 Nos casos a seguir, o texto de menu ou o texto de dica de ferramenta pode não corresponder exatamente o que está na definição de comando.  
  
-   Itens de menu que incluem um caractere de sublinhado, como o **Print** comando o **arquivo** menu, em que o *P* está sublinhado.  
  
     Caracteres que são precedidos por um e comercial (&) caractere em nomes de item de menu são exibidas como sublinhado. No entanto, *VSCT* arquivos são gravados em XML, que usa o caractere e comercial (&) para indicar caracteres especiais e requer que um e comercial a ser exibido deve ser escrito como  *&amp;amp;*. Portanto, em um *VSCT* arquivo, o **impressão** comando aparece como  *&amp;amp; Impressão*.  
  
-   Comandos que contêm texto dinâmico, como **salve** \<nome do arquivo atual\>e gerado dinamicamente os itens de menu, como os itens no **arquivos recentes** lista.  
  
     Não há nenhuma maneira confiável para pesquisar texto dinâmico. Em vez disso, localizar um grupo que hospeda o comando desejado por consultoria [menus GUIDs e IDs do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md) ou [barras de ferramentas GUIDs e IDs do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)e procure a ID do grupo. Se a definição de comando não tem o grupo como seu [elemento pai](../../extensibility/parent-element.md), search *SharedCmdPlace.vsct* e *ShellCmdPlace.vsct* (ou  *VsDbgCmdPlace.vsct* para comandos de depurador) para um `<CommandPlacement>` elemento que define o pai do comando. *SharedCmdPlace.vsct*, *ShellCmdPlace.vsct*, e *VsDbgCmdPlace.vsct* estão no *\<caminho de instalação do SDK do Visual Studio\>\ VisualStudioIntegration\Common\Inc\\* pasta.  
  
## <a name="see-also"></a>Consulte também  
 [MenuCommands vs. OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md)   
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Referência de esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md)
