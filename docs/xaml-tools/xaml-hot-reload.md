---
title: Gravar e depurar XAML usando o Hot recarregamento de XAML
description: O Hot recarregamento de XAML ou editar e continuar XAML permite que você faça alterações no código XAML durante a execução de aplicativos
ms.date: 08/05/2019
ms.topic: conceptual
helpviewer_keywords:
- xaml edit and continue
- xaml hot reload
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 875608fbaa2e5c7532371fd95858fe87cdc81ca1
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815884"
---
# <a name="write-and-debug-running-xaml-code-with-xaml-hot-reload-in-visual-studio"></a>Escrever e depurar o código XAML em execução com o Hot recarregamento de XAML no Visual Studio

O Hot recarregamento de XAML ajuda você a criar sua interface do usuário do aplicativo do WPF ou UWP, permitindo que você faça alterações no código XAML enquanto seu aplicativo está em execução. A recarga ativa está disponível no Visual Studio e no Blend para Visual Studio. Esse recurso permite criar e testar incrementalmente o código XAML com o benefício do contexto de dados do aplicativo em execução, o estado de autenticação e outras complexidades do mundo real que são difíceis de simular durante o tempo de design. Se você precisar de ajuda para solucionar problemas de recarregamento dinâmico de XAML, consulte [Solucionando problemas de recarga em XAML](xaml-hot-reload-troubleshooting.md) .

> [!NOTE]
> Se você estiver usando o Xamarin. Forms, consulte [a Hot recarga XAML para Xamarin. Forms](/xamarin/xamarin-forms/xaml/hot-reload).

O Hot recarregamento de XAML é especialmente útil nesses cenários:

* Correção de problemas de interface do usuário encontrados no código XAML depois que o aplicativo foi iniciado no modo de depuração.

* Criar um novo componente de interface do usuário para um aplicativo que está em desenvolvimento, aproveitando, ao mesmo tempo, o contexto do tempo de execução do aplicativo.

|Tipos de aplicativos com suporte|Sistema operacional e ferramentas|
|-|-|-|
|Windows Presentation Foundation (WPF) |.NET Framework 4.6 + e .NET Core</br>Windows 7 e posterior |
|Aplicativos universais do Windows (UWP)|Windows 10 e posterior, com o [SDK do Windows 10](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 14393 + |

A ilustração a seguir mostra o uso da árvore visual ao vivo para abrir o código-fonte e, em seguida, o recarregamento de XAML para alterar o texto do botão e a cor do botão.

![Recarga Dinâmica de XAML](../debugger/media/xaml-hot-reload-using.gif)

> [!NOTE]
> Atualmente, há suporte para o Hot recarregamento XAML do Visual Studio apenas ao executar seu aplicativo no Visual Studio ou Blend para Visual Studio com o depurador anexado (**F5** ou **iniciar a depuração**). Não é possível habilitar essa experiência usando [anexar ao processo](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md) , a menos que você [defina manualmente uma variável de ambiente](xaml-hot-reload-troubleshooting.md#verify-that-you-use-start-debugging-rather-than-attach-to-process).

## <a name="known-limitations"></a>Limitações conhecidas

Veja a seguir as limitações conhecidas do Hot recarregamento XAML. Para solucionar qualquer limitação que você encontrar, basta parar o depurador e concluir a operação.

|Limitações|WPF|UWP|Observações|
|-|-|-|-|
|Eventos de fiação para controles enquanto o aplicativo está em execução|Sem suporte|Sem suporte|Consulte erro: *falha no evento de garantia*. Observe que no WPF você pode fazer referência a um manipulador de eventos existente. Em aplicativos UWP, não há suporte para a referência a um manipulador de eventos existente.|
|Criando objetos de recurso em um dicionário de recursos, como aqueles na página/janela do seu aplicativo ou *app. XAML*|Com suporte a partir do Visual Studio 2019 atualização 2|Com suporte|Exemplo: adicionando um a `SolidColorBrush` um dicionário de recursos para uso como um `StaticResource` .</br>Observação: recursos estáticos, conversores de estilo e outros elementos gravados em um dicionário de recursos podem ser aplicados/usados ao usar o Hot recarregamento de XAML. Somente a criação do recurso não tem suporte.</br> Alterando a propriedade do dicionário de recursos `Source` .|
|Adicionar novos controles, classes, janelas ou outros arquivos ao seu projeto enquanto o aplicativo está em execução|Sem suporte|Sem suporte|Nenhum|
|Gerenciando pacotes NuGet (adicionando/removendo/atualizando pacotes)|Sem suporte|Sem suporte|Nenhum|
|Alterando a associação de dados que usa a extensão de marcação {x:Bind}|N/D|Com suporte a partir do Visual Studio 2019|Isso requer o Windows 10 versão 1809 (Build 10.0.17763). Sem suporte no Visual Studio 2017 ou em versões anteriores.|
|Não há suporte para a alteração de diretivas x:Uid|N/D|Sem suporte|Nenhum|
|Vários processos | Sem suporte | Sem suporte | A recarga a quente só pode ser usada em um processo de cada vez. |

## <a name="error-messages"></a>Mensagens de erro

Você pode se deparar com os seguintes erros ao usar o Hot recarregamento de XAML.

|Mensagem de erro|Description|
|-|-|
|Verifique se o evento falhou|Erro indica que você está tentando vincular um evento a um de seus controles, o que não tem suporte enquanto o aplicativo está em execução.|
|Essa alteração não é suportada pelo Hot recarregamento XAML e não será aplicada durante a sessão de depuração.|Erro indica que a alteração que você está tentando executar não é suportada pelo Hot recarregamento XAML. Pare a sessão de depuração, faça a alteração e reinicie a sessão de depuração. Se você encontrar um cenário sem suporte que gostaria de ver com suporte, use nossa nova opção "sugerir um recurso" na [comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/spaces/8/index.html). |

## <a name="see-also"></a>Veja também

* [Solução de problemas de Recarga Dinâmica de XAML](xaml-hot-reload-troubleshooting.md)
* [Recarga Dinâmica de XAML para Xamarin.Forms](/xamarin/xamarin-forms/xaml/hot-reload)
* [Editar e continuar (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
