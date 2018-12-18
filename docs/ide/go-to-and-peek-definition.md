---
title: Exibindo definições de tipo no Visual Studio
ms.date: 01/10/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code editor, view definition
- go to definition
- peek definition
- type definition [Visual Studio]
- member definition [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 529486e39db57228feb703817eea44fab9399c85
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34745757"
---
# <a name="view-type-and-member-definitions"></a>Exibir Definições de Membro e de Tipo

Os desenvolvedores normalmente precisam exibir as definições de código de origem para tipos ou membros de classe que eles usam no código. No Visual Studio, os recursos **Ir para Definição** e **Espiar Definição** permitem exibir facilmente a definição de um tipo ou membro. Se o código-fonte não estiver disponível, os metadados serão exibidos no lugar.

## <a name="go-to-definition"></a>Ir para definição

O recurso **Ir para Definição** navega para a fonte de um tipo ou membro e abre o resultado em uma nova guia. Se você estiver usando um teclado, coloque o cursor de texto em algum lugar dentro do nome do símbolo e pressione **F12**. Se você estiver usando um mouse, selecione **Ir para Definição** no menu de contexto ou use a funcionalidade **Ctrl + clique** descrita na seção a seguir.

### <a name="ctrl-click-go-to-definition"></a>CTRL + clique para Ir para Definição

No Visual Studio 2017 versão 15.4, há uma maneira mais fácil para os usuários de mouse acessarem **Ir para Definição** rapidamente. Os símbolos tornam-se clicáveis quando você pressiona **Ctrl** e passa o mouse sobre o tipo ou membro. Para navegar rapidamente para a definição de um símbolo, pressione a tecla **Ctrl** e, em seguida, clique nele. É fácil assim!

![Animação de Ir para Definição com o clique do mouse](../ide/media/click_gotodef.gif)

Você pode alterar a tecla modificadora do clique do mouse para **Ir para Definição** acessando **Ferramentas** > **Opções** > **Editor de Texto** > **Geral** e selecionando **Alt** ou **Ctrl+Alt** na lista suspensa **Usar tecla modificadora**. Você também pode desabilitar o clique do mouse para **Ir para Definição** desmarcando a caixa de seleção **Habilitar clique do mouse para Ir para Definição**.

![Habilitando o clique do mouse para Ir para Definição](../ide/media/editor_options_mouse_click_gotodef.png)

## <a name="peek-definition"></a>Inspecionar Definição

O recurso **Espiar Definição** permite visualizar a definição de um tipo sem sair do local atual no editor. Se você estiver usando um teclado, coloque o cursor de texto em algum lugar dentro do nome do tipo ou do membro e pressione **Alt + F12**. Se você estiver usando um mouse, selecione **Espiar Definição** no menu de contexto. No Visual Studio 2017 versão 15.4 e posteriores, há uma nova maneira de espiar a exibição de uma definição usando o mouse. Primeiro, vá até **Ferramentas** > **Opções** > **Editor de Texto** > **Geral**. Selecione a opção **Abrir definição na espiada de exibição** e clique em **OK** para fechar a caixa de diálogo **Opções**.

![Configurando a opção de espiar definição com o clique do mouse](../ide/media/editor_options_peek_view.png)

Em seguida, pressione **Ctrl** (ou qualquer outra tecla modificadora que estiver selecionada em **Opções**) e clique no tipo ou no membro.

![Animação de espiar definição](../ide/media/peek_definition.gif)

Se você inspecionar outra definição da janela pop-up, iniciará um caminho de navegação estrutural no qual poderá navegar usando os círculos e setas que aparecem acima da janela pop-up.

Para obter mais informações, consulte [Como exibir e editar códigos usando Inspecionar Definição (Alt + F12)](how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md).

## <a name="view-metadata-as-source-code-c"></a>Exibir metadados como código de origem (C#)

Quando você exibe a definição de tipos ou membros de C# cujo código-fonte não está disponível, seus metadados são exibido no lugar. Você pode ver as declarações de tipos e membros, mas não suas implementações.

Quando você executa o comando **Ir para Definição** ou **Inspecionar Definição** para um item cujo código-fonte está indisponível, um documento com guias que contém uma exibição dos metadados do item, exibidos como código-fonte, ele é exibido no editor de códigos. O nome do tipo, seguido por **[de metadados]**, aparece na guia do documento.

Por exemplo, se você executar o comando **Ir para Definição** para o <xref:System.Console>, os metadados para o <xref:System.Console> aparecerão no editor de código como o código-fonte de C#. O código será semelhante a sua declaração, mas não exibirá uma implementação.

![Metadados como origem](../ide/media/metadatasource.png)

> [!NOTE]
> Quando você tenta executar o comando **Ir para Definição** ou **Inspecionar Definição** para tipos ou membros que estão marcados como internos, o Visual Studio não exibe seus metadados como código-fonte, independentemente se o assembly de referência for um amigo ou não.

### <a name="view-decompiled-source-definitions-instead-of-metadata-c"></a>Exibir definições de fonte descompilada em vez de metadados (C#)

Novidade na No Visual Studio 2017 versão 15.6, você pode definir uma opção para ver o código-fonte descompilado quando exibir a definição de um tipo ou membro de C# cujo código-fonte não está disponível. Para ativar esse recurso, escolha **Ferramentas** > **Opções** na barra de menus. Em seguida, expanda **Editor de Texto** > **C#** > **Avançado**e selecione **Habilitar navegação para fontes descompiladas**.

![Exibindo uma definição descompilada](media/go-to-definition-decompiled-sources.png)

> [!NOTE]
> O Visual Studio reconstrói corpos de método usando a descompilação ILSpy. Na primeira vez que você acessar esse recurso, deverá concordar com uma isenção de responsabilidade sobre leis de direitos autorais de marcas e licenciamento de software.

## <a name="see-also"></a>Consulte também

- [Navegar pelo código](../ide/navigating-code.md)
- [Como exibir e editar códigos usando a janela Inspecionar Definição (Alt+F12)](how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)