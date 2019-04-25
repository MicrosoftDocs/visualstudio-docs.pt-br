---
title: Identificar e personalizar atalhos de teclado
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Environment.Keyboard
helpviewer_keywords:
- keyboard shortcuts [Visual Studio], customizing
- importing shortcut keys [Visual Studio]
- shortcut key combinations [Visual Studio]
- commands [Visual Studio], shortcut keys
- custom shortcut keys [Visual Studio]
- customizing keyboard shortcuts [Visual Studio]
- exporting shortcut keys [Visual Studio]
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e166e28af02e3e9497b94cdf75a05bd9bf534629
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62428598"
---
# <a name="identify-and-customize-keyboard-shortcuts-in-visual-studio"></a>Identificar e personalizar atalhos de teclado no Visual Studio

Você pode identificar atalhos de teclado para comandos do Visual Studio, personalizar esses atalhos e exportá-los para que outras pessoas os usem. Muitos atalhos sempre invocam os mesmos comandos, mas o comportamento de um atalho pode variar de acordo com as seguintes condições:

- Quais configurações de ambiente padrão você escolheu na primeira vez que executou o Visual Studio (por exemplo, Desenvolvimento Geral ou Visual C#).

- Se você personalizou o comportamento do atalho.

- Em que contexto você está quando escolhe o atalho. Por exemplo, o atalho **F2** invocará o comando `Edit.EditCell` se você estiver usando o **Designer de Configurações** e o comando `File.Rename` se você estiver usando o **Team Explorer**.

Independentemente das configurações, da personalização e do contexto, você sempre pode localizar e alterar um atalho de teclado na caixa de diálogo **Opções**. Também é possível procurar os atalhos de teclado padrão de dezenas de comandos em [Atalhos de teclado padrão para comandos usados com frequência](../ide/default-keyboard-shortcuts-for-frequently-used-commands-in-visual-studio.md) e pode encontrar uma lista completa de todos os atalhos padrão (com base nas **Configurações Gerais de Desenvolvimento**) em [Atalhos de teclado padrão](../ide/default-keyboard-shortcuts-in-visual-studio.md).

Se um atalho for atribuído a um comando no contexto Global e em mais nenhum outro contexto, esse atalho sempre invocará o comando em questão. Porém, um atalho pode ser atribuído a um comando no contexto Global e a um comando diferente em um contexto específico. Se você usar tal atalho quando estiver no contexto específico, o atalho invocará o comando para o contexto específico, e não para o contexto Global.

> [!NOTE]
> Suas configurações e a edição do Visual Studio podem alterar os nomes e os locais dos comandos de menu, bem como as opções que aparecem nas caixas de diálogo. Este tópico se baseia nas **Configurações Gerais de Desenvolvimento**.

## <a name="identify-a-keyboard-shortcut"></a>Identificar um atalho de teclado

1. Na barra de menus, escolha **Ferramentas** > **Opções**.

2. Expanda **Ambiente** e escolha **Teclado**.

   ![Exibir atalhos de teclado na caixa de diálogo Opções](../ide/media/optionskeyboard.png)

3. Na caixa **Mostrar comandos que contenham**, digite todo ou parte do nome do comando sem espaços.

   Por exemplo, você pode localizar os comandos para `solutionexplorer`.

4. Na lista, escolha o comando correto.

    Por exemplo, você pode escolher `View.SolutionExplorer`.

5. Se o comando tiver um atalho de teclado, ele será exibido na lista **Atalho(s) para o comando selecionado**.

   ![Exibir um atalho para um comando especificado](../ide/media/viewshortcut.png)

## <a name="customize-a-keyboard-shortcut"></a>Personalizar um atalho de teclado

1. Na barra de menus, escolha **Ferramentas** > **Opções**.

2. Expanda a pasta **Ambiente** e escolha **Teclado**.

3. Opcional: Filtre a lista de comandos inserindo todo ou parte do nome do comando, sem espaços, na caixa **Mostrar comandos que contêm**.

4. Na lista, escolha o comando ao qual você deseja atribuir um atalho de teclado.

    Na lista **Usar novo atalho em**, escolha a área do recurso em que deseja usar o atalho.

    Por exemplo, você pode escolher **Global** se desejar que o atalho funcione em todos os contextos. É possível usar qualquer atalho que não esteja mapeado (como Global) em outro editor. Caso contrário, o editor substitui o atalho.

    > [!NOTE]
    > Não é possível atribuir as seguintes teclas como parte de um atalho de teclado em **Global**: Print Scrn/Sys Rq, Scroll Lock, Pause/Break, Tab, Caps Lock, Insert, Home, End, Page Up, Page Down, a tecla do logotipo do Windows, a tecla Aplicativo, nenhuma das teclas de Direção ou Enter e, no teclado numérico, Num Lock, Delete ou Clear, nem a combinação Ctrl+Alt+Delete.

6. Na caixa **Pressionar tecla(s) de atalho**, digite o atalho que deseja usar.

    > [!NOTE]
    > Você pode criar um atalho que combine uma letra com a tecla **Alt** e/ou com a tecla **Ctrl**. Você também pode criar um atalho que combine a tecla **Shift** e uma letra com a tecla **Alt** e/ou a tecla **Ctrl**.

     Se um atalho já estiver atribuído a outro comando, ele aparecerá na caixa **Atalho usado atualmente por**. Nesse caso, escolha a tecla **Backspace** para excluir esse atalho antes de tentar outro.

    ![Especificar um atalho diferente para um comando](../ide/media/reassignshortcut.png)

7. Escolha o botão **Atribuir**.

    > [!NOTE]
    > Se você especificar um atalho diferente para um comando, escolha o botão **Atribuir** e, em seguida, **Cancelar**; a caixa de diálogo é fechada, mas a alteração não é revertida.

## <a name="share-custom-keyboard-shortcuts"></a>Compartilhar atalhos de teclado personalizados

Você pode compartilhar os atalhos de teclado personalizados exportando-os para um arquivo e fornecendo o arquivo a outras pessoas para que elas importem os dados.

### <a name="to-export-only-keyboard-shortcuts"></a>Para exportar apenas atalhos de teclado

1. Na barra de menus, escolha **Ferramentas** > **Importar e Exportar Configurações**.

2. Escolha **Exportar configurações de ambiente selecionadas** e escolha o botão **Avançar**.

3. Em **Quais configurações você deseja exportar?**, desmarque a caixa de seleção **Todas as Configurações**, expanda **Opções** e expanda **Ambiente**.

4. Marque a caixa de seleção **Teclado** e escolha o botão **Avançar**.

   ![Exportar apenas atalhos de teclado personalizados](../ide/media/exportshortcuts.png)

5. Nas caixas **Qual nome deseja dar ao arquivo de configurações** e **Armazenar meu arquivo de configurações neste diretório**, mantenha os valores padrão ou especifique outros valores e, em seguida, escolha o botão **Finalizar**.

::: moniker range="vs-2017"

Por padrão, seus atalhos são salvos em um arquivo na pasta *%USERPROFILE%\Documents\Visual Studio 2017\Settings*. O nome do arquivo reflete a data de quando as configurações foram exportadas, e a extensão é *.vssettings*.

::: moniker-end

::: moniker range=">=vs-2019"

Por padrão, os atalhos são salvos em um arquivo na pasta *%USERPROFILE%\Documents\Visual Studio 2019\Settings*. O nome do arquivo reflete a data de quando as configurações foram exportadas, e a extensão é *.vssettings*.

::: moniker-end

### <a name="to-import-only-keyboard-shortcuts"></a>Para importar apenas atalhos de teclado

1. Na barra de menus, escolha **Ferramentas** > **Importar e Exportar Configurações**.

2. Escolha o botão de opção **Importar configurações de ambiente selecionadas** e o botão **Avançar**.

3. Escolha o botão de opção **Não, apenas importe as novas configurações, substituindo minhas configurações atuais** e o botão **Avançar**.

4. Em **Minhas Configurações**, escolha o arquivo que contém os atalhos que deseja importar, ou escolha o botão **Procurar** para localizar o arquivo correto.

5. Escolha o botão **Avançar**.

6. Em **Quais configurações você deseja importar?**, desmarque a caixa de seleção **Todas as Configurações**, expanda **Opções** e expanda **Ambiente**.

7. Marque a caixa de seleção **Teclado** e escolha o botão **Finalizar**.

    ![Importar apenas atalhos de teclado personalizados](../ide/media/importshortcuts.png)

## <a name="see-also"></a>Consulte também

- [Recursos de acessibilidade do Visual Studio](../ide/reference/accessibility-features-of-visual-studio.md)