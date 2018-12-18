---
title: Formatar especificadores em c# | Microsoft Docs
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
- CSharp
helpviewer_keywords:
- expressions [C#], formatting values
- variables [debugger], watch variable symbols
- symbols, watch variable formatting
- QuickWatch dialog box, using format specifiers
- specifiers, watch variable format
- QuickWatch dialog box, format specifiers in C#
- specifiers
- watch variable symbols
- Watch window, format specifiers in C#
- format specifiers, debugger
- debugger, format specifiers recognized by
ms.assetid: 345c8589-5f36-4d34-a58c-e56271687dd6
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 330a32b20eeab172ebf36e49f16e79aa936a1bdc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51754165"
---
# <a name="format-specifiers-in-c"></a>Especificadores de formato em C# #
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode alterar o formato no qual um valor é exibido na **inspeção** janela usando especificadores de formato. Você também pode usar especificadores de formato na **Immediate** janela, o **comando** janela e até mesmo em janelas de origem. Se você pausar em uma expressão nessas janelas, o resultado aparecerá em uma DataTip. As DataTips refletirão o especificador de formato na tela DataTip.  
  
 Para usar um especificador de formato, digite a expressão seguida por uma vírgula. Após a vírgula, adicione o especificador apropriado.  
  
## <a name="using-format-specifiers"></a>Usando especificadores de formato  
 Se você tiver o seguinte código:  
  
```  
{  
        int my_var1 = 0x0065;  
        int my_var2 = 0x0066;  
        int my_var3 = 0x0067;  
}  
```  
  
 Adicionar o `my_var1` variável à janela Inspeção (durante a depuração, **depurar / Windows / Assista / Assista 1**) e definir a exibição em hexadecimal (no **inspeção** janela, a variável com o botão direito e selecione **Exibição hexadecimal**). Agora o **inspeção** janela mostra que ele contém o valor 0x0065. Para ver esse valor, expresso como um inteiro decimal em vez de um inteiro hexadecimal, na coluna Nome, após o nome da variável, adicione o especificador de formato decimal: **, d**. A coluna de valor agora exibe o valor decimal 101  
  
 ![WatchFormatCSharp](../debugger/media/watchformatcsharp.png "WatchFormatCSharp")  
  
## <a name="format-specifiers"></a>Especificadores de formato  
 A tabela a seguir exibe os especificadores de formato C# reconhecidos pelo depurador.  
  
|Especificador|Formatar|Valor original de inspeção|Telas|  
|---------------|------------|--------------------------|--------------|  
|CA|Forçar avaliação de uma expressão. Isso pode ser útil quando a avaliação implícita das propriedades e das chamadas de função implícitas é desativada. Ver [efeitos colaterais e expressões](http://msdn.microsoft.com/library/e1f8a6ea-9e19-481d-b6bd-df120ad3bf4e).|"Avaliação da função implícita está desativada pelo usuário" da mensagem|\<value>|  
|d|inteiro decimal|0x0065|101|  
|dinâmica|Exibe o objeto especificado usando um Modo de Exibição Dinâmico|Exibe todos os membros do objeto, incluindo o modo de exibição dinâmico|Exibe apenas o modo de exibição dinâmico|  
|h|inteiro hexadecimal|61541|0x0000F065|  
|nq|cadeia de caracteres sem aspas|"Minha cadeia de caracteres"|Minha cadeia de caracteres|  
|oculto|Exibe todos os membros públicos e não públicos|Exibe os membros públicos|Exibe todos os membros|  
|bruto|Exibe o item como aparece no nó bruto do item. Válido apenas em objetos proxy.|Dicionário\<T >|Modo de exibição bruto do dicionário\<T >|  
|resultados|Usado com uma variável de um tipo que implementa IEnumerable ou IEnumerable\<T >, geralmente o resultado de uma expressão de consulta. Exibe apenas os membros que contém o resultado da consulta.|Exibe todos os membros.|Exibe os membros que atendam as condições da consulta.|  
  
## <a name="see-also"></a>Consulte também  
 [Inspeção e QuickWatch Windows](../debugger/watch-and-quickwatch-windows.md)   
 [Windows variável](http://msdn.microsoft.com/library/ce0a67f6-2502-4b7a-ba45-cc32f8aeba3e)





