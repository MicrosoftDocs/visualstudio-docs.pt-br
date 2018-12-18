---
title: Formatar especificadores em C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- QuickWatch dialog box, format specifiers in C++
- variables [debugger], watch variable symbols
- symbols, watch variable formatting
- QuickWatch dialog box, using format specifiers
- expressions [C++], format specifiers
- specifiers, watch variable format
- specifiers
- Watch window, format specifiers in C++
- watch variable symbols
- format specifiers, debugger
- debugger, format specifiers recognized by
ms.assetid: 0f6f3b7c-ce2c-4b4d-b14f-7589dbed5444
caps.latest.revision: 45
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6634124e7dc0b50236a9fd6ff9c5c5388c3063bc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810514"
---
# <a name="format-specifiers-in-c"></a>Especificadores de formato em C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode alterar o formato no qual um valor é exibido na **inspeção** janela usando especificadores de formato.  
  
 Você também pode usar especificadores de formato na **Immediate** janela, o **comando** janela e até mesmo em janelas de origem. Se você pausar em uma expressão nessas janelas, o resultado aparecerá em uma DataTip. A exibição de DataTip reflete o especificador de formato.  
  
> [!NOTE]
>  O depurador nativo do Visual Studio foi alterado para um novo mecanismo de depuração. Como parte dessa alteração, alguns novos especificadores de formato foram adicionados e alguns antigos foram removidos. O depurador antigo ainda é usado quando você fizer interop (nativa e gerenciada combinadas) depuração com c++ CLI. As seções a seguir neste tópico mostram os especificadores de formato para cada mecanismo de depuração.  
> 
> - [Especificadores de formato](#BKMK_Visual_Studio_2012_format_specifiers) descreve os especificadores de formato no novo mecanismo de depuração.  
>   -   [Especificadores de formato para depuração interop com c++ CLI](#BKMK_Format_specifiers_for_interop_debugging_and_C___edit_and_continue) descreve os especificadores de formato no mecanismo de depuração antigo.  
  
## <a name="using-format-specifiers"></a>Usando especificadores de formato  
 Se você tiver o seguinte código:  
  
```cpp  
int main() {  
    int my_var1 = 0x0065;  
    int my_var2 = 0x0066;  
    int my_var3 = 0x0067;  
}  
```  
  
 Adicionar o `my_var1` variável para o **inspeção** janela (durante a depuração, **depurar / Windows / Assista / Assista 1**) e definir a exibição em hexadecimal (no **inspeção** janela, a variável com o botão direito e selecione **exibição Hexadecimal**). Agora, a janela Inspeção mostre que ela contém o valor 0x0065. Para ver esse valor, expresso como um caractere em vez de um inteiro, na coluna Nome, após o nome da variável, adicione o especificador de formato de caractere **, c**. O **valor** coluna agora aparece **101 'e'**.  
  
 ![WatchFormatCPlus1](../debugger/media/watchformatcplus1.png "WatchFormatCPlus1")  
  
##  <a name="BKMK_Visual_Studio_2012_format_specifiers"></a> Especificadores de formato  
 As tabelas a seguir mostram os especificadores de formato que você pode usar no Visual Studio. Não há suporte para especificadores em negrito para depuração interop com C + + / CLI.  
  
|Especificador|Formatar|Valor original de inspeção|Valor exibido|  
|---------------|------------|--------------------------|---------------------|  
|d|inteiro decimal|0x00000066|102|  
|o|inteiro octal não assinado|0x00000066|000000000146|  
|x<br /><br /> **h**|inteiro hexadecimal|102|0xcccccccc|  
|X<br /><br /> **H**|inteiro hexadecimal|102|0xCCCCCCCC|  
|c|caractere único|0x0065, c|101 'e'|  
|s|Const char * cadeia de caracteres|\<local > "hello world"|"hello world"|  
|**sb**|Const char * cadeia de caracteres|\<local > "hello world"|Olá, mundo|  
|s8|Const char * cadeia de caracteres|\<local > "hello world"|"hello world"|  
|**s8b**|Const char * cadeia de caracteres|\<local > "hello world"|"hello world"|  
|su|Const wchar_t * const<br /><br /> char16_t\* cadeia de caracteres|\<local > L "hello world"|L "hello world"<br /><br /> u "hello world"|  
|sub|Const wchar_t * const<br /><br /> char16_t\* cadeia de caracteres|\<local > L "hello world"|Olá, mundo|  
|bstr|Cadeia de caracteres BSTR|\<local > L "hello world"|L "hello world"|  
|**s32**|Cadeia de caracteres UTF-32|\<local > U "hello world"|U "hello world"|  
|**s32b**|Cadeia de caracteres UTF-32 (sem aspas)|\<local > U "hello world"|Olá, mundo|  
|**en**|enum|Saturday(6)|Sábado|  
|**hv**|Tipo de ponteiro - indica que o valor do ponteiro está sendo inspecionado é o resultado da alocação de heap de uma matriz, por exemplo, `new int[3]`.|\<local > {\<primeiro membro >}|\<local > {\<primeiro membro >, \<segundo membro >,...}|  
|**na**|Suprime o endereço de memória de um ponteiro para um objeto.|\<local >, {membro = valor...}|{membro = valor...}|  
|**nd**|Exibe apenas as informações de classe base, ignorando as classes derivadas|`(Shape*) square` inclui a classe base e derivadas informações de classe|Exibe somente informações de classe de base|  
|hr|Código de erro HRESULT ou Win32. (O depurador agora decodifica HRESULTs automaticamente. Portanto, esse especificador não é necessário nesses casos.|S_OK|S_OK|  
|wc|Sinalizador de classe de janela|0x0010|WC_DEFAULTCHAR|  
|wm|Números de mensagens do Windows|16|WM_CLOSE|  
|!|formato bruto, ignorando qualquer personalização de exibições de tipo de dados|\<personalizado representação >|4|  
  
> [!NOTE]
>  Quando o **hv** especificador de formato estiver presente, o depurador tenta determinar o comprimento do buffer e exibir o número apropriado de elementos. Como nem sempre é possível que o depurador localizar o tamanho do buffer exata de uma matriz, você deve usar um especificador de tamanho `(pBuffer,[bufferSize])` sempre que possível. O **hv** especificador de formato é destinado para cenários em que o tamanho do buffer não está prontamente disponível  
  
###  <a name="BKMK_Size_specifiers_for_pointers_as_arrays_in_Visual_Studio_2012"></a> Especificadores de tamanho para ponteiros como matrizes  
 Se você tiver um ponteiro para um objeto que queira exibir como uma matriz, pode usar um inteiro ou uma expressão para especificar o número de elementos da matriz:  
  
|Especificador|Formatar|Valuen original de inspeção|Valor exibido|  
|---------------|------------|---------------------------|---------------------|  
|n|Decimal ou **hexadecimal** inteiro|pBuffer,[32]<br /><br /> pBuffer,**[0x20]**|Exibe `pBuffer` como uma matriz de 32 elementos.|  
|**[exp]**|Uma expressão C++ válida que é avaliada como um inteiro.|pBuffer,[bufferSize]|Exibe pBuffer como uma matriz de `bufferSize` elementos.|  
|**expand(n)**|Uma expressão C++ válida que é avaliada como um número inteiro|pBuffer, expand(2)|Exibe o terceiro elemento da  `pBuffer`|  
  
##  <a name="BKMK_Format_specifiers_for_interop_debugging_and_C___edit_and_continue"></a> Especificadores de formato para depuração interop com c++ CLI  
 Especificadores em **negrito** têm suporte somente para depuração nativos e c++ /CLI código CLI.  
  
|Especificador|Formatar|Valor original de inspeção|Valor exibido|  
|---------------|------------|--------------------------|---------------------|  
|**1!d, eu**|inteiro decimal assinado|0xF000F065|-268373915|  
|**u**|inteiro decimal não assinado|0x0065|101|  
|o|inteiro octal não assinado|0xF065|0170145|  
|x,X|Inteiro hexadecimal|61541|0x0000f065|  
|**l, h**|prefixo longo ou curto para: d, i, u, o, x, X|00406042|0x0c22|  
|**f**|ponto flutuante assinado|(3./2.), f|1.500000|  
|**e**|notação científica assinada|(3.0/2.0)|1.500000e+000|  
|**g**|ponto flutuante assinado ou notação científica assinada, o que for menor|(3.0/2.0)|1.5|  
|c|caractere único|\<location>|101 'e'|  
|s|Const char *|\<location>|"hello world"|  
|su|Const wchar_t *<br /><br /> char16_t const\*|\<location>|L "hello world"|  
|sub|Const wchar_t *<br /><br /> char16_t const\*|\<location>|Olá, mundo|  
|s8|Const char *|\<location>|"hello world"|  
|hr|Código de erro HRESULT ou Win32. (O depurador agora decodifica HRESULTs automaticamente. Portanto, esse especificador não é necessário nesses casos.|S_OK|S_OK|  
|wc|Sinalizador de classe do Windows.|0x00000040,|WC_DEFAULTCHAR|  
|wm|Números de mensagens do Windows|0x0010|WM_CLOSE|  
|!|formato bruto, ignorando qualquer personalização de exibições de tipo de dados|\<personalizado representação >|4|  
  
###  <a name="BKMK_Format_specifiers_memory_locations_in_interop_debugging_and_C___edit_and_continue"></a> Formatar os locais de memória de especificadores em depuração interop com C + + / CLI  
 A tabela a seguir contém os símbolos de formatação usados para locais de memória. Você pode usar um especificador de local da memória com qualquer valor ou expressão que seja avaliada como um local.  
  
|Símbolo|Formatar|Valor original de inspeção|Valor exibido|  
|------------|------------|--------------------------|---------------------|  
|**ma**|Caracteres ASCII na base 64|0x0012ffac|0x0012ffac .4...0...".0W&.......1W&.0.:W..1...."..1.JO&.1.2.."..1...0y....1|  
|**m**|16 bytes em hexadecimal, seguidos caracteres ASCII na base 16|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|  
|**mb**|16 bytes em hexadecimal, seguidos caracteres ASCII na base 16|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|  
|**mw**|8 palavras|0x0012ffac|0x0012ffac 34B3 00CB 3084 8094 22FF 308A 2657 0000|  
|**md**|4 palavra duplas|0x0012ffac|0x0012ffac 00CB34B3 80943084 308A22FF 00002657|  
|**mq**|2 palavras quádruplas|0x0012ffac|0x0012ffac 7ffdf00000000000 5f441a790012fdd4|  
|**mu**|Caracteres de 2 bytes (Unicode)|0x0012ffac|0x0012ffac 8478 77f4 ffff ffff 0000 0000 0000 0000|  
  
###  <a name="BKMK_Size_specifier_for_pointers_as_arrays_in_interop_debugging_and_C___edit_and_continue"></a> Especificador de tamanho para ponteiros como matrizes em depuração interop com c++ /CLI CLIt  
 Se você tiver um ponteiro para um objeto que você deseja exibir como uma matriz, pode usar um inteiro para especificar o número de elementos da matriz:  
  
|Especificador|Formatar|Expressão|Valor exibido|  
|---------------|------------|----------------|---------------------|  
|n|Inteiro decimal|pBuffer[32]|Exibe `pBuffer` como uma matriz de 32 elementos.|





