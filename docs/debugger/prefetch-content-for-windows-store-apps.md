---
title: Depurar usando conteúdo de pré-busca em aplicativos UWP | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 65b889452a23bb970cbee4c65455679a3473abab
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348061"
---
# <a name="debug-uwp-apps-using-prefetched-content-in-visual-studio"></a>Depurar aplicativos UWP usando conteúdo de pré-busca no Visual Studio

 Para tornar seu aplicativo UWP mais responsivo, você pode solicitar que o Windows faça o pré-carregamento de algum conteúdo da Web, como páginas da Web ou imagens, no cache do [WinInet](/windows/desktop/WinInet/about-wininet) do aplicativo. Essa funcionalidade chama-se pré-busca. É especialmente eficiente para o conteúdo usado na inicialização, mas você também pode executar a pré-busca de outro conteúdo usado frequentemente. Os métodos da classe [Windows.Networking.BackgroundTransfer.ContentPrefetcher](/uwp/api/Windows.Networking.BackgroundTransfer.ContentPrefetcher) permitem especificar os URIs do conteúdo que você deseja pré-carregar. Confira a [Amostra de pré-busca de conteúdo](https://code.msdn.microsoft.com/windowsapps/ContentPrefetcher-Sample-432c8309) do SDK do Windows para obter exemplos de como adicionar a funcionalidade ContentPrefetcher ao seu aplicativo.

 O Windows usa heurística para determinar quando e se a pré-busca deve ocorrer e quais recursos serão baixados. A heurística leva em conta condições de energia e rede do sistema da conta, o histórico de uso do aplicativo do usuário e os resultados das tentativas anteriores de pré-busca. No Visual Studio, você pode usar o comando **Disparar Pré-busca de Aplicativo da Windows Store** para forçar o Windows a ignorar a heurística ContentPrefetcher e pré-carregar todo o conteúdo da Web especificado. Isso pode ser útil se você quiser testar o comportamento ou desempenho do aplicativo com o conteúdo para pré-buscar em um estado conhecido (carregado ou não carregado).

## <a name="to-force-preloading-of-contentprefetcher-specified-resources"></a>Para forçar o pré-carregamento dos recursos especificados do ContentPrefetcher
 Este procedimento presume que você já definiu a funcionalidade ContentPrefetcher e especificou os URIs de conteúdo para pré-carregar em seu projeto de aplicativo. Para forçar o pré-carregamento de conteúdo quando os recursos especificados são novos ou modificados, você tem de iniciar e parar o aplicativo antes de escolher o comando **Disparar Pré-busca de Aplicativo da Windows Store**. Você executa o aplicativo primeiro para registrar os URIs. O comando **Disparar Pré-busca de Aplicativo da Windows Store** força o ContentPrefetcher a baixar o conteúdo e adicioná-lo ao cache. Nas execuções subsequentes do aplicativo, você pode presumir que o conteúdo esteja pré-carregado.

1. Inicie o aplicativo para registrar os URIs de conteúdo para pré-busca com o aplicativo. No menu **Depurar**, escolha **Iniciar Depuração** (atalho do teclado: F5).

2. **No menu Depurar**, escolha **Parar Depuração** (atalho do teclado: Shift+F5).

3. No menu **Depurar**, escolha **Outros Destinos de Depuração** e escolha **Disparar Pré-busca de Aplicativo da Windows Store**.

   Agora você pode depurar, testar ou analisar seu aplicativo com os recursos Web pré-buscados.

> [!NOTE]
> Repita estas etapas sempre que adicionarem ou modificar o conteúdo da Web especificado.

## <a name="see-also"></a>Veja também
- [Postagem no blog: disparando a pré-busca para aplicativos da Windows Store no Visual Studio 2013 atualização 2](https://devblogs.microsoft.com/devops/triggering-prefetch-for-windows-store-apps-in-visual-studio-2013-update-2/)