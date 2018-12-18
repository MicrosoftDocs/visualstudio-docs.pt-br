---
title: Realizar pré-busca de conteúdo para aplicativos da Windows Store | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: b4481fef-3ebf-4f7d-9748-d43821a0ebac
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7ad7c09e163833c295be45a7ee81e2e0587fa6b2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51797397"
---
# <a name="prefetch-content-for-windows-store-apps"></a>Executar pré-busca de conteúdo para aplicativos da Windows Store
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows apenas] (... /Image/windows_only_content.png "windows_only_content")  
  
 Para tornar seu aplicativo da Windows Store mais responsivo, você pode solicitar o Windows para pré-carregar algum conteúdo da web, como imagens, ou páginas da web para o aplicativo [WinINet](http://msdn.microsoft.com/en-us/0a06f2af-957a-4dff-a8cc-187370181b5c)[WinINet](http://msdn.microsoft.com/library/aa383630.aspx)cache. Essa funcionalidade chama-se pré-busca. É especialmente eficiente para o conteúdo que é usado na inicialização, mas você também pode executar a pré-busca de outro conteúdo usado frequentemente. Os métodos do [Windows.Networking.BackgroundTransfer.ContentPrefetcher](http://msdn.microsoft.com/library/windows/apps/windows.networking.backgroundtransfer.contentprefetcher.aspx) classe permitem que você especifique os URIs do conteúdo que você deseja pré-carregar. Consulte o SDK do Windows [amostra de pré-busca de conteúdo](http://code.msdn.microsoft.com/windowsapps/ContentPrefetcher-Sample-432c8309) para obter exemplos de como adicionar a funcionalidade ContentPrefetcher ao seu aplicativo.  
  
 O Windows usa heurística para determinar quando e se a pré-busca deve ocorrer e quais recursos serão baixados. A heurística leva em conta condições de energia e rede do sistema da conta, o histórico de uso do aplicativo do usuário e os resultados das tentativas anteriores de pré-busca. No Visual Studio, você pode usar o **acionar Windows Store App pré-busca** comando para forçar o Windows para ignorar a heurística ContentPrefetcher e pré-carregar todo o conteúdo da web especificado. Isso pode ser útil se você quiser testar o comportamento ou desempenho do aplicativo com o conteúdo para pré-buscar em um estado conhecido (carregado ou não carregado).  
  
## <a name="to-force-preloading-of-contentprefetcher-specified-resources"></a>Para forçar o pré-carregamento dos recursos especificados do ContentPrefetcher  
 Este procedimento presume que você já definiu a funcionalidade ContentPrefetcher e especificou os URIs de conteúdo para pré-carregar em seu projeto de aplicativo. Para forçar o pré-carregamento de conteúdo quando os recursos especificados são novos ou modificados, você precisará iniciar e parar o aplicativo antes de escolher o **acionar Windows Store App pré-busca** comando. Você executa o aplicativo primeiro para registrar os URIs. **Acionar pré-busca do Windows Store App** comando força o ContentPrefetcher a baixar o conteúdo e adicioná-lo ao cache. Nas execuções subsequentes do aplicativo, você pode presumir que o conteúdo esteja pré-carregado.  
  
1. Inicie o aplicativo para registrar os URIs de conteúdo para pré-busca com o aplicativo. Sobre o **Debug** menu, escolha **iniciar depuração** (atalho de teclado: F5).  
  
2. Sobre o **Debug** menu, escolha **parar depuração** (atalho de teclado: Shift + F5).  
  
3. Sobre o **depurar** menu, escolha **outros destinos de depuração** e, em seguida, escolha **acionar Windows Store App pré-busca**.  
  
   Agora você pode depurar, testar ou analisar seu aplicativo com os recursos Web pré-buscados.  
  
> [!NOTE]
>  Repita estas etapas sempre que adicionarem ou modificar o conteúdo da Web especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Postagem de blog: acionar a pré-busca para aplicativos Windows da Store no Visual Studio 2013 atualização 2](http://blogs.msdn.com/b/visualstudioalm/archive/2014/02/06/triggering-prefetch-for-windows-store-apps-in-visual-studio-2013-update-2.aspx)



