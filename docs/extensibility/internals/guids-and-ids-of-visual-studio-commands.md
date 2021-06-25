---
title: GUIDs e IDs de comandos do Visual Studio | Microsoft Docs
description: Saiba como localizar o GUID e os valores de ID dos comandos incluídos no IDE (ambiente de desenvolvimento integrado) do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8442e6430ead8f28d2afc7f51d14968b6999fcd9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898273"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>GUIDs e IDs de comandos do Visual Studio
Os valores de GUID e ID dos comandos incluídos no IDE (ambiente de desenvolvimento integrado) do Visual Studio são definidos em arquivos. vsct que são instalados como parte do SDK do Visual Studio. Para obter mais informações, consulte [comandos, menus e grupos definidos pelo IDE](../../extensibility/internals/ide-defined-commands-menus-and-groups.md).

 Para obter mais informações sobre como trabalhar com objetos IDE definidos em arquivos *. vsct* , consulte [estender menus e comandos](../../extensibility/extending-menus-and-commands.md).

## <a name="find-a-command-definition"></a>Localizar uma definição de comando
 Como o Visual Studio define mais de 1000 comandos, é impraticável listá-los aqui. Em vez disso, siga estas etapas para localizar a definição de um comando.

### <a name="to-locate-a-command-definition"></a>Para localizar uma definição de comando

1. No Visual Studio, abra os seguintes arquivos na pasta *<caminho de instalação do SDK do Visual Studio \> \VisualStudioIntegration\Common\Inc \\* : *SharedCmdDef. vsct*, *ShellCmdDef. vsct*, *VsDbgCmdUsed. vsct*, *Venusmenu. vsct*.

    A maioria dos comandos do Visual Studio são definidos em *SharedCmdDef. vsct* e *ShellCmdDef. vsct*. *VsDbgCmdUsed. vsct* define os comandos que pertencem ao depurador, e *Venusmenu. vsct* define os comandos que são específicos do desenvolvimento para a Web.

2. Se o comando for um item de menu, observe o texto exato do item de menu. Se o comando for um botão em uma barra de ferramentas, observe o texto da dica de ferramenta que aparece quando você pausa nele.

3. Pressione **Ctrl** + **F** para abrir a caixa de diálogo **Localizar** .

4. Na caixa **Localizar** , digite o texto que você anotou na etapa 2.

5. Verifique se **todos os documentos abertos** são exibidos na caixa **examinar** .

6. Clique no botão **Localizar próximo** até que o texto seja selecionado na `<Strings>` seção de um [elemento de botão](../../extensibility/button-element.md).

    O `<Button>` elemento no qual o comando aparece é a definição do comando.

   Quando você encontrar a definição de comando, poderá colocar uma cópia do comando em outro menu ou barra de ferramentas criando um [elemento CommandPlacement](../../extensibility/commandplacement-element.md) que tenha o mesmo `guid` valor e os mesmos valores que `id` o comando. Para obter mais informações, consulte [criar grupos de botões reutilizáveis](../../extensibility/creating-reusable-groups-of-buttons.md).

### <a name="special-cases"></a>Casos especiais
 Nos casos a seguir, o texto do menu ou a dica de ferramenta pode não corresponder exatamente ao que está na definição de comando.

- Itens de menu que incluem um caractere sublinhado, como o comando **Imprimir** no menu **arquivo** , no qual o *P* é sublinhado.

     Os caracteres precedidos pelo caractere de e comercial (&) em nomes de itens de menu são exibidos como sublinhados. No entanto, os arquivos *. vsct* são gravados em XML, que usa o caractere de e comercial (&) para indicar caracteres especiais e requer que um e comercial seja exibido deve ser escrito como *&amp; amp;*. Portanto, em um arquivo *. vsct* , o comando **Print** é exibido como *&amp; amp; Imprimir*.

- Comandos que têm texto dinâmico, como **salvar** \<Current Filename\> e itens de menu gerados dinamicamente, como os itens na lista de **arquivos recentes** .

     Não há uma maneira confiável de Pesquisar texto dinâmico. Em vez disso, localize um grupo que hospede o comando desejado por [GUIDs de consultoria e IDs de menus](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md) ou [GUIDs do Visual Studio e IDs das barras de ferramentas do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)e pesquise a ID desse grupo. Se a definição do comando não tiver o grupo como seu [elemento pai](../../extensibility/parent-element.md), pesquise *SharedCmdPlace. vsct* e *ShellCmdPlace. vsct* (ou *VsDbgCmdPlace. vsct* para comandos do depurador) para um `<CommandPlacement>` elemento que defina o pai do comando. *SharedCmdPlace. vsct*, *ShellCmdPlace. vsct* e *VsDbgCmdPlace. vsct* estão na pasta *\<Visual Studio SDK installation path\> \VisualStudioIntegration\Common\Inc \\* .

## <a name="see-also"></a>Confira também

- [Arquivos de tabela de comando do Visual Studio (. vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Referência de esquema XML VSCT](../../extensibility/vsct-xml-schema-reference.md)
