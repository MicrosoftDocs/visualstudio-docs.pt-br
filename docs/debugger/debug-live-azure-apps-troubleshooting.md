---
title: Solucionando problemas de depuração de instantâneo | Microsoft Docs
ms.custom: seodec18
ms.date: 11/07/2017
ms.technology: vs-ide-debug
ms.topic: troubleshooting
helpviewer_keywords:
- debugger
ms.assetid: 511a0697-c68a-4988-9e29-8d0166ca044a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 82d8a310b86d5dc3c776243293a91f176025f897
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53059821"
---
# <a name="troubleshooting-and-known-issues-for-snapshot-debugging-in-visual-studio"></a>Solução de problemas e problemas conhecidos para instantâneo de depuração no Visual Studio

Se as etapas descritas neste artigo não resolverem seu problema, entre em contato com snaphelp@microsoft.com.

## <a name="issue-snappoint-does-not-turn-on"></a>Problema: Snappoint não ativa

Se você vir um ícone de aviso ![ícone de aviso de Snappoint](../debugger/media/snapshot-troubleshooting-snappoint-warning-icon.png "ícone de aviso de Snappoint") com seu snappoint em vez de no ícone de snappoint regular, em seguida, o snappoint não está ativado.

![Snappoint não ativa](../debugger/media/snapshot-troubleshooting-dont-turn-on.png "Snappoint não ativa")

Siga estas etapas:

1. Verifique se que você tem a mesma versão do código-fonte que foi usado para criar e implantar seu app.isua1. Verifique se que você estiver carregando os símbolos corretos para sua implantação. Para fazer isso, exiba a **módulos** janela durante a depuração de instantâneo e verifique se a coluna do arquivo de símbolo mostra um arquivo. PDB carregado para o módulo que você está depurando. O depurador de instantâneos tentará baixar automaticamente e usar os símbolos para a sua implantação.

## <a name="issue-symbols-do-not-load-when-i-open-a-snapshot"></a>Problema: Símbolos não são carregados quando eu abro um instantâneo

Se você vir a janela a seguir, os símbolos não foram carregado.

![Símbolos não são carregados](../debugger/media/snapshot-troubleshooting-symbols-wont-load.png "símbolos não são carregados.")

Siga estas etapas:

- Clique o **alterar configurações de símbolo...** link nesta página. No **depuração > símbolos** configurações, adicionar um diretório de cache de símbolo. Reinicie a depuração de instantâneo depois que o caminho do símbolo foi definido.

   Os símbolos ou arquivos. PDB, disponíveis em seu projeto devem corresponder à sua implantação do serviço de aplicativo. A maioria das implantações (implantação por meio do Visual Studio, CI/CD com Pipelines do Azure ou o Kudu, etc.) será publicar os arquivos de símbolo ao longo de seu serviço de aplicativo. Definir o diretório de cache de símbolo permite que o Visual Studio para usar esses símbolos.

   ![Configurações de símbolo](../debugger/media/snapshot-troubleshooting-symbol-settings.png "configurações de símbolo")

- Como alternativa, se sua organização usa um servidor de símbolos ou descarta os símbolos em um caminho diferente, use as configurações de símbolo para carregar os símbolos corretos para sua implantação.

## <a name="issue-i-cannot-see-the-attach-snapshot-debugger-option-in-the-cloud-explorer"></a>Problema: Não consigo ver a opção "Anexar depurador de instantâneos" no Gerenciador de nuvem

Siga estas etapas:

- Verifique se que o componente do depurador de instantâneos está instalado. Abra o instalador do Visual Studio e verifique as **depurador de instantâneo** componente na carga de trabalho do Azure.
- Verifique se que seu aplicativo tem suporte. Atualmente, somente o ASP.NET (4.6.1+) e há suporte para aplicativos ASP.NET Core (2.0 +) implantados nos serviços de aplicativo do Azure.

## <a name="issue-i-only-see-throttled-snapshots-in-the-diagnostic-tools"></a>Problema: Vejo apenas limitada instantâneos nas ferramentas de diagnóstico

![Snappoint restrito](../debugger/media/snapshot-troubleshooting-throttled-snapshots.png "limitadas snappoint")

Siga estas etapas:

- Instantâneos ocupam pouca memória, mas têm um encargo de confirmação. Se o depurador de instantâneo detecta que o servidor está sob carga pesada de memória, ele não será tirar instantâneos. Você pode excluir instantâneos já capturados por interromper a sessão do depurador de instantâneo e tentar novamente.

## <a name="known-issues"></a>Problemas Conhecidos

- Atualmente, não há suporte para a depuração de instantâneo com vários clientes do Visual Studio no mesmo serviço de aplicativo.
- Otimizações de Roslyn IL não têm suporte total em projetos ASP.NET Core. Para alguns projetos ASP.NET Core, você pode não ser capaz de ver algumas variáveis ou usar algumas variáveis em instruções condicionais. 
- Variáveis especiais, como *$FUNCTION* ou *$CALLER*, não pode ser avaliada em instruções condicionais ou logpoints para projetos do ASP.NET Core.
- Depuração de instantâneo não funciona nos serviços de aplicativos que têm [Cache Local](/azure/app-service/app-service-local-cache) ativado.
- Atualmente não há suporte para aplicativos de API de depuração de instantâneo.

## <a name="site-extension-upgrade"></a>Atualização de extensão de site

Depuração de instantâneo e o Application Insights dependem de um ICorProfiler, que carrega no processo do site e faz com que os problemas de bloqueio de arquivo durante a atualização. É recomendável que esse processo para garantir que não há nenhum tempo de inatividade para seu site de produção.

- Criar uma [Slot de implantação](/azure/app-service/web-sites-staged-publishing) dentro de seu serviço de aplicativo e implantar seu site no slot.
- Troque o Slot de produção do Cloud Explorer no Visual Studio ou do portal do Azure.
- Pare o site do Slot. Isso levará alguns segundos para eliminar o processo de w3wp.exe do site de todas as instâncias.
- Atualizar a extensão de site do Slot do site do Kudu ou o portal do Azure (*folha de serviço de aplicativo > Ferramentas de desenvolvimento > extensões > atualização*).
- Inicie o site do Slot. Recomendamos que você visitar o site para aquecê-lo novamente.
- Troque o Slot de produção.

## <a name="see-also"></a>Consulte também

[Depurando no Visual Studio](../debugger/index.md)  
[Depurar aplicativos ASP.NET dinâmicos usando o depurador de instantâneo](../debugger/debug-live-azure-applications.md)  
[Perguntas frequentes sobre depuração de instantâneos](../debugger/debug-live-azure-apps-faq.md)  
