---
title: VSPerf | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b5854e62-279e-4850-bfeb-0c6ef82f4805
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 051c983920ddc80909d721e569c5efb5ecd33a7c
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779929"
---
# <a name="vsperf"></a>VSPerf
Use a ferramenta de linha de comando **VsPerf** para:

1. Crie perfil de aplicativos UWP na linha de comando quando o Visual Studio não estiver instalado no dispositivo.

2. Crie perfil de aplicativos de área de trabalho do Windows 8 e aplicativos do Windows Server 2012 usando o método de criação de perfil de amostragem.

   Para obter mais informações sobre opções de criação de perfil, consulte [Ferramentas de desempenho em aplicativos do Windows 8 e Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

## <a name="uwp-apps-only"></a>Apenas os aplicativos UWP
 Essas opções se aplicam somente aos aplicativos UWP.

|||
|-|-|
|**/app:{AppName}**|Inicia o criador de perfil e aguarda o lançamento do aplicativo especificado no menu Iniciar.<br /><br /> Execute `vsperf /listapps` para exibir o nome do aplicativo e o PackageFullName de aplicativos instalados.|
|**/package:{PackageFullName}**|Inicia o criador de perfil e aguarda o lançamento do aplicativo especificado no menu Iniciar.<br /><br /> Execute `vsperf /listapps` para exibir o nome do aplicativo e o PackageFullName de aplicativos instalados.|
|**/js**|Necessário para aplicativos JavaScript de criação de perfil.<br /><br /> Colete dados de desempenho de aplicativos JavaScript.<br /><br /> Use somente com /package ou /attach.|
|**/noclr**|Opcional. Não colete dados CLR.<br /><br /> Use somente com /package ou /attach.<br /><br /> Otimização, nenhum símbolo gerenciado será resolvido.|
|**/listapps**|Lista nomes de aplicativos instalados e PackageFullNames.|

## <a name="windows-8-desktop-applications-and-windows-server-2012-applications-only"></a>Somente aplicativos da área de trabalho do Windows 8 e do Windows Server 2012
 Essas opções não funcionam em aplicativos UWP.

|||
|-|-|
|**/launch:{Executable}**|Inicia e começa a criação de perfil do arquivo executável especificado.|
|**/args:{ExecutableArguments}**|Especifica os argumentos de linha de comando que passarão o destino **/launch**.|
|**/console**|Executa o destino **/launch** em uma nova janela de comando.|

## <a name="all-applications"></a>Todos os aplicativos
 Essas opções aplicam-se a qualquer aplicativo Windows 8 ou o Windows Server 2012.

|||
|-|-|
|**/attach:{PID&#124;ProcessName}[,PID&#124;ProcessName]...**|Coleta dados dos processos especificados.<br /><br /> Use o Gerenciador de Tarefas para exibir a PID (ID do Processo) e processar os nomes dos aplicativos em execução.|
|**/file:{ReportName}**|Opcional. Especifica o arquivo de saída (substitui o arquivo existente).<br /><br /> Use somente com /package ou /attach.|
|**/pause**|Pause a coleta de dados.|
|**/resume**|Retome a coleta de dados.|
|**/stop**|Pare a coleta de dados e encerre os processos de destino.|
|**/detach**|Pare a coleta de dados, mas permita que os processos de destino continuem a executar.|
|**/status**|Mostre status do criador de perfil.|

## <a name="see-also"></a>Consulte também
- [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)
- [Criar perfil da linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)
