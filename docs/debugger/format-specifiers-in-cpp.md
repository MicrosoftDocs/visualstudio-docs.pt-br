---
title: Especificadores de formato no depurador (C++) | Microsoft Docs
description: Use um especificador de formato para alterar o formato no qual um valor é exibido em uma janela Watch, Autos ou Locals. Este artigo fornece detalhes de uso.
ms.custom: SEO-VS-2020
ms.date: 3/11/2019
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
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
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: 868c02091814fe49ea0224190c7d205e8b67c42b
ms.sourcegitcommit: 4b2b6068846425f6964c1fd867370863fc4993ce
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2021
ms.locfileid: "112042971"
---
# <a name="format-specifiers-for-c-in-the-visual-studio-debugger"></a>Especificadores de formato para C++ no Visual Studio depurador

Você pode alterar o formato no qual um valor é exibido nas **janelas** Observar **,** **Autos** e Locais usando especificadores de formato.

Você também pode usar especificadores de  formato na janela Imediato, na janela Comando, nos pontos de rastreamento e até mesmo nas [janelas](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)de origem.  Se você pausar em uma expressão nessas janelas, o resultado será exibido em uma [DataTip](../debugger/view-data-values-in-data-tips-in-the-code-editor.md). A exibição DataTip reflete o especificador de formato.

> [!NOTE]
> Quando o Visual Studio depurador nativo foi alterado para um novo mecanismo de depuração, alguns novos especificadores de formato foram adicionados e alguns antigos foram removidos. O depurador mais antigo ainda é usado quando você faz a depuração de interop (nativa mista e gerenciada) com C++/CLI.

## <a name="set-format-specifiers"></a>Definir especificadores de formato

Vamos usar o seguinte código de exemplo:

```C++
int main() {
    int my_var1 = 0x0065;
    int my_var2 = 0x0066;
    int my_var3 = 0x0067;
}
```

Adicione a `my_var1` variável à **janela** Observar durante a depuração, **Depurar**  >  **o Windows**  >  **Watch**  >  **Watch 1**. Em seguida, clique com o botão direito do mouse na variável e **selecione Exibição Hexadecimal.** Agora, **a janela** Observar mostra o valor 0x0065. Para ver esse valor expresso como um caractere em vez de um inteiro, primeiro clique com o botão direito do mouse e desmarque Exibir **Hexadecimal**. Em seguida, adicione o especificador de formato de **caractere , c** na coluna **Nome** após o nome da variável. A **coluna** Valor agora mostra **101 'e'.**

![Captura de tela Visual Studio janela Inspeção com uma linha selecionada que mostra my_var1.c com um valor de 101 'e' e um tipo de int.](../debugger/media/watchformatcplus1.png)

::: moniker range=">= vs-2019" 
Você pode exibir e selecionar em uma lista de especificadores de formato disponíveis, ao lado de uma vírgula (,) com o valor na **janela** Observar. 

![WatchFormatSpecDropdown](../debugger/media/vs-2019/format-specs-cpp.png "FormatSpecCpp")

::: moniker-end

## <a name="format-specifiers"></a><a name="BKMK_Visual_Studio_2012_format_specifiers"></a> Especificadores de formato

As tabelas a seguir descrevem os especificadores de formato que você pode usar em Visual Studio. Os especificadores em negrito só têm suporte para o novo depurador e não para depuração de interop com C++/CLI.

::: moniker range=">= vs-2019" 

|Especificador|Formatar|Valor de Relógio Original|Valor exibido|
|---------------|------------|--------------------------|---------------------|
|d|inteiro decimal|0x00000066|102|
|o|inteiro octal não assinado|0x00000066|000000000146|
|x<br /><br /> **h**|inteiro hexadecimal|102|0xcccccccc|
|X<br /><br /> **H**|inteiro hexadecimal|102|0xCCCCCCCC|
|xb<br /><br /> **Hb**|inteiro hexadecimal (sem 0x à esquerda)|102|cccccccc|
|Xb<br /><br /> **Hb**|inteiro hexadecimal (sem 0x à esquerda)|102|CCCCCCCC|
|b|inteiro não assinado de binário|25|0b00000000000000000000000000011001|
|bb|inteiro não assinado de binário (sem 0b à esquerda)|25|00000000000000000000000000011001|
|e|notação científica|25000000|2.500000e+07|
|g|mais curto do ponto flutuante ou científico|25000000|2.5e+07|
|c|caractere único|0x0065|101 'e'|
|s|cadeia de caracteres const char* (com aspas)|\<location> "olá, mundo"|“Olá Mundo”|
|**Sb**|cadeia de caracteres const char* (sem aspas)|\<location> "olá, mundo"|hello world|
|s8|Cadeia de caracteres UTF-8|\<location> "Esta é uma cafeteira UTF-8 â•"|"Esta é uma cafeteira UTF-8 ☕"|
|**s8b**|Cadeia de caracteres UTF-8 (sem aspas)|\<location> "olá, mundo"|hello world|
|su|Cadeia de caracteres Unicode (codificação UTF-16) (com aspas)|\<location> L"hello world"|L"hello world"<br /><br /> u"hello world"|
|sub|Cadeia de caracteres Unicode (codificação UTF-16) (sem aspas)|\<location> L"hello world"|hello world|
|bstr|Cadeia de caracteres binária BSTR (com aspas)|\<location> L "Olá mundo"|L"hello world"|
|env|Bloco de ambiente (cadeia de caracteres terminada em nulo duplo)|\<location>L "=:: =:: \\ \\ "|L "=:: =:: \\ \\ \\ 0 = c: = c: \\ \\ Windows \\ \\ System32 \\ 0ALLUSERSPROFILE =...|
|**s32**|Cadeia de caracteres UTF-32 (com aspas)|\<location> U "Olá mundo"|U "Olá mundo"|
|**s32b**|Cadeia de caracteres UTF-32 (sem aspas)|\<location> U "Olá mundo"|hello world|
|**en**|enum|Saturday(6)|Sábado|
|**hv**|Tipo de ponteiro – indica que o valor do ponteiro sendo inspecionado é o resultado da alocação de heap de uma matriz, por exemplo, `new int[3]` .|\<location>{\<first member>}|\<location>{\<first member>, \<second member>, ...}|
|**na**|Inibe o endereço de memória de um ponteiro para um objeto.|\<location>, {member = Value...}|{member=value...}|
|**segunda**|Exibe somente as informações de classe base, ignorando classes derivadas|`(Shape*) square` inclui a classe base e as informações de classe derivada|Exibe somente informações da classe base|
|h|Código de erro HRESULT ou Win32. Esse especificador não é mais necessário para HRESULTs, pois o depurador os decodifica automaticamente.|S_OK|S_OK|
|wc|Sinalizador de classe do Windows|0x0010|WC_DEFAULTCHAR|
|wm|Números de mensagens do Windows|16|WM_CLOSE|
|nr|Suprimir item "Raw View"|
|nvo|Mostrar item "modo de exibição bruto" somente para valores numéricos|
|!|formato bruto, ignorando qualquer personalização de exibições de tipo de dados|\<customized representation>|4|
|processamento|Exibe informações sobre o identificador do Win32|0x000000000000009c| Exibe informações úteis sobre o identificador, como ID de thread, etc. |

::: moniker-end

::: moniker range="vs-2017" 

|Especificador|Formatar|Valor de inspeção original|Valor exibido|
|---------------|------------|--------------------------|---------------------|
|d|inteiro decimal|0x00000066|102|
|o|inteiro octal não assinado|0x00000066|000000000146|
|x<br /><br /> **h**|inteiro hexadecimal|102|0xcccccccc|
|X<br /><br /> **H**|inteiro hexadecimal|102|0xCCCCCCCC|
|c|caractere único|0x0065, c|101 'e'|
|s|const char * cadeia de caracteres (com aspas)|\<location> "Olá, mundo"|“Olá Mundo”|
|**SB**|cadeia de caracteres const char* (sem aspas)|\<location> "Olá, mundo"|hello world|
|s8|Cadeia de caracteres UTF-8|\<location> "Este é um UTF-8 Coffee Cup â ̃ •"|"Esta é uma xícara de café UTF-8 ☕"|
|**s8b**|Cadeia de caracteres UTF-8 (sem aspas)|\<location> "Olá, mundo"|hello world|
|su|Cadeia de caracteres Unicode (codificação UTF-16) (com aspas)|\<location> L "Olá mundo"|L"hello world"<br /><br /> u"hello world"|
|sub|Cadeia de caracteres Unicode (codificação UTF-16) (sem aspas)|\<location> L"hello world"|hello world|
|bstr|Cadeia de caracteres binária BSTR (com aspas)|\<location> L"hello world"|L"hello world"|
|env|Bloco de ambiente (cadeia de caracteres terminada em nulo duplo)|\<location>L"=::=:: \\ \\ "|L"=::=:: \\ \\ \\ 0=C:=C: \\ \\ windows \\ \\ system32 \\ 0ALLUSERSPROFILE=...|
|**s32**|Cadeia de caracteres UTF-32 (com aspas)|\<location> U"hello world"|U"hello world"|
|**s32b**|Cadeia de caracteres UTF-32 (sem aspas)|\<location> U"hello world"|hello world|
|**en**|enum|Saturday(6)|Sábado|
|**hv**|Tipo de ponteiro – indica que o valor do ponteiro que está sendo inspecionado é o resultado da alocação de heap de uma matriz, por exemplo, `new int[3]` .|\<location>{\<first member>}|\<location>{\<first member>, \<second member>, ...}|
|**na**|Inibe o endereço de memória de um ponteiro para um objeto.|\<location>, {member=value...}|{member=value...}|
|**Nd**|Exibe somente as informações de classe base, ignorando classes derivadas|`(Shape*) square` inclui informações de classe base e de classe derivada|Exibe apenas informações de classe base|
|h|Código de erro HRESULT ou Win32. Esse especificador não é mais necessário para HRESULTs, pois o depurador os decodifica automaticamente.|S_OK|S_OK|
|wc|Sinalizador de classe do Windows|0x0010|WC_DEFAULTCHAR|
|wm|Números de mensagens do Windows|16|WM_CLOSE|
|!|formato bruto, ignorando qualquer personalização de exibições de tipo de dados|\<customized representation>|4|

::: moniker-end

> [!NOTE]
> Quando o **especificador de formato hv** está presente, o depurador tenta determinar o comprimento do buffer e exibir esse número de elementos. Como nem sempre é possível para o depurador encontrar o tamanho exato do buffer de uma matriz, você deve usar um especificador de tamanho `(pBuffer,[bufferSize])` sempre que possível. O **especificador de formato hv** é útil quando o tamanho do buffer não está prontamente disponível.

### <a name="size-specifiers-for-pointers-as-arrays"></a><a name="BKMK_Size_specifiers_for_pointers_as_arrays_in_Visual_Studio_2012"></a> Especificadores de tamanho para ponteiros como matrizes

Se você tiver um ponteiro para um objeto que queira exibir como uma matriz, poderá usar um inteiro ou uma expressão para especificar o número de elementos da matriz.

|Especificador|Formatar|Valor de Relógio Original|Valor exibido|
|---------------|------------|---------------------------|---------------------|
|n|Inteiro decimal ou inteiro **hexadecimal**|pBuffer,[32]<br /><br /> pBuffer,**[0x20]**|Exibe como `pBuffer` uma matriz de 32 elementos.|
|**[exp]**|Uma expressão C++ válida que é avaliada como um inteiro.|pBuffer,[bufferSize]|Exibe pBuffer como uma matriz de `bufferSize` elementos.|
|**expand(n)**|Uma expressão C++ válida que é avaliada como um inteiro|pBuffer, expand(2)|Exibe o terceiro elemento de  `pBuffer`|

## <a name="format-specifiers-for-interop-debugging-with-ccli"></a><a name="BKMK_Format_specifiers_for_interop_debugging_and_C___edit_and_continue"></a> Especificadores de formato para depuração de interop com C++/CLI

Os especificadores em **negrito** têm suporte apenas para depuração de código nativo e C++/CLI. Isso requer o depurador herdado, especificado usando [o Modo de Compatibilidade Gerenciada](../debugger/general-debugging-options-dialog-box.md).

|Especificador|Formatar|Valor de Relógio Original|Valor exibido|
|---------------|------------|--------------------------|---------------------|
|**d**<br /><br />**i**|inteiro decimal assinado|0xF000F065|-268373915|
|**u**|inteiro decimal não assinado|0x0065|101|
|o|inteiro octal não assinado|0xF065|0170145|
|x<br /><br />X|Inteiro hexadecimal|61541|0x0000f065|
|**l**<br /><br />**h**|prefixo longo ou curto para: d, i, u, o, x, X|00406042|0x0c22|
|**f**|ponto flutuante assinado|(3./2.), f|1.500000|
|**Oriental**|notação científica assinada|(3.0/2.0)|1.500000e+000|
|**m**|ponto flutuante assinado ou notação científica assinada,<br/> o que for menor|(3.0/2.0)|1.5|
|c|caractere único|\<location>|101 'e'|
|s|const char * (com aspas)|\<location>|“Olá Mundo”|
|su|const wchar_t*<br /><br /> const char16_t \* (entre aspas)|\<location>|L"hello world"|
|sub|const wchar_t*<br /><br /> const char16_t\*|\<location>|hello world|
|s8|const char * (com aspas)|\<location>|“Olá Mundo”|
|h|Código de erro HRESULT ou Win32.<br/>Esse especificador não é mais necessário para HRESULTs, pois o depurador os decodifica automaticamente.|S_OK|S_OK|
|wc|Sinalizador de classe do Windows|0x00000040,|WC_DEFAULTCHAR|
|wm|Números de mensagens do Windows|0x0010|WM_CLOSE|
|!|formato bruto, ignorando quaisquer personalizações de exibição de tipo de dados|\<customized representation>|4|

### <a name="format-specifiers-for-memory-locations-in-interop-debugging-with-ccli"></a><a name="BKMK_Format_specifiers_memory_locations_in_interop_debugging_and_C___edit_and_continue"></a> Especificadores de formato para locais de memória na depuração de interoperabilidade com C++/CLI

A tabela a seguir descreve os símbolos de formatação usados para locais de memória. Você pode usar um especificador de local da memória com qualquer valor ou expressão que seja avaliada como um local.

Não há suporte para especificadores em **negrito** apenas para depuração de código nativo e C++/CLI. Isso requer o depurador herdado, especificado usando o [modo de compatibilidade gerenciado](../debugger/general-debugging-options-dialog-box.md).

|Símbolo|Formatar|Valor de inspeção original|Valor exibido|
|------------|------------|--------------------------|---------------------|
|**Massachusetts**|Caracteres ASCII na base 64|0x0012ffac|0x0012ffac .4...0...".0W&.......1W&.0.:W..1...."..1.JO&.1.2.."..1...0y....1|
|**m**|16 bytes em hexadecimal, seguidos caracteres ASCII na base 16|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|
|**MBS**|16 bytes em hexadecimal, seguidos caracteres ASCII na base 16|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|
|**MW**|8 palavras|0x0012ffac|0x0012ffac 34B3 00CB 3084 8094 22FF 308A 2657 0000|
|**md**|4 palavra duplas|0x0012ffac|0x0012ffac 00CB34B3 80943084 308A22FF 00002657|
|**MQ**|2 palavras quádruplas|0x0012ffac|0x0012ffac 7ffdf00000000000 5f441a790012fdd4|
|**Mu**|Caracteres de 2 bytes (Unicode)|0x0012ffac|0x0012ffac 8478 77f4 ffff ffff 0000 0000 0000 0000|

### <a name="size-specifier-for-pointers-as-arrays-in-interop-debugging-with-ccli"></a><a name="BKMK_Size_specifier_for_pointers_as_arrays_in_interop_debugging_and_C___edit_and_continue"></a> Especificador de tamanho para ponteiros como matrizes na depuração de interoperabilidade com C++/CLI

Se você tiver um ponteiro para um objeto que você deseja exibir como uma matriz, poderá usar um inteiro para especificar o número de elementos da matriz.

|Especificador|Formatar|Expression|Valor exibido|
|---------------|------------|----------------|---------------------|
|n|Inteiro decimal|pBuffer[32]|Exibe `pBuffer` como uma matriz de elemento 32.|
