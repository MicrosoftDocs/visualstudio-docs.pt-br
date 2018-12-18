---
title: Salvando informações de símbolo com arquivos de dados de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- packsymbols, in profiling tools reports
- profiling tools, packsymbols
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b5a485baaa1fdeab4a0d4c61b82f5381a931ac85
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49897180"
---
# <a name="saving-symbol-information-with-performance-data-files"></a>Salvando informações de símbolo com arquivos de dados de desempenho

Se você estiver usando o IDE do Visual Studio para analisar arquivos e pretender mover o arquivo VSP para um computador diferente, você deverá definir as configurações de projeto de desempenho para salvar ou *serializar* símbolos no arquivo de relatório. No entanto, isso aumenta o tamanho de um arquivo de relatório. A serialização de símbolos é necessária por dois motivos:

- Para inserir símbolos de código em um relatório de desempenho antes que ocorra a perda dos assemblies de destino de seu local no armazenamento temporário.

- Para preservar os símbolos, de modo que o relatório de desempenho seja portátil do computador com perfil criado e tenha como saída as mesmas informações que seriam apresentadas se o relatório fosse aberto para análise em outro computador, o que poderia apresentar símbolos diferentes.

Você pode serializar símbolos no IDE do Visual Studio ou na linha de comando:

- Para serializar os símbolos no IDE [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], aponte para **Ferramentas** na barra de menus e depois clique em **Opções**. Na janela **Opções**, selecione **Ferramentas de Desempenho** e, em seguida, selecione a caixa de seleção **Serializar informações de símbolo automaticamente**.

- Ao salvar arquivos de relatório, PACKSYMBOLS é a opção de linha de comando equivalente. Para serializar os símbolos, digite **vsperfreport /summary:all /packsymbols filename.vsp**.

## <a name="troubleshooting-symbol-problems"></a>Solução de problemas de símbolo

Se você não vir nenhum símbolos em seu próprio código, há soluções comuns disponíveis:

- Execute vsperfreport /debugsympath na linha de comando para exibir uma lista completa dos locais nos quais os componentes do criador de perfil estão carregando informações de símbolo e se os arquivos de símbolo usados correspondem aos arquivos que seu projeto está usando.

- Certifique-se executar vsperfreport com o sinalizador /PACKSYMBOLS ou, no IDE [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], o que você tem a opção de informações de símbolo serialize selecionada nas opções gerais do gerenciador de desempenho.

- Se você tiver coletado dados de tipo, adicione /SUMMARY:TYPE à linha de comando de vsperfreport.

  Se você não vir os símbolos do Windows ou outros programas da Microsoft:

- Certifique-se de ter configurado o caminho do seu cache de símbolos do Windows. Siga um destes procedimentos para definir o caminho do cache de símbolos:

  - Definir a opção Depurador-> Símbolos no IDE [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para o caminho correto.

  - Adicionar a opção -symbolpath à linha de comando do VSPerfReport para incluir os símbolos.

- Se você não vir os símbolos no [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], certifique-se de que o servidor de símbolos esteja configurado corretamente para o servidor ASP.

## <a name="repacking-symbols"></a>Recompactando símbolos

Se você quiser compactar novamente os símbolos em um relatório, você poderá fazer isso usando a ferramenta de linha de comando VsPerfReport. Use as seguintes linhas de comando:

VsPerfReport -clearpackedsymbols filename.vsp

VsPerfReport -packsymbols -summary:all filename.vsp

## <a name="see-also"></a>Consulte também

[Salvando e exportando dados de ferramentas de desempenho](../profiling/saving-and-exporting-performance-tools-data.md)  
[Como fazer referência a informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md)  
[VSPerfReport](../profiling/vsperfreport.md)