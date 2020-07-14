---
title: Sincronizar as configurações
ms.date: 06/18/2020
ms.topic: conceptual
ms.assetid: a3d2ea29-be5d-4012-9820-44b06adbb7dd
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3129543656c0defe09543b8531d8a10998791083
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285199"
---
# <a name="synchronize-visual-studio-settings-across-multiple-computers"></a>Sincronizar as configurações do Visual Studio em vários computadores

Quando você entra no Visual Studio em vários computadores usando a mesma conta de personalização, as configurações podem ser sincronizadas nos computadores.

## <a name="synchronized-settings"></a>Configurações sincronizadas

Por padrão, as seguintes configurações são sincronizadas:

- Configurações de desenvolvimento. Você seleciona uma coleção de configurações na primeira vez que abrir o Visual Studio, mas pode alterar a seleção a qualquer momento. Para obter mais informações, confira [Configurações do ambiente](../ide/environment-settings.md).

- Alias de comando definidos pelo usuário. Para saber mais sobre como definir aliases de comando, veja [Aliases de comando do Visual Studio](../ide/reference/visual-studio-command-aliases.md).

- Layouts de janela definidos pelo usuário **Window**na  >  página**gerenciar layouts de janela** do Windows.

- As opções a seguir nas **Tools**  >  páginas**Opções** de ferramentas:

  - Configurações de caixas de tema e barra de **Environment**menus na  >  página opções**gerais** do ambiente.

  - Todas as configurações na **Environment**  >  página opções de**fontes e cores** do ambiente.

  - Todos os atalhos de teclado **Environment**na  >  página opções de**teclado** do ambiente.

  - Todas as configurações nas **Environment**  >  **guias ambiente e** na página Opções do Windows.

  - Todas as configurações na **Environment**  >  página opções de**inicialização** do ambiente.

  - Todas as configurações nas páginas de opção do **Editor de Texto**, por exemplo, [preferências de estilo de código](code-styles-and-code-cleanup.md).

  - Todas as configurações das páginas de opções **Designer XAML**.

## <a name="turn-off-synchronized-settings-on-a-particular-computer"></a>Desligar configurações sincronizadas em um computador específico

As configurações sincronizadas para o Visual Studio são ativadas por padrão. Você pode desativar as configurações sincronizadas em um computador acessando a página **ferramentas**  >  **Opções**do  >  **ambiente**  >  **contas** e desmarcando **sincronizar configurações entre dispositivos quando estiver conectado ao Visual Studio**.

Por exemplo, se você decidir não sincronizar as configurações no Visual Studio no computador "A", as alterações de configuração feitas no computador "A" não aparecerão no computador "B" ou no computador "C". Os computadores "B" e "C" continuarão sendo sincronizados um com o outro, mas não com o computador "A".

> [!NOTE]
> Se você optar por não sincronizar as configurações desmarcando a opção na página contas do ambiente de opções de **ferramentas**  >  **Options**  >  **Environment**  >  **Accounts** , outras versões ou edições do Visual Studio que você tem no mesmo computador não serão afetadas. Essas instalações lado a lado do Visual Studio continuarão sincronizando as configurações (a menos que você desmarque a opção nelas também).

## <a name="synchronize-settings-across-visual-studio-ide-products-and-editions"></a>Sincronizar configurações em produtos e edições do IDE do Visual Studio

As configurações são sincronizadas em todas as versões e edições do Visual Studio instaladas *lado a lado*. As configurações também são sincronizadas entre os produtos IDE do Visual Studio, incluindo Blend para Visual Studio. No entanto, um produto IDE individual do Visual Studio pode ter suas próprias configurações que não são compartilhadas com o Visual Studio. Por exemplo, as configurações específicas do Blend para Visual Studio no computador "A" não são compartilhadas com o Visual Studio nos computadores "A" ou "B".

## <a name="side-by-side-synchronized-settings"></a>Configurações sincronizadas lado a lado

::: moniker range="vs-2017"

Algumas configurações, como o layout da janela de ferramentas, não são compartilhadas entre diferentes instalações lado a lado do Visual Studio. O arquivo *CurrentSettings.vssettings* em *%userprofile%\Documents\Visual Studio 2017\Settings* é uma pasta específica à instalação semelhante a *%localappdata%\Microsoft\VisualStudio\15.0_xxxxxxxx\Settings*.

> [!NOTE]
> Para usar as novas configurações específicas à instalação, faça uma nova instalação. Quando você atualiza uma instalação existente do Visual Studio, ela usa a localização compartilhada existente.

Se você tiver instalações lado a lado do Visual Studio e desejar usar a localização de arquivo das novas configurações específicas da instalação, siga estas etapas:

1. Atualizar para o Visual Studio 2017 versão 15.3 ou posterior.

2. Use o **Assistente para Importar e Exportar Configurações** para exportar todas as configurações existentes para uma localização fora da pasta *%localappdata%\Microsoft\VisualStudio\15.0_xxxxxxxx*.

3. Abra o **Prompt de Comando do Desenvolvedor para VS 2017** e execute `devenv /resetuserdata`.

1. Abra o Visual Studio e importe as configurações salvas do arquivo de configurações exportado.

::: moniker-end

::: moniker range=">=vs-2019"

Algumas configurações, como o layout da janela de ferramentas, não são compartilhadas entre diferentes instalações lado a lado do Visual Studio. O arquivo *CurrentSettings.vssettings* em *%userprofile%\Documents\Visual Studio 2019\Settings* é uma pasta específica da instalação semelhante a *%localappdata%\Microsoft\VisualStudio\16.0_xxxxxxxx\Settings*.

::: moniker-end

## <a name="reset-synchronized-settings"></a>Restaurar as configurações sincronizadas

Para redefinir todas as configurações para seus padrões, entre no Visual Studio e, em seguida, selecione **ferramentas**  >  **importar e exportar configurações** para abrir o **Assistente de importação e exportação de configurações**. Selecione **Restaurar todas as configurações** e siga as etapas restantes do assistente.

## <a name="see-also"></a>Veja também

- [Personalizar o IDE](../ide/personalizing-the-visual-studio-ide.md)
- [Configurações do ambiente](../ide/environment-settings.md)
- [Caixa de diálogo Ambiente > Opções de Contas](reference/accounts-environment-options-dialog-box.md)
- [Instalar versões do Visual Studio lado a lado](../install/install-visual-studio-versions-side-by-side.md)
