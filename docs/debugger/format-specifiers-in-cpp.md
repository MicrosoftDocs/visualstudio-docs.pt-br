---
title: Formatar especificadores no depurador (C++) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
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
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 73cd5655a5cb843c29fb628a2ec233860410dc7c
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305735"
---
# <a name="format-specifiers-for-c-in-the-visual-studio-debugger"></a>Especificadores de formato para C++ no depurador do Visual Studio
Você pode alterar o formato no qual um valor é exibido na **inspeção** janela usando especificadores de formato.  
  
 Você também pode usar especificadores de formato na **Immediate** janela, o **comando** janela, na [tracepoints](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)e até mesmo em janelas de origem. Se você pausar em uma expressão nessas janelas, o resultado é exibido em uma [DataTip](../debugger/view-data-values-in-data-tips-in-the-code-editor.md). A exibição de DataTip reflete o especificador de formato.  
  
> [!NOTE]
>  Quando o depurador nativo do Visual Studio é alterado para um novo mecanismo de depuração, alguns novos especificadores de formato foram adicionados e alguns antigos foram removidos. O depurador antigo ainda é usado quando você fizer interop (nativa e gerenciada combinadas) depuração com c++ CLI. 
  
## <a name="set-format-specifiers"></a>Especificadores de formato de conjunto  
Vamos usar o código de exemplo a seguir:  
  
```C++  
int main() {  
    int my_var1 = 0x0065;  
    int my_var2 = 0x0066;  
    int my_var3 = 0x0067;  
}  
```  
  
 Adicione a `my_var1` variável para o **inspeção** janela durante a depuração, **depurar** > **Windows** > **Assista**  >  **Assista 1**. Em seguida, a variável com o botão direito e selecione **exibição Hexadecimal**. Agora o **inspeção** janela mostra o valor 0x0065. Para ver esse valor, expresso como um caractere em vez de um número inteiro, primeiro clique com botão direito e desmarque **exibição Hexadecimal**. Em seguida, adicione o especificador de formato de caractere **, c** na **nome** coluna após o nome da variável. O **valor** coluna agora mostra **101 'e'**.  
  
 ![WatchFormatCPlus1](../debugger/media/watchformatcplus1.png "WatchFormatCPlus1")  
  
##  <a name="BKMK_Visual_Studio_2012_format_specifiers"></a> Especificadores de formato  
 As tabelas a seguir descrevem os especificadores de formato que você pode usar no Visual Studio. Especificadores em negrito têm suporte apenas para o novo depurador e não para depuração interop com C + + / CLI.  
  
|Especificador|Formatar|Valor original de inspeção|Valor exibido|  
|---------------|------------|--------------------------|---------------------|  
|d|inteiro decimal|0x00000066|102|  
|o|inteiro octal não assinado|0x00000066|000000000146|  
|x<br /><br /> **h**|inteiro hexadecimal|102|0xCCCCCCCC|  
|X<br /><br /> **H**|inteiro hexadecimal|102|0xCCCCCCCC|  
|c|caractere único|0x0065, c|101 'e'|  
|s|Const char * cadeia de caracteres (com aspas)|\<local > "hello world"|"hello world"|  
|**sb**|cadeia de caracteres const char* (sem aspas)|\<local > "hello world"|hello world|  
|s8|Cadeia de caracteres UTF-8|\<local > "Este é um â˜• xícara de café de UTF-8"|"Este é um ☕ xícara de café de UTF-8"|
|**s8b**|Cadeia de caracteres UTF-8 (sem aspas)|\<local > "hello world"|hello world|  
|su|Cadeia de caracteres Unicode (codificação UTF-16) (com aspas)|\<local > L "hello world"|L"hello world"<br /><br /> u "hello world"|  
|sub|Cadeia de caracteres Unicode (codificação UTF-16) (sem aspas)|\<local > L "hello world"|hello world|  
|bstr|Cadeia de caracteres binária (com aspas) BSTR|\<local > L "hello world"|L"hello world"|  
|env|Bloco de ambiente (cadeia de caracteres terminada em nulo duplo)|\<local > L "=:: =::\\\\"|L "=:: =::\\\\\\0 = C: = C:\\\\windows\\\\system32\\0ALLUSERSPROFILE =...|
|**s32**|Cadeia de caracteres UTF-32 (com aspas)|\<local > U "hello world"|u "hello world"|  
|**s32b**|Cadeia de caracteres UTF-32 (sem aspas)|\<local > U "hello world"|hello world|  
|**en**|enum|Saturday(6)|Sábado|  
|**hv**|Tipo de ponteiro - indica que o valor do ponteiro está sendo inspecionado é o resultado da alocação de heap de uma matriz, por exemplo, `new int[3]`.|\<local > {\<primeiro membro >}|\<local > {\<primeiro membro >, \<segundo membro >,...}|  
|**na**|Inibe o endereço de memória de um ponteiro para um objeto.|\<local >, {membro = valor...}|{membro = valor...}|  
|**nd**|Exibe somente as informações de classe base, ignorando classes derivadas|`(Shape*) square` inclui a classe base e derivadas informações de classe|Exibe somente informações de classe de base|  
|hr|Código de erro HRESULT ou Win32. Esse especificador não é necessário para HRESULTs como o depurador decodifica automaticamente.|S_OK|S_OK|  
|wc|Sinalizador de classe do Windows|0x0010|WC_DEFAULTCHAR|  
|wm|Números de mensagens do Windows|16|WM_CLOSE|  
|!|formato bruto, ignorando qualquer personalização de exibições de tipo de dados|\<personalizado representação >|4|  
  
> [!NOTE]
>  Quando o **hv** especificador de formato estiver presente, o depurador tenta determinar o comprimento do buffer e exibir esse número de elementos. Como nem sempre é possível que o depurador localizar o tamanho do buffer exata de uma matriz, você deve usar um especificador de tamanho `(pBuffer,[bufferSize])` sempre que possível. O **hv** especificador de formato é útil quando o tamanho do buffer não está prontamente disponível  
  
###  <a name="BKMK_Size_specifiers_for_pointers_as_arrays_in_Visual_Studio_2012"></a> Especificadores de tamanho para ponteiros como matrizes  
 Se você tiver um ponteiro para um objeto que queira exibir como uma matriz, poderá usar um inteiro ou uma expressão para especificar o número de elementos da matriz. 
  
|Especificador|Formatar|Valor original de inspeção|Valor exibido|  
|---------------|------------|---------------------------|---------------------|  
|n|Inteiro decimal ou inteiro **hexadecimal**|pBuffer,[32]<br /><br /> pBuffer,**[0x20]**|Exibe `pBuffer` como uma matriz de 32 elementos.|  
|**[exp]**|Uma expressão C++ válida que é avaliada como um inteiro.|pBuffer,[bufferSize]|Exibe pBuffer como uma matriz de `bufferSize` elementos.|  
|**expand(n)**|Uma expressão C++ válida que é avaliada como um inteiro|pBuffer, expand(2)|Exibe o terceiro elemento da  `pBuffer`|  
  
##  <a name="BKMK_Format_specifiers_for_interop_debugging_and_C___edit_and_continue"></a> Especificadores de formato para depuração interop com c++ CLI  
 Especificadores em **negrito** têm suporte somente para depuração nativos e c++ /CLI código CLI.  
  
|Especificador|Formatar|Valor original de inspeção|Valor exibido|  
|---------------|------------|--------------------------|---------------------|  
|**d**<br /><br />**i**|inteiro decimal assinado|0xF000F065|-268373915|  
|**u**|inteiro decimal não assinado|0x0065|101|  
|o|inteiro octal não assinado|0xF065|0170145|  
|x<br /><br />X|Inteiro hexadecimal|61541|0x0000f065|  
|**l**<br /><br />**h**|prefixo longo ou curto para: d, i, u, o, x, X|00406042|0x0c22|  
|**f**|ponto flutuante assinado|(3./2.), f|1,500000|  
|**e**|notação científica assinada|(2.0/3.0)|1.500000e+000|  
|**g**|ponto flutuante assinado ou notação científica assinada,<br/> o que for menor|(2.0/3.0)|1.5|  
|c|caractere único|\<localização>|101 'e'|  
|s|Const char * (com aspas)|\<localização>|"hello world"|  
|su|const wchar_t*<br /><br /> char16_t const\* (com aspas)|\<localização>|L"hello world"|  
|sub|const wchar_t*<br /><br /> char16_t const\*|\<localização>|hello world|  
|s8|Const char * (com aspas)|\<localização>|"hello world"|  
|hr|Código de erro HRESULT ou Win32.<br/>Esse especificador não é necessário para HRESULTs como o depurador decodifica automaticamente.|S_OK|S_OK|  
|wc|Sinalizador de classe do Windows|0x00000040,|WC_DEFAULTCHAR|  
|wm|Números de mensagens do Windows|0x0010|WM_CLOSE|  
|!|formato bruto, ignorando qualquer personalização de modo de exibição do tipo de dados|\<personalizado representação >|4|  
  
###  <a name="BKMK_Format_specifiers_memory_locations_in_interop_debugging_and_C___edit_and_continue"></a> Formatar os especificadores de locais de memória em depuração interop com C + + / CLI  
 A tabela a seguir descreve os símbolos de formatação usados para locais de memória. Você pode usar um especificador de local da memória com qualquer valor ou expressão que seja avaliada como um local.  
  
|Símbolo|Formatar|Valor original de inspeção|Valor exibido|  
|------------|------------|--------------------------|---------------------|  
|**ma**|Caracteres ASCII na base 64|0x0012ffac|0x0012ffac .4...0...".0W&.......1W&.0.:W..1...."..1.JO&.1.2.."..1...0y....1|  
|**m**|16 bytes em hexadecimal, seguidos caracteres ASCII na base 16|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|  
|**mb**|16 bytes em hexadecimal, seguidos caracteres ASCII na base 16|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|  
|**mw**|8 palavras|0x0012ffac|0x0012ffac 34B3 00CB 3084 8094 22FF 308A 2657 0000|  
|**md**|4 palavra duplas|0x0012ffac|0x0012ffac 00CB34B3 80943084 308A22FF 00002657|  
|**mq**|2 palavras quádruplas|0x0012ffac|0x0012ffac 7ffdf00000000000 5f441a790012fdd4|  
|**mu**|Caracteres de 2 bytes (Unicode)|0x0012ffac|0x0012ffac 8478 77f4 ffff ffff 0000 0000 0000 0000|  
  
###  <a name="BKMK_Size_specifier_for_pointers_as_arrays_in_interop_debugging_and_C___edit_and_continue"></a> Especificador de tamanho para ponteiros como matrizes em depuração interop com c++ CLI  
 Se você tiver um ponteiro para um objeto que você deseja exibir como uma matriz, poderá usar um inteiro para especificar o número de elementos da matriz.
  
|Especificador|Formatar|Expressão|Valor exibido|  
|---------------|------------|----------------|---------------------|  
|n|Inteiro decimal|pBuffer[32]|Exibe `pBuffer` como uma matriz de 32 elementos.|
