---
title: Solução de problemas de Recarga Dinâmica de XAML
description: Corrija os problemas que você pode encontrar com o Hot recarregamento de XAML.
ms.date: 09/04/2019
ms.topic: troubleshooting
helpviewer_keywords:
- xaml edit and continue, troubleshooting
- xaml hot reload, troubleshooting
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 447725fd27ab81b85890d37a8f0df8a35ad5fbee
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328473"
---
# <a name="troubleshooting-xaml-hot-reload"></a>Solução de problemas de Recarga Dinâmica de XAML

Este guia de solução de problemas inclui instruções detalhadas que devem resolver a maioria dos problemas que impedem que o Hot Load de XAML funcione corretamente.

O Hot recarregamento de XAML tem suporte para aplicativos do WPF e UWP. Para obter detalhes sobre os requisitos de sistema operacional e de ferramentas, consulte [gravar e depurar o código XAML em execução com o Hot recarregamento de XAML](xaml-hot-reload.md).

## <a name="hot-reload-is-not-available"></a>O Hot recarregamento não está disponível

Se você vir a mensagem "a recarga automática não está disponível" na barra de ferramentas no aplicativo durante a depuração do aplicativo, siga as instruções descritas neste artigo para resolver o problema.

## <a name="verify-that-xaml-hot-reload-is-enabled"></a>Verificar se o Hot recarregamento XAML está habilitado

O recurso é habilitado por padrão. Quando você começar a depurar seu aplicativo, verifique se você vê a barra de ferramentas no aplicativo, que confirma que o Hot recarregamento XAML está disponível:

![Hot recarregamento de XAML disponível](../debugger/media/xaml-hot-reload-available.png)

Se você não vir a barra de ferramentas no aplicativo, abra **Debug**  >  **as opções**de depuração  >  **geral**. Verifique se as duas opções, **habilitar ferramentas de depuração da interface do usuário para XAML** e **habilitar o Hot recarregamento de XAML** estão selecionadas.

![Habilitar o Hot recarregamento de XAML](../debugger/media/xaml-hot-reload-enable.png)

Se essas opções forem selecionadas, vá para árvore visual dinâmica (**depurar**  >  **Windows**  >  **árvore visual**do Windows Live) e certifique-se de que **Mostrar ferramentas de tempo de execução no** botão da barra de ferramentas do aplicativo (na extrema esquerda) esteja selecionado.

![Habilitar o Hot recarregamento de XAML](../debugger/media/xaml-hot-reload-show-runtime-tools.png)

## <a name="verify-that-you-use-start-debugging-rather-than-attach-to-process"></a>Verifique se você usa iniciar depuração em vez de anexar ao processo

O Hot recarregamento de XAML requer que a variável de ambiente `ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO` seja definida como 1 no momento em que o aplicativo é iniciado. O Visual Studio define isso automaticamente como parte do comando **depurar**  >  **Iniciar Depuração** (ou **F5**). Se você quiser usar o Hot recarregamento de XAML com o comando **debug**  >  **Attach to Process** , em vez disso, defina a variável de ambiente por conta própria.

> [!NOTE]
> Para definir uma variável de ambiente, use o botão Iniciar para procurar "variável de ambiente" e escolha **Editar as variáveis de ambiente do sistema**. Na caixa de diálogo que é aberta, escolha **variáveis de ambiente**, em seguida, adicione-a como uma variável de usuário e defina o valor como `1` . Para limpar, remova a variável quando terminar a depuração.

## <a name="verify-that-your-msbuild-properties-are-correct"></a>Verifique se as propriedades do MSBuild estão corretas

Por padrão, as informações de origem são incluídas em uma configuração de depuração. Ele é controlado pelas propriedades do MSBuild em seus arquivos de projeto (como *. csproj). Para o WPF, a propriedade é `XamlDebuggingInformation` , que deve ser definida como `True` . Para UWP, a propriedade é `DisableXbfLineInfo` , que deve ser definida como `False` . Por exemplo:

WPF:

`<XamlDebuggingInformation>True</XamlDebuggingInformation>`

UWP

`<DisableXbfLineInfo>False</DisableXbfLineInfo>`

## <a name="verify-that-you-are-using-the-correct-build-configuration-name"></a>Verifique se você está usando o nome de configuração de compilação correto

Você deve definir manualmente a propriedade correta do MSBuild para dar suporte ao Hot recarregamento de XAML (consulte a seção anterior) ou deve usar o nome de configuração de compilação padrão (depuração). Se você não definir a Propriedade MSBuild corretamente, um nome de configuração de compilação personalizado não funcionará, nem será criado um Build de versão.

## <a name="verify-that-your-xaml-file-has-no-errors"></a>Verifique se o arquivo XAML não tem erros

Se o arquivo XAML mostrar erros no **lista de erros**, o Hot recarregamento XAML pode não funcionar.

## <a name="see-also"></a>Veja também

[Gravar e depurar o código XAML em execução com o Hot recarregamento de XAML](xaml-hot-reload.md)
