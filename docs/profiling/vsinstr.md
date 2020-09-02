---
title: VSInstr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- performance tools, instrumentation
- instrumentation, VSInstr tool
- profiling tools,VSInstr
- command-line tools, instrumentation
- command line, tools
- VSInstr
- VSInstr tool
- performance tools, VSInstr tool
ms.assetid: 7b1334f7-f9b0-4a82-a145-d0607bfa8467
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: fc68ad7da06a1710e3c34ddb601155fc3d0b1182
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "85330503"
---
# <a name="vsinstr"></a>VSInstr
A ferramenta VSInstr é usada para instrumentar binários. Ela é chamada usando a seguinte sintaxe:

```cmd
VSInstr [/U] filename [/options]
```

 A tabela a seguir descreve as opções da ferramenta VSInstr:

|Opções|Descrição|
|-------------|-----------------|
|**Ajuda** ou **?**|Exibe a ajuda.|
|**U**|Grava a saída redirecionada do console como Unicode. Deve ser a primeira opção especificada.|
|`@filename`|Especifica o nome de um arquivo de resposta que contém uma opção de comando por linha.  Não use aspas.|
|**OutputPath** `:path`|Especifica um diretório de destino para a imagem instrumentada. Se um caminho de saída não for especificado, o binário original será renomeado acrescentando "Orig" ao nome do arquivo no mesmo diretório e uma cópia do binário será instrumentada.|
|**Excluir:**`funcspec`|Determina uma especificação de função a ser excluída da instrumentação por testes. É útil quando a entrada de teste de criação de perfil em uma função causa resultados imprevisíveis ou indesejados.<br /><br /> Não use as opções **Exclude** e **Include** que se referem a funções no mesmo binário.<br /><br /> Você pode determinar várias especificações de função com opções **Exclude** separadas.<br /><br /> `funcspec` é definida como:<br /><br /> [namespace \<separator1> ] [classe \<separator2> ] funcionamento<br /><br /> \<separator1> é `::` para código nativo e `.` para código gerenciado.<br /><br /> \<separator2> é sempre `::`<br /><br /> **Exclude** tem suporte com a cobertura de código.<br /><br /> Há suporte para o caractere curinga \*. Por exemplo, para excluir todas as funções em um namespace, use:<br /><br /> MyNamespace::\*<br /><br /> Você pode usar **VSInstr /DumpFuncs** para listar os nomes completos de funções no binário especificado.|
|**Incluir:**`funcspec`|Determina uma especificação de função em um binário para instrumentar com testes. Todas as outras funções nos binários não são instrumentadas.<br /><br /> Você pode determinar várias especificações de função com opções **Include** separadas.<br /><br /> Não use as opções **Include** e **Exclude** que se referem a funções no mesmo binário.<br /><br /> Não há suporte para **Include** com cobertura de código.<br /><br /> `funcspec` é definida como:<br /><br /> [namespace \<separator1> ] [classe \<separator2> ] funcionamento<br /><br /> \<separator1> é `::` para código nativo e `.` para código gerenciado.<br /><br /> \<separator2> é sempre `::`<br /><br /> Há suporte para o caractere curinga \*. Por exemplo, para incluir todas as funções em um namespace, use:<br /><br /> MyNamespace::\*<br /><br /> Você pode usar **VSInstr /DumpFuncs** para listar os nomes completos de funções no binário especificado.|
|**DumpFuncs**|Lista as funções dentro da imagem especificada. Nenhuma instrumentação é executada.|
|**ExcludeSmallFuncs**|Exclui funções pequenas, que são funções curtas que não fazem chamadas de função, da instrumentação. A opção **ExcludeSmallFuncs** oferece menos sobrecarga devido à instrumentação, portanto, uma velocidade de instrumentação aprimorada.<br /><br /> A exclusão de funções pequenas também reduz o tamanho do arquivo .*vsp* e o tempo necessário para análise.|
|**Marca:**{**Antes**\|**Depois**\|**Superior**\|**Inferior**}`,funcname,markid`|Insere uma marca de perfil (um identificador usado para delimitar os dados em relatórios) que você pode usar para identificar o início ou término de um intervalo de dados no arquivo de relatório. vsp.<br /><br /> **Antes** -imediatamente antes da entrada da função de destino.<br /><br /> **After** – Imediatamente depois da saída da função de destino.<br /><br /> **Top** – Imediatamente depois da entrada da função de destino.<br /><br /> **Bottom** – Imediatamente antes de cada retorno na função de destino.<br /><br /> `funcname` – Nome da função de destino<br /><br /> `Markid` – Um inteiro positivo (longo) para usar como o identificador da marca de perfil.|
|**Cobertura**|Executa a instrumentação de cobertura. Pode ser usado apenas com as seguintes opções: **Verbose**, **OutputPath**, **Exclude** e **Logfile**.|
|**Verbose**|A opção **Verbose** é usada para exibir informações detalhadas sobre o processo de instrumentação.|
|**Nowarn**`[:[Message Number[;Message Number]]]`|Suprime todos os avisos ou avisos específicos.<br /><br /> `Message Number` – o número o aviso. Se `Message Number` for omitido, todos os avisos serão suprimidos.<br /><br /> Para obter mais informações, consulte [Avisos VSInstr](../profiling/vsinstr-warnings.md).|
|**Controle:** `{` **Thread** \| do **Processo** \| do **Global**`}`|Especifica o nível de criação de perfil das seguintes opções de controle de coleta de dados VSInstr:<br /><br /> **Iniciar**<br /><br /> **StartOnly**<br /><br /> **Suspend**<br /><br /> **StopOnly**<br /><br /> **SuspendOnly**<br /><br /> **ResumeOnly**<br /><br /> **Thread** – Especifica as funções de controle da coleta de dados de nível de thread. A criação de perfil é iniciada ou interrompida somente para o thread atual. O estado da criação de perfil de outros threads não é afetado. O padrão é thread.<br /><br /> **Process** – Especifica as funções de controle da coleta de dados da criação de perfil em nível de processo. A criação de perfil é iniciada ou interrompida para todos os threads no processo atual. O estado da criação de perfil de outros processos não é afetado.<br /><br /> **Global** – Especifica as funções de controle de coleta de dados em nível global (processo cruzado).<br /><br /> Se você não especificar o nível de criação de perfil, ocorrerá um erro.|
|**Início:** `{` **Dentro** \| de **Fora** do `},funcname`|Limita a coleta de dados à função de destino e a funções filho chamadas por essa função.<br /><br /> **Inside** – Insere a função StartProfile imediatamente após a entrada na função de destino. Insere a função StopProfile imediatamente antes de cada retorno na função de destino.<br /><br /> **Outside** – Insere a função StartProfile imediatamente antes de cada chamada à função de destino. Insere a função StopProfile imediatamente depois de cada chamada à função de destino.<br /><br /> `funcname` – o nome da função de destino.|
|**Suspender:** `{` **Dentro** \| de **Fora** do `},funcname`|Exclui a coleta de dados da função de destino e das funções filho chamadas por essa função.<br /><br /> **Inside** – Insere a função SuspendProfile imediatamente após a entrada na função de destino. Insere a função ResumeProfile imediatamente antes de cada retorno na função de destino.<br /><br /> **Outside** – Insere a função SuspendProfile imediatamente antes da entrada na função de destino. Insere a função ResumeProfile imediatamente antes da entrada da função de destino.<br /><br /> `funcname` – nome da função de destino.<br /><br /> Se a função de destino contiver uma função StartProfile, a função SuspendProfile será inserida antes dela. Se a função de destino contiver uma função StopProfile, a função ResumeProfile será inserida depois dela.|
|**StartOnly:** `{` **Before** \| **After** \| **Top** \| **Bottom** `},funcname`|Inicia a coleta de dados durante uma execução de criação de perfil. Insere a função API StartProfile no local especificado.<br /><br /> **Before** – Imediatamente antes da entrada da função de destino.<br /><br /> **After** -imediatamente após a saída da função de destino.<br /><br /> **Top** -imediatamente após a entrada da função de destino.<br /><br /> **Inferior** -imediatamente antes de cada retorno na função de destino.<br /><br /> `funcname` – nome da função de destino.|
|**StopOnly:**{**Before**\|**After**\|**Top**\|**Bottom**}`,funcname`|Para a coleta de dados durante uma execução de criação de perfil. Insere a função StopProfile no local especificado.<br /><br /> **Before** – Imediatamente antes da entrada da função de destino.<br /><br /> **After** -imediatamente após a saída da função de destino.<br /><br /> **Top** -imediatamente após a entrada da função de destino.<br /><br /> **Inferior** -imediatamente antes de cada retorno na função de destino.<br /><br /> `funcname` – nome da função de destino.|
|**SuspendOnly:**{**Before**\|**After**\|**Top**\|**Bottom**}`,funcname`|Para a coleta de dados durante uma execução de criação de perfil. Insere a API SuspendProfile no local especificado.<br /><br /> **Before** – Imediatamente antes da entrada da função de destino.<br /><br /> **After** -imediatamente após a saída da função de destino.<br /><br /> **Top** -imediatamente após a entrada da função de destino.<br /><br /> **Inferior** -imediatamente antes de cada retorno na função de destino.<br /><br /> `funcname` – nome da função de destino.<br /><br /> Se a função de destino contiver uma função StartProfile, a função SuspendProfile será inserida antes dela.|
|**ResumeOnly:**{**Before**\|**After**\|**Top**\|**Bottom**}`,funcname`|Inicia ou retoma a coleta de dados durante uma execução de criação de perfil.<br /><br /> Geralmente é usado para iniciar a criação de perfil depois que uma opção **SuspendOnly** interrompe a criação de perfil. Insere a API ResumeProfile no local especificado.<br /><br /> **Before** – Imediatamente antes da entrada da função de destino.<br /><br /> **After** -imediatamente após a saída da função de destino.<br /><br /> **Top** -imediatamente após a entrada da função de destino.<br /><br /> **Inferior** -imediatamente antes de cada retorno na função de destino.<br /><br /> `funcname` – nome da função de destino.<br /><br /> Se a função de destino contiver uma função StopProfile, a função ResumeProfile será inserida depois dela.|

## <a name="see-also"></a>Confira também
- [VSPerfMon](../profiling/vsperfmon.md)
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [VSPerfReport](../profiling/vsperfreport.md)
- [Avisos de VSInstr](../profiling/vsinstr-warnings.md)
- [Exibições de relatório de desempenho](../profiling/performance-report-views.md)
