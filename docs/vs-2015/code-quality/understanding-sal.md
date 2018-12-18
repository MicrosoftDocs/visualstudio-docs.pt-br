---
title: Noções básicas sobre o SAL | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a94d6907-55f2-4874-9571-51d52d6edcfd
caps.latest.revision: 20
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 712d99f3839982632e54b622b3512eb611f2bf95
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792808"
---
# <a name="understanding-sal"></a>Noções básicas de SAL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A linguagem de anotação de código-fonte do Microsoft (SAL) fornece um conjunto de anotações que você pode usar para descrever como uma função usa seus parâmetros, as suposições que faz sobre eles e as garantias de que ele faz quando ele for concluído. As anotações são definidas no arquivo de cabeçalho `<sal.h>`. Análise de código do Visual Studio para C++ usa anotações de SAL para modificar sua análise de funções. Para obter mais informações sobre o SAL 2.0 para o desenvolvimento de driver do Windows, consulte [SAL 2.0 anotações para o Windows Drivers](http://go.microsoft.com/fwlink/?LinkId=250979).  
  
 Modo nativo, C e C++ fornecem somente de maneiras limitadas para os desenvolvedores expressem consistentemente a intenção e invariância. Usando anotações de SAL, você pode descrever suas funções mais detalhadamente, para que os desenvolvedores que estão consumindo eles podem entender melhor como usá-los.  
  
## <a name="what-is-sal-and-why-should-you-use-it"></a>Qual é o SAL e por que você deve usá-lo?  
 Em poucas palavras, o SAL é uma maneira barata de deixar que o compilador verifique seu código para você.  
  
### <a name="sal-makes-code-more-valuable"></a>SAL torna o código mais valiosos  
 SAL pode ajudá-lo a tornar o design de código mais compreensível, tanto para os humanos para ferramentas de análise de código. Considere este exemplo que mostra a função de tempo de execução C `memcpy`:  
  
```cpp  
  
void * memcpy(  
   void *dest,   
   const void *src,   
   size_t count  
);  
  
```  
  
 Você pode dizer que essa função faz? Quando uma função é implementada ou chamada, certas propriedades devem ser mantidas para garantir a exatidão do programa. Apenas observando uma declaração, como o exemplo, você não sabe o que são. Sem anotações de SAL, você teria que se baseiam na documentação ou comentários de código. Aqui está a documentação do MSDN para `memcpy` diz:  
  
> "Contagem de cópias de bytes de origem para dest. Se a origem e destino se sobrepõem, o comportamento de memcpy é indefinido. Use memmove para lidar com regiões sobrepostas.   
> **Observação de segurança:** Certifique-se de que o buffer de destino é o mesmo tamanho ou maior que o buffer de origem. Para obter mais informações, consulte"evitando saturações de Buffer."  
  
 A documentação contém algumas partes de informações que sugerem que seu código deve manter determinadas propriedades para garantir a exatidão do programa:  
  
- `memcpy` Copia o `count` de bytes do buffer de origem para o buffer de destino.  
  
- O buffer de destino deve ser pelo menos tão grande quanto o buffer de origem.  
  
  No entanto, o compilador não pode ler a documentação ou comentários informais. Ele não sabe que há uma relação entre dois buffers e `count`, e ele também não pode efetivamente adivinhar sobre uma relação. SAL pode fornecer mais clareza sobre as propriedades e implementação da função, conforme mostrado aqui:  
  
```cpp  
  
void * memcpy(  
   _Out_writes_bytes_all_(count) void *dest,   
   _In_reads_bytes_(count) const void *src,   
   size_t count  
);  
```  
  
 Observe que essas anotações se parecer com as informações na documentação do MSDN, mas eles são mais concisos e eles seguem um padrão de semântico. Quando você lê este código, você pode rapidamente compreender as propriedades dessa função e como evitar problemas de segurança de saturação de buffer. Melhor ainda, os padrões de semânticos fornece SAL podem melhorar a eficiência e eficácia das ferramentas de análise de código automático na detecção antecipada de possíveis bugs. Imagine que alguém grava essa implementação com bugs de `wmemcpy`:  
  
```cpp  
  
wchar_t * wmemcpy(  
   _Out_writes_all_(count) wchar_t *dest,   
   _In_reads_(count) const wchar_t *src,   
   size_t count)  
{  
   size_t i;  
   for (i = 0; i <= count; i++) { // BUG: off-by-one error  
      dest[i] = src[i];  
   }  
   return dest;  
}  
  
```  
  
 Essa implementação contém um erro comum de off-by-one. Felizmente, o autor do código incluído a anotação de tamanho do buffer SAL — uma ferramenta de análise de código pode capturar o bug, analisando essa função sozinha.  
  
### <a name="sal-basics"></a>Noções básicas SAL  
 SAL define quatro tipos básicos de parâmetros, que são categorizados por padrão de uso.  
  
|Categoria|Anotação de parâmetro|Descrição|  
|--------------|--------------------------|-----------------|  
|**A entrada para a chamada de função**|`_In_`|Dados são passados para a função chamada e são tratados como somente leitura.|  
|**Entrada para chamada de função e de saída ao chamador**|`_Inout_`|Dados utilizáveis são passados para a função e possivelmente serão modificados.|  
|**Saída ao chamador**|`_Out_`|O chamador só fornece espaço para a função de chamada gravar. A função chamada grava dados nesse espaço.|  
|**Saída de ponteiro para o chamador**|`_Outptr_`|Como o **de saída ao chamador**. O valor retornado pela função chamada é um ponteiro.|  
  
 Essas quatro anotações básicas podem ser feitas mais explícitas de várias maneiras. Por padrão, parâmetros de ponteiro anotados são considerados necessários — eles devem ser não nulo para a função seja bem-sucedida. A variação mais comumente usada das anotações básicas indica que um parâmetro de ponteiro é opcional – se for NULL, a função ainda pode ter êxito ao fazer seu trabalho.  
  
 Esta tabela mostra como distinguir entre os parâmetros obrigatórios e opcionais:  
  
||Parâmetros são obrigatórios|Os parâmetros são opcionais|  
|-|-----------------------------|-----------------------------|  
|**A entrada para a chamada de função**|`_In_`|`_In_opt_`|  
|**Entrada para chamada de função e de saída ao chamador**|`_Inout_`|`_Inout_opt_`|  
|**Saída ao chamador**|`_Out_`|`_Out_opt_`|  
|**Saída de ponteiro para o chamador**|`_Outptr_`|`_Outptr_opt_`|  
  
 Essas anotações ajudar a identificar possíveis valores não inicializados e usa o ponteiro nulo inválido de uma maneira formal e precisa. Passagem de NULL para um parâmetro obrigatório pode causar uma falha, ou pode fazer com que um código de erro "Falha" a ser retornado. De qualquer forma, a função não conseguir obter êxito ao fazer seu trabalho.  
  
## <a name="sal-examples"></a>Exemplos SAL  
 Esta seção mostra exemplos de código para as anotações de SAL básicos.  
  
### <a name="using-the-visual-studio-code-analysis-tool-to-find-defects"></a>Usando a ferramenta de análise de código do Visual Studio para encontrar defeitos  
 Nos exemplos, a ferramenta de análise de código do Visual Studio é usada junto com anotações de SAL para encontrar defeitos de código. Aqui está como fazer isso.  
  
##### <a name="to-use-visual-studio-code-analysis-tools-and-sal"></a>Usar ferramentas de análise de código do Visual Studio e o SAL  
  
1. No Visual Studio, abra um projeto de C++ que contém as anotações de SAL.  
  
2. Na barra de menus, escolha **construir**, **executar análise de código na solução**.  
  
    Considere a \_em\_ exemplo nesta seção. Se você executar a análise de código nele, esse aviso é exibido:  
  
   > **C6387 o valor de parâmetro inválido**   
   > 'pInt' pode ser '0': isso não adere à especificação para a função 'InCallee'.  
  
### <a name="example-the-in-annotation"></a>Exemplo: O \_em\_ anotação  
 O `_In_` anotação indica que:  
  
-   O parâmetro deve ser válido e não será modificado.  
  
-   A função lerá apenas do buffer de elemento único.  
  
-   O chamador deve fornecer ao buffer e inicializá-lo.  
  
-   `_In_` Especifica a "somente leitura". Um erro comum é aplicar `_In_` para um parâmetro que deve ter o `_Inout_` anotação em vez disso.  
  
-   `_In_` é permitido, mas são ignorados pelo analisador de em não ponteiro escalares.  
  
```cpp  
void InCallee(_In_ int *pInt)  
{  
   int i = *pInt;  
}  
  
void GoodInCaller()  
{  
   int *pInt = new int;  
   *pInt = 5;  
  
   InCallee(pInt);  
   delete pInt;     
}  
  
void BadInCaller()  
{  
   int *pInt = NULL;  
   InCallee(pInt); // pInt should not be NULL  
}  
  
```  
  
 Se você usar a análise de código do Visual Studio neste exemplo, ele valida que os chamadores passam um ponteiro não nulo para um buffer inicializado para `pInt`. Nesse caso, `pInt` ponteiro não pode ser NULL.  
  
### <a name="example-the-inopt-annotation"></a>Exemplo: O \_In_opt\_ anotação  
 `_In_opt_` é o mesmo que `_In_`, exceto que o parâmetro de entrada tem permissão para ser NULL e, portanto, a função deve verificar isso.  
  
```cpp  
  
void GoodInOptCallee(_In_opt_ int *pInt)  
{  
   if(pInt != NULL) {  
      int i = *pInt;  
   }  
}  
  
void BadInOptCallee(_In_opt_ int *pInt)  
{  
   int i = *pInt; // Dereferencing NULL pointer ‘pInt’  
}  
  
void InOptCaller()  
{  
   int *pInt = NULL;  
   GoodInOptCallee(pInt);  
   BadInOptCallee(pInt);  
}  
  
```  
  
 Análise de código do Visual Studio valida que a função verifica para nulo antes de acessar o buffer.  
  
### <a name="example-the-out-annotation"></a>Exemplo: O \_Out\_ anotação  
 `_Out_` dá suporte a um cenário comum em que é passado um ponteiro não nulo que aponta para um buffer de elemento e a função inicializa o elemento. O chamador não tem que inicializar o buffer antes da chamada; a função chamada promete inicializá-lo antes de retornar.  
  
```cpp  
  
void GoodOutCallee(_Out_ int *pInt)  
{  
   *pInt = 5;  
}  
  
void BadOutCallee(_Out_ int *pInt)  
{  
   // Did not initialize pInt buffer before returning!  
}  
  
void OutCaller()  
{  
   int *pInt = new int;  
   GoodOutCallee(pInt);  
   BadOutCallee(pInt);  
   delete pInt;  
}  
  
```  
  
 Ferramenta de análise de código do Visual Studio valida que o chamador passa um ponteiro não nulo para um buffer para `pInt` e que o buffer é inicializado pela função antes de retornar.  
  
### <a name="example-the-outopt-annotation"></a>Exemplo: O \_Out_opt\_ anotação  
 `_Out_opt_` é o mesmo que `_Out_`, exceto que o parâmetro pode ser NULL e, portanto, a função deve verificar isso.  
  
```cpp  
  
void GoodOutOptCallee(_Out_opt_ int *pInt)  
{  
   if (pInt != NULL) {  
      *pInt = 5;  
   }  
}  
  
void BadOutOptCallee(_Out_opt_ int *pInt)  
{  
   *pInt = 5; // Dereferencing NULL pointer ‘pInt’  
}  
  
void OutOptCaller()  
{  
   int *pInt = NULL;  
   GoodOutOptCallee(pInt);  
   BadOutOptCallee(pInt);  
}  
  
```  
  
 Análise de código do Visual Studio valida que essa função verifica para nulo antes de `pInt` sua referência é cancelada e se `pInt` não for nulo, o que o buffer é inicializado pela função antes de retornar.  
  
### <a name="example-the-inout-annotation"></a>Exemplo: O \_Inout\_ anotação  
 `_Inout_` é usado para anotar um parâmetro de ponteiro que poderá ser alterado pela função. O ponteiro deve apontar para dados inicializados válidos antes da chamada e, mesmo se ele for alterado, ele ainda deve ter um valor válido no retorno. A anotação Especifica que a função pode ler e gravar no buffer de um elemento livremente. O chamador deve fornecer ao buffer e inicializá-lo.  
  
> [!NOTE]
>  Como o `_Out_`, `_Inout_` devem se aplicar a um valor modificável.  
  
```cpp  
  
void InOutCallee(_Inout_ int *pInt)  
{  
   int i = *pInt;  
   *pInt = 6;  
}  
  
void InOutCaller()  
{  
   int *pInt = new int;  
   *pInt = 5;  
   InOutCallee(pInt);  
   delete pInt;  
}  
  
void BadInOutCaller()  
{  
   int *pInt = NULL;  
   InOutCallee(pInt); // ‘pInt’ should not be NULL  
}  
  
```  
  
 Análise de código do Visual Studio valida que os chamadores passam um ponteiro não nulo para um buffer inicializado para `pInt`e que, antes de retorno, `pInt` ainda não for nulo e o buffer é inicializado.  
  
### <a name="example-the-inoutopt-annotation"></a>Exemplo: O \_Inout_opt\_ anotação  
 `_Inout_opt_` é o mesmo que `_Inout_`, exceto que o parâmetro de entrada tem permissão para ser NULL e, portanto, a função deve verificar isso.  
  
```cpp  
  
void GoodInOutOptCallee(_Inout_opt_ int *pInt)  
{  
   if(pInt != NULL) {  
      int i = *pInt;  
      *pInt = 6;  
   }  
}  
  
void BadInOutOptCallee(_Inout_opt_ int *pInt)  
{  
   int i = *pInt; // Dereferencing NULL pointer ‘pInt’  
   *pInt = 6;  
}  
  
void InOutOptCaller()  
{  
   int *pInt = NULL;  
   GoodInOutOptCallee(pInt);  
   BadInOutOptCallee(pInt);  
}  
  
```  
  
 Análise de código do Visual Studio valida a essa função verifica para nulo antes de acessar o buffer e se `pInt` não for nulo, o que o buffer é inicializado pela função antes de retornar.  
  
### <a name="example-the-outptr-annotation"></a>Exemplo: O \_Outptr\_ anotação  
 `_Outptr_` é usado para anotar um parâmetro que tem como objetivo retornar um ponteiro.  O parâmetro em si não deve ser NULL e a função chamada retorna um ponteiro não nulo nele e esse ponteiro aponta para dados inicializados.  
  
```cpp  
  
void GoodOutPtrCallee(_Outptr_ int **pInt)  
{  
   int *pInt2 = new int;  
   *pInt2 = 5;  
  
   *pInt = pInt2;  
}  
  
void BadOutPtrCallee(_Outptr_ int **pInt)  
{  
   int *pInt2 = new int;  
   // Did not initialize pInt buffer before returning!  
   *pInt = pInt2;  
}  
  
void OutPtrCaller()  
{  
   int *pInt = NULL;  
   GoodOutPtrCallee(&pInt);  
   BadOutPtrCallee(&pInt);  
}  
  
```  
  
 Análise de código do Visual Studio valida que o chamador passa um ponteiro não nulo `*pInt`, e que o buffer é inicializado pela função antes de retornar.  
  
### <a name="example-the-outptropt-annotation"></a>Exemplo: O \_Outptr_opt\_ anotação  
 `_Outptr_opt_` é o mesmo que `_Outptr_`, exceto que o parâmetro é opcional, o chamador pode passar um ponteiro NULL para o parâmetro.  
  
```cpp  
  
void GoodOutPtrOptCallee(_Outptr_opt_ int **pInt)  
{  
   int *pInt2 = new int;  
   *pInt2 = 6;  
  
   if(pInt != NULL) {  
      *pInt = pInt2;  
   }  
}  
  
void BadOutPtrOptCallee(_Outptr_opt_ int **pInt)  
{  
   int *pInt2 = new int;  
   *pInt2 = 6;  
   *pInt = pInt2; // Dereferencing NULL pointer ‘pInt’  
}  
  
void OutPtrOptCaller()  
{  
   int **ppInt = NULL;  
   GoodOutPtrOptCallee(ppInt);  
   BadOutPtrOptCallee(ppInt);  
}  
  
```  
  
 Análise de código do Visual Studio valida que essa função verifica para nulo antes de `*pInt` sua referência é cancelada, e que o buffer é inicializado pela função antes de retornar.  
  
### <a name="example-the-success-annotation-in-combination-with-out"></a>Exemplo: O \_sucesso\_ anotação em combinação com \_Out\_  
 As anotações podem ser aplicadas à maioria dos objetos.  Em particular, é possível anotar uma função inteira.  Uma das características de uma função mais óbvias é que ele pode ter êxito ou falhar. Mas, como a associação entre um buffer e seu tamanho, C/C++ não pode expressar função êxito ou falha. Usando o `_Success_` anotação, você pode dizer o que é sucesso para uma função.  O parâmetro para o `_Success_` anotação é apenas uma expressão que quando ele é true indica que a função foi bem-sucedida. A expressão pode ser qualquer coisa que o analisador de anotação pode manipular. Os efeitos das anotações depois que a função retorna só são aplicáveis quando a função for bem-sucedida. Este exemplo mostra como `_Success_` interage com `_Out_` para fazer a coisa certa. Você pode usar a palavra-chave `return` para representar o valor de retorno.  
  
```cpp  
  
_Success_(return != false) // Can also be stated as _Success_(return)  
bool GetValue(_Out_ int *pInt, bool flag)  
{  
   if(flag) {  
      *pInt = 5;  
      return true;  
   } else {  
      return false;  
   }  
}  
  
```  
  
 O `_Out_` anotação faz análise de código do Visual Studio para validar que o chamador passa um ponteiro não nulo para um buffer para `pInt`, e que o buffer é inicializado pela função antes de retornar.  
  
## <a name="sal-best-practice"></a>Prática recomendada de SAL  
  
### <a name="adding-annotations-to-existing-code"></a>Adicionando anotações para o código existente  
 SAL é uma tecnologia poderosa que pode ajudá-lo a melhorar a segurança e confiabilidade do seu código. Depois que você saiba o SAL, você pode aplicar a nova habilidade para seu trabalho diário. No novo código, você pode usar as especificações de SAL por design em todo; no código anterior, você pode adicionar anotações de forma incremental e, portanto, aumentar os benefícios, sempre que você atualizar.  
  
 Cabeçalhos públicos da Microsoft já são anotados. Portanto, sugerimos que seus projetos você primeiro anota funções do nó de folha e funções que chamam as APIs do Win32 para tirar o máximo proveito.  
  
### <a name="when-do-i-annotate"></a>Ao anotar?  
 Aqui estão algumas diretrizes:  
  
- Anote todos os parâmetros de ponteiro.  
  
- Anote as anotações de intervalo de valores para que a análise de código pode garantir a segurança do buffer e ponteiro.  
  
- Anote as regras de bloqueio e travamento efeito colateral. Para obter mais informações, consulte [anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md).  
  
- Anote propriedades do driver e outras propriedades específicas de domínio.  
  
  Ou você pode anotar todos os parâmetros para tornar sua intenção clear em todo e tornar mais fácil de verificar que as anotações foram feitas.  
  
## <a name="related-resources"></a>Recursos relacionados  
 [Blog da equipe de análise de código](http://go.microsoft.com/fwlink/p/?LinkId=251197)  
  
## <a name="see-also"></a>Consulte também  
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [Anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md)   
 [Anotando o comportamento da função](../code-quality/annotating-function-behavior.md)   
 [Anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md)   
 [Anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md)   
 [Especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [Práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)



