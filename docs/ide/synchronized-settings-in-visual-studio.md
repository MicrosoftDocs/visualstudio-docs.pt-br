---
title: Sincronizar as configurações
ms.date: 11/21/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Environment.RoamingSettings
ms.assetid: a3d2ea29-be5d-4012-9820-44b06adbb7dd
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ecac148e745eff956151af71a37b23f67a816f56
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388485"
---
# <a name="synchronize-visual-studio-settings-across-multiple-computers"></a>Sincronizar as configurações do Visual Studio em vários computadores

Quando você entra no Visual Studio em vários computadores usando a mesma conta de personalização, as configurações podem ser sincronizadas nos computadores.

## <a name="synchronized-settings"></a>Configurações sincronizadas

Por padrão, as seguintes configurações são sincronizadas:

- Configurações de desenvolvimento. Você seleciona uma coleção de configurações na primeira vez que abrir o Visual Studio, mas pode alterar a seleção a qualquer momento. Para obter mais informações, confira [Configurações do ambiente](../ide/environment-settings.md).

- Alias de comando definidos pelo usuário. Para saber mais sobre como definir aliases de comando, veja [Aliases de comando do Visual Studio](../ide/reference/visual-studio-command-aliases.md).

- Layouts de janela definidos pelo usuário na página **Janela** > **Gerenciar Layouts de Janela**.

- As seguintes opções nas páginas **Ferramentas** > **Opções**:

   - Configurações de tema e de uso de maiúsculas na barra de menus, na página de opções **Ambiente** > **Geral**.

   - Todas as configurações da página de opções **Ambiente** > **Fontes e Cores**.

   - Todos os atalhos de teclado da página de opções **Ambiente** > **Teclado**.

   - Todas as configurações da página de opções **Ambiente** > **Guias e Janelas**.

   - Todas as configurações da página de opções **Ambiente** > **Inicialização**.

   - Todas as configurações das páginas de opções **Editor de Texto**.

   - Todas as configurações das páginas de opções **Designer XAML**.

## <a name="turn-off-synchronized-settings-on-a-particular-computer"></a>Desligar configurações sincronizadas em um computador específico

As configurações sincronizadas para o Visual Studio são ativadas por padrão. Desligue as configurações sincronizadas em um computador acessando a página **Ferramentas** > **Opções** > **Ambiente** > **Contas** e desmarcando a opção **Sincronizar as configurações em dispositivos quando estiver conectado ao Visual Studio**. Por exemplo, se você optar por não sincronizar as configurações do Visual Studio no computador "A", as alterações de configuração feitas no computador "A" não serão exibidas nos computadores "B" ou "C". Os computadores "B" e "C" continuarão sendo sincronizados um com o outro, mas não com o computador "A".

## <a name="synchronize-settings-across-visual-studio-family-products-and-editions"></a>Sincronizar configurações em edições e produtos da família Visual Studio

As configurações podem ser sincronizadas em qualquer edição do Visual Studio, incluindo Community Edition. As configurações também são sincronizadas em todos os produtos da família Visual Studio. No entanto, cada um desses produtos da família pode ter suas próprias configurações que não são compartilhadas com o Visual Studio. Por exemplo, as configurações específicas a um produto no computador "A" são compartilhadas com outro produto no computador "B", mas não com o Visual Studio nos computadores "A" ou "B".

## <a name="side-by-side-synchronized-settings"></a>Configurações sincronizadas lado a lado

No Visual Studio 2017 versão 15.3 e posterior, algumas configurações como o layout da janela de ferramentas não são compartilhadas entre as diferentes instalações lado a lado do Visual Studio 2017. O arquivo *CurrentSettings.vssettings* em *%userprofile%\Documents\Visual Studio 2017\Settings* é uma pasta específica à instalação semelhante a *%localappdata%\Microsoft\VisualStudio\15.0_xxxxxxxx\Settings*.

> [!NOTE]
> Para usar as novas configurações específicas à instalação, faça uma nova instalação. Quando você atualiza uma instalação existente do Visual Studio 2017 para a versão mais atual, ela usa o local compartilhado existente.

Se, no momento, você tem instalações lado a lado do Visual Studio 2017 e deseja usar o local de arquivo das novas configurações específicas à instalação, siga estas etapas:

1. Atualizar para o Visual Studio 2017 versão 15.3 ou posterior.

1. Use o assistente de **configurações de Importação\Exportação** para exportar todas as configurações existentes para um local fora da pasta *%localappdata%\Microsoft\VisualStudio\15.0_xxxxxxxx*.

1. Abra o **Prompt de Comando do Desenvolvedor para VS 2017** da instalação atualizada do Visual Studio e execute `devenv /resetuserdata`.

1. Inicie o Visual Studio e importe as configurações salvas do arquivo de configurações exportado.

## <a name="see-also"></a>Consulte também

- [Personalizar o IDE](../ide/personalizing-the-visual-studio-ide.md)
- [Configurações do ambiente](../ide/environment-settings.md)
- [Caixa de diálogo Ambiente > Opções de Contas](reference/synchronized-settings-environment-options-dialog-box.md)
