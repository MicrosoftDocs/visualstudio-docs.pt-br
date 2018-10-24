---
title: Expressões no depurador | Microsoft Docs
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
- vs.debug.expressions
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VBScript
helpviewer_keywords:
- expressions [debugger]
- debugging [Visual Studio], expressions
- expression evaluation, debugger evaluator
- native expression evaluation
- expression evaluators
- debugger, evaluating expressions
- debugging [Visual Studio], expression evaluation
- debugging [Visual Studio], variable evaluation
ms.assetid: 70f9b531-44c7-4d77-980d-5eddbf2bff41
caps.latest.revision: 30
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3254ea0197ee0b241735df9c1f437490a09da969
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49914303"
---
# <a name="expressions-in-the-debugger"></a>Expressões no depurador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O depurador do Visual Studio inclui avaliadores de expressão que funcionam quando você insere uma expressão na **QuickWatch** caixa de diálogo **inspeção** janela, ou **imediato** janela. Os avaliadores de expressão também estão em funcionamento na **pontos de interrupção** janela e muitos outros locais no depurador.  
  
 As seções a seguir fornecem detalhes sobre as expressões em idiomas diferentes.  
  
## <a name="f-expressions-are-not-supported"></a>Não há suporte para expressões de F #  
 Expressões de F # não são reconhecidas. Se você estiver depurando código F #, você precisa converter as expressões na sintaxe c# antes de inserir expressões em uma caixa de diálogo ou janela do depurador. Quando você converter expressões de F # para c#, não se esqueça de que c# usa a `==` operador para testar a igualdade, enquanto o F # usa o único `=`.  
  
## <a name="c-expressions"></a>Expressões C++  
 Para obter informações sobre como usar operadores de contexto com expressões em C++, consulte [operador de contexto (C++)](../debugger/context-operator-cpp.md).  
  
### <a name="unsupported-expressions-in-c"></a>Não há suporte para expressões em C++  
  
#### <a name="constructors-destructors-and-conversions"></a>Construtores, destruidores e conversões  
 Você não pode chamar um construtor ou destruidor para um objeto, explicitamente ou implicitamente. Por exemplo, a expressão a seguir chama explicitamente um construtor e resulta em uma mensagem de erro:  
  
```cpp  
my_date( 2, 3, 1985 )  
```  
  
 Você não pode chamar uma função de conversão se o destino da conversão for uma classe. Essa conversão envolve a construção de um objeto. Por exemplo, se `myFraction` for uma instância de `CFraction`, que define o operador da função de conversão `FixedPoint`, a expressão a seguir resultará em erro:  
  
```cpp  
(FixedPoint)myFraction  
```  
  
 Você não pode chamar o novo ou excluir operadores. Por exemplo, não há suporte para a expressão a seguir:  
  
```cpp  
new Date(2,3,1985)  
```  
  
#### <a name="preprocessor-macros"></a>Macros de pré-processador  
 Não há suporte para macros de pré-processador no depurador. Por exemplo, se uma constante `VALUE` é declarado como: `#define VALUE 3`, você não pode usar `VALUE` no **inspeção** janela. Para evitar essa limitação, você deve substituir `#define`com enums e funções sempre que possível.  
  
### <a name="using-namespace-declarations"></a>usando declarações de namespace  
 Não é possível usar `using namespace` declarações.  Para acessar um nome de tipo ou variável fora do namespace atual, você deve usar o nome totalmente qualificado.  
  
### <a name="anonymous-namespaces"></a>Namespaces anônimos  
 Não há suporte para namespaces anônimos. Se você tiver o código a seguir, você não pode adicionar `test` à janela Inspeção:  
  
```cpp  
namespace mars   
{   
    namespace  
    {  
        int test = 0;   
    }   
}   
int main()   
{   
    // Adding a watch on test does not work.   
    mars::test++;   
    return 0;   
}  
  
```  
  
###  <a name="BKMK_Using_debugger_intrinisic_functions_to_maintain_state"></a> Usando funções intrínsecas do depurador para manter o estado  
 As funções intrínsecas do depurador oferecem uma maneira de chamar determinadas funções C/C++ em expressões sem alterar o estado do aplicativo.  
  
 Funções intrínsecas do depurador:  
  
- São certamente seguras: executar uma função intrínseca do depurador não corromperá o processo que está sendo depurado.  
  
- São permitidas em todas as expressões, mesmo em cenários onde os efeitos colaterais e a avaliação de função não são permitidos.  
  
- Trabalham em cenários onde as chamadas de funções normais não são possíveis, por exemplo, depurar um minidespejo.  
  
  As funções intrínsecas do depurador também podem tornar mais convenientes as expressões de avaliação. Por exemplo, `strncmp(str, “asd”)` é muito mais fácil escrever em uma condição de ponto de interrupção que `str[0] == ‘a’ && str[1] == ‘s’ && str[2] == ‘d’`. )  
  
|Área|Funções intrínsecas|  
|----------|-------------------------|  
|**Comprimento da cadeia de caracteres**|strlen, wcslen, strnlen, wcsnlen|  
|**Comparação de cadeia de caracteres**|strcmp, wcscmp, stricmp, _stricmp, _strcmpi, wcsicmp, _wcscmpi, _wcsnicmp, strncmp, wcsncmp, strnicmp, wcsnicmp|  
|**Pesquisa de cadeia de caracteres**|strchr, wcschr, strstr, wcsstr|  
|**Win32**|GetLastError(), TlsGetValue()|  
|**Windows 8**|WindowsGetStringLen(), WindowsGetStringRawBuffer()<br /><br /> Essas funções exigem que o processo que está sendo depurado seja executado no Windows 8. Depurar os arquivos de despejo gerados a partir de um dispositivo do Windows 8 também exige que o computador do Visual Studio esteja executando o Windows 8. No entanto, se você estiver depurando um dispositivo do Windows 8 remotamente, o computador do Visual Studio poderá executar o Windows 7.|  
|**Diversos**|__log2<br /><br /> Retorna a base 2 de log de um inteiro especificado, arredondada para o menor inteiro próximo.|  
  
## <a name="ccli---unsupported-expressions"></a>C + + c++ CLI - expressões sem suporte  
  
-   Conversões que envolvem ponteiros ou conversões definidas pelo usuário, não têm suporte.  
  
-   Não há suporte para a atribuição e comparação de objeto.  
  
-   Não há suporte para operadores sobrecarregados e funções sobrecarregadas.  
  
-   Não há suporte para conversões boxing e unboxing.  
  
-   `Sizeof` Não há suporte para o operador.  
  
## <a name="c---unsupported-expressions"></a>C# - expressões sem suporte  
  
### <a name="dynamic-objects"></a>Objetos dinâmicos  
 Você pode usar variáveis em expressões de depurador que são estaticamente tipadas como dinâmicas. Quando os objetos que implementam o <xref:System.Dynamic.IDynamicMetaObjectProvider> são avaliados na janela de inspeção, uma exibição dinâmica de nó é adicionado. O nó do Modo de Exibição Dinâmico exibe membros do objeto, mas não permite editar os valores dos membros.  
  
 Os seguintes recursos de objetos dinâmicos não têm suporte:  
  
-   Os operadores compostos `+=`, `-=`, `%=`, `/=`, e `*=`  
  
-   Várias conversões, inclusive conversões numéricas e conversões de tipo de argumento  
  
-   Chamadas de método com mais de dois argumentos  
  
-   Getters da propriedade com mais de dois argumentos  
  
-   Setters de propriedade com argumentos  
  
-   Atribuição a um indexador  
  
-   Operadores boolianos `&&` e `||`  
  
### <a name="anonymous-methods"></a>Métodos anônimos  
 Não há suporte para a criação de novos métodos anônimos.  
  
## <a name="visual-basic---unsupported-expressions"></a>Visual Basic – expressões sem suporte  
  
### <a name="dynamic-objects"></a>Objetos dinâmicos  
 Você pode usar variáveis em expressões de depurador que são estaticamente tipadas como dinâmicas. Quando os objetos que implementam o <xref:System.Dynamic.IDynamicMetaObjectProvider> são avaliados na janela de inspeção, uma exibição dinâmica de nó é adicionado. O nó do Modo de Exibição Dinâmico exibe membros do objeto, mas não permite editar os valores dos membros.  
  
 Os seguintes recursos de objetos dinâmicos não têm suporte:  
  
-   Os operadores compostos `+=`, `-=`, `%=`, `/=`, e `*=`  
  
-   Várias conversões, inclusive conversões numéricas e conversões de tipo de argumento  
  
-   Chamadas de método com mais de dois argumentos  
  
-   Getters da propriedade com mais de dois argumentos  
  
-   Setters de propriedade com argumentos  
  
-   Atribuição a um indexador  
  
-   Operadores boolianos `&&` e `||`  
  
### <a name="local-constants"></a>Constantes locais  
 As constantes locais não têm suporte.  
  
### <a name="import-aliases"></a>Aliases de importação  
 Não há suporte para aliases de importação.  
  
### <a name="variable-declarations"></a>Declarações de variável  
 Você não pode declarar novas variáveis explícitas nas janelas do depurador. No entanto, você pode atribuir novas variáveis implícitas dentro de **imediato** janela. Essas variáveis implícitas têm escopo para a sessão de depuração e não estão acessíveis fora do depurador. Por exemplo, a instrução `o = 5` implicitamente cria uma nova variável `o` e atribua o valor 5 a ele. Essas variáveis implícitas são do tipo **objeto** , a menos que o tipo pode ser inferido pelo depurador.  
  
### <a name="unsupported-keywords"></a>Palavras-chave sem suporte  
  
-   `AddressOf`  
  
-   `End`  
  
-   `Error`  
  
-   `Exit`  
  
-   `Goto`  
  
-   `On Error`  
  
-   `Resume`  
  
-   `Return`  
  
-   `Select/Case`  
  
-   `Stop`  
  
-   `SyncLock`  
  
-   `Throw`  
  
-   `Try/Catch/Finally`  
  
-   `With`  
  
-   Namespace ou módulo nível palavras-chave, como `End Sub` ou `Module`.  
  
## <a name="see-also"></a>Consulte também  
 [Especificadores de formato em C++](../debugger/format-specifiers-in-cpp.md)   
 [Operador de contexto (C++)](../debugger/context-operator-cpp.md)   
 [Especificadores de formato em c#](../debugger/format-specifiers-in-csharp.md)   
 [Pseudovariáveis](../debugger/pseudovariables.md)





