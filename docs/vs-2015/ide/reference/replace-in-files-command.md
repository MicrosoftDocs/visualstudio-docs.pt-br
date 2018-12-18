---
title: Comando Substituir nos arquivos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- edit.replaceinfiles
helpviewer_keywords:
- Edit.ReplaceInFiles command
- Replace In Files command
- ReplaceInFiles command
ms.assetid: f116066a-4f65-4f2c-94ef-12cbd8cfb598
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: eba6dfcf95c006fb05d4faaa0c370c9dba56e4e7
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49197659"
---
# <a name="replace-in-files-command"></a>Comando Substituir nos Arquivos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Substitui texto em arquivos usando um subconjunto das opções disponíveis na guia **Substituir nos Arquivos** da janela **Localizar e Substituir**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Edit.ReplaceinFiles findwhat replacewith [/all] [/case]  
[/ext:extensions] [/keep] [/lookin:searchpath] [/options] [/regex]  
[/reset] [/stop] [/sub] [/text2] [/wild] [/word]  
```  
  
## <a name="arguments"></a>Arguments  
 `findwhat`  
 Necessário. O texto a ser correspondido.  
  
 `replacewith`  
 Necessário. O texto a ser substituído pelo texto correspondido.  
  
## <a name="switches"></a>Opções  
 /all ou /a  
 Opcional. Substitui todas as ocorrências do texto da pesquisa pelo texto de substituição.  
  
 /case ou /c  
 Opcional. As correspondências ocorrerão somente se os caracteres maiúsculos e minúsculos corresponderem exatamente aos especificados no argumento `findwhat`.  
  
 /ext: `extensions`  
 Opcional. Especifica as extensões de arquivo para os arquivos a serem pesquisados.  
  
 /keep ou /k  
 Opcional. Especifica que todos os arquivos modificados são deixados abertos.  
  
 /lookin: `searchpath`  
 Opcional. Diretório a pesquisar. Se o caminho contiver espaços, coloque todo o caminho entre aspas.  
  
 /options ou /t  
 Opcional. Exibe uma lista das configurações atuais da opção de localização e não realiza uma pesquisa.  
  
 /regex ou /r  
 Opcional. Usa caracteres especiais predefinidos no argumento `findwhat` como notações que representam padrões de texto, em vez de caracteres literais. Para obter uma lista completa de caracteres de expressão regular, consulte [Expressões Regulares](../../ide/using-regular-expressions-in-visual-studio.md).  
  
 /reset ou /e  
 Opcional. Retorna as opções de localização para suas configurações padrão e não realiza uma pesquisa.  
  
 /stop  
 Opcional. Interromperá a operação de pesquisa atual se houver uma em andamento. Substituir ignorará todos os outros argumentos quando `/stop` tiver sido especificado. Por exemplo, para interromper a substituição atual, você digitaria o seguinte:  
  
```  
>Edit.ReplaceinFiles /stop  
```  
  
 /sub ou /s  
 Opcional. Procura as subpastas dentro do diretório especificado no argumento /lookin:`searchpath`.  
  
 /text2 ou /2  
 Opcional. Exibe os resultados da substituição na janela **Localizar Resultados 2**.  
  
 /wild ou /l  
 Opcional. Usa caracteres especiais predefinidos no argumento `findwhat` como notações para representar um caractere ou uma sequência de caracteres.  
  
 /word ou /w  
 Opcional. Pesquisa somente palavras inteiras.  
  
## <a name="example"></a>Exemplo  
 Este exemplo pesquisa `btnCancel` e o substitui por `btnReset` em todos os arquivos .cls localizados na pasta "Meus Projetos do Visual Studio" e exibe as informações de substituição na janela **Localizar Resultados 2** janela.  
  
```  
>Edit.ReplaceinFiles btnCancel btnReset /lookin:"c:/my visual studio projects" /ext:.cls /text2  
```  
  
## <a name="see-also"></a>Consulte também  
 [Localizando e substituindo texto](../../ide/finding-and-replacing-text.md)   
 [Substituir nos Arquivos](../../ide/replace-in-files.md)   
 [Janela Comando](../../ide/reference/command-window.md)   
 [Caixa Localizar/Comando](../../ide/find-command-box.md)   
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)   
 [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)



