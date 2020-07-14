---
title: VSPerfASPNetCmd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- profiling tools,VSPerfASPNETCmd
- VSPerfASPNETCmd
ms.assetid: f9e9f895-57bb-41e8-8bd1-cdaa738ec220
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: b6ddadc15a5e0d53535b82d87aadd31fec65adaf
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330480"
---
# <a name="vsperfaspnetcmd"></a>VSPerfASPNetCmd
A ferramenta de linha de comando **VSPerfASPNetCmd.exe** permite que você crie o perfil de sites da Web do ASP.NET sem exigir que você defina variáveis de ambiente ou reinicie o computador. Use **VSPerfASPNetCmd.exe** em vez de [VSPerfCmd](../profiling/vsperfcmd.md) quando estiver criando o perfil de sites do ASP.NET e não precisar da funcionalidade adicional fornecida pelo **VSPerfCmd**. Para obter mais informações sobre o **VSPerfASPNETCmd**, consulte [Rapid Web site profiling with VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md). **VSPerfASPNETCmd** é a ferramenta de linha de comando preferida a ser usada quando você estiver usando o criador de perfil autônomo para fazer o profile de um site da web do ASP.net.

## <a name="syntax"></a>Sintaxe
 **vsperfaspnetcmd** [/*Options*] *Website*

## <a name="options"></a>Opções

|Opção|Descrição|
|------------|-----------------|
|**/Sample** ou **/s**|Cria perfil de site usando o método de amostragem. **/Sample** é o método padrão. /Sample não pode ser usado com **/Trace**.|
|**/Trace** ou **/t**|Cria perfil de site usando o método de instrumentação. /Trace não pode ser usado com **/Sample**.|
|**/Memory**[**:** `Type` ] ou **/m**[**:**{**a**&#124;**l**}]|Cria perfil de alocação de memória e, opcionalmente, cria perfil de tempos de vida do objeto (coleta de lixo). **/Memory** pode ser usado com o método de amostragem ou instrumentação.<br /><br /> *Tipo* pode ser um dos seguintes:<br /><br /> -   **alocação** (ou **a**) coleta apenas dados de alocação de memória.<br />-   **tempo de vida** (ou **l**) coleta dados de alocação de memória e de tempo de vida do objeto.<br /><br /> O `Type` padrão é **alocação**.|
|**/Tip** ou **/i**|Adiciona informações detalhadas de solicitação ASP.NET e de chamada de ADO.NET para os dados de criação de perfil. **/Tip** pode ser usado com o método de amostragem ou instrumentação e pode ser usado com a opção **/Memory**.|
|**/Output:** `File` ou   **/o:**`File`|Especifica o caminho e o nome do arquivo dos dados de criação de perfil (.* VSP*).|
|**/NoWait** ou **/n**|Retorna o prompt de comando imediatamente para que os comandos adicionais possam ser usados na janela do prompt de comando. Você deve digitar **VSPerfASPNETCmd /Shutdown** em uma linha de comando separada para desativar a criação de perfil.|
|**/PackSymbols**[:{**on**&#124;**off**}ou   **/p**[:{**on**&#124;**off**}|Insere símbolos (nomes de função e parâmetro, etc.) no arquivo de dados de criação de perfil (.*vsp*).|
|**/Shutdown:** `Website`ou **/d:**`Website`|Desativa a criação de perfil. Use como a única opção na linha de comando depois de usar a opção **/NoWait** para iniciar a criação de perfil ou se o criador de perfil encerrar inesperadamente. Especifique a mesma URL que você usou no comando original **VSPerfASPNETCmd**.|
|`Website`|A URL do site para criação de perfil.|

## <a name="see-also"></a>Veja também
- [Criação rápida de perfil de site com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)
- [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)
