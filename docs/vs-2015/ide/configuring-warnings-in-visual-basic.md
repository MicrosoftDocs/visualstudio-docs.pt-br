---
title: Configurando avisos no Visual Basic | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- errors [Visual Basic], warnings
- run-time errors, warnings
- warnings, configuring
ms.assetid: 99cf4781-bd4d-47b4-91b9-217933509f82
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: c3b28bea858c867bd7fae8e1b4045d79d5e4b513
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49297603"
---
# <a name="configuring-warnings-in-visual-basic"></a>Configurando avisos no Visual Basic
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O compilador [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] inclui um conjunto de avisos sobre o código que podem causar erros em tempo de execução. É possível usar essas informações para escrever códigos mais limpos, mais rápidos e melhores com menos bugs. Por exemplo, o compilador produzirá um aviso quando o usuário tentar invocar um membro de uma variável de objeto não atribuída, retornar de uma função sem definir o valor retornado ou executar um bloco `Try` com erros na lógica para capturar exceções.  
  
 Às vezes, o compilador fornece lógica extra em nome do usuário para que o usuário possa se concentrar na tarefa em questão, em vez de antecipar possíveis erros. Nas versões anteriores do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], o `Option Strict` era usado para limitar a lógica adicional fornecida pelo compilador [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]. A configuração de avisos permite limitar essa lógica de uma maneira mais granular, no nível dos avisos individuais.  
  
 Talvez você deseje personalizar seu projeto e desligar alguns avisos não relevantes ao aplicativo enquanto transforma outros avisos em erros. Esta página explica como ativar e desativar avisos individuais.  
  
## <a name="turning-warnings-off-and-on"></a>Ativando e desativando avisos  
 Há duas maneiras diferentes para configurar avisos: é possível configurá-los usando o **Designer de Projeto** ou usar as opções **/warnaserror** e **/nowarn** do compilador.  
  
 A guia **Compilar** da página **Designer de Projeto** permite ativar e desativar avisos. Marque a caixa de seleção **Desabilitar Todos os Avisos** para desabilitar todos os avisos; marque **Tratar Todos os Avisos como Erros** para tratar todos os avisos como erros. Alguns avisos individuais podem ser ativados/desativados como erro ou aviso, conforme desejado, na tabela exibida.  
  
 Quando **Opção Estrita** é definida como **Desativado**, os avisos relacionados à **Opção Estrita** não podem ser tratados independentemente uns dos outros. Quando **Opção Estrita** é definida como **Ativado**, os avisos associados são tratados como erros, independentemente de seu status. Quando **Opção Estrita** é definida como **Personalizado** especificando `/optionstrict:custom` no compilador de linha de comando, os avisos da **Opção Estrita** podem ser ativados ou desativados de forma independente.  
  
 A opção de linha de comando **/warnaserror** do compilador também pode ser usada para especificar se os avisos são tratados como erros. É possível adicionar uma lista delimitada por vírgula a essa opção para especificar quais avisos devem ser tratados como erros ou avisos, usando + ou -. A tabela a seguir fornece detalhes das possíveis opções.  
  
|Opção de linha de comando|Especifica|  
|--------------------------|---------------|  
|`/warnaserror+`|Tratar todos os avisos como erros|  
|`/warnsaserror`-|Não trate avisos como erros. Esse é o padrão.|  
|`/warnaserror+:<warning list` `>`|Trate avisos específicos como erros, listados por seus números de ID de erro em uma lista delimitada por vírgula.|  
|`/warnaserror-:<warning list>`|Não trate avisos específicos como erros, listados por seus números de ID de erro em uma lista delimitada por vírgula.|  
|`/nowarn`|Não relate os avisos.|  
|`/nowarn:<warning list>`|Não relate os avisos especificados, listados por seus números de ID de erro em uma lista delimitada por vírgula.|  
  
 A lista de avisos contém os números de ID de erro dos avisos que devem ser tratados como erros, que podem ser usados com as opções de linha de comando para ativar ou desativar avisos específicos. Se a lista de avisos contiver um número inválido, um erro será relatado.  
  
## <a name="examples"></a>Exemplos  
 Esta tabela de exemplos de argumentos de linha de comando descreve a ação de cada argumento.  
  
|Argumento|Descrição|  
|--------------|-----------------|  
|`vbc /warnaserror`|Especifica que todos os avisos devem ser tratado como erros.|  
|`vbc /warnaserror:42024`|Especifica que o aviso 42024 deve ser tratado como um erro.|  
|`vbc /warnaserror:42024,42025`|Especifica que os avisos 42024 e 42025 devem ser tratados como erros.|  
|`vbc /nowarn`|Especifica que nenhum aviso deve ser relatado.|  
|`vbc /nowarn:42024`|Especifica que o aviso 42024 não deve ser relatado.|  
|`vbc /nowarn:42024,42025`|Especifica que os avisos 42024 e 42025 não devem ser relatados.|  
  
## <a name="types-of-warnings"></a>Tipos de avisos  
 Veja a seguir uma lista de avisos que você pode desejar tratar como erros.  
  
### <a name="implicit-conversion-warning"></a>Aviso de conversão implícita  
 Gerado para instâncias de conversão implícita. Eles não incluem conversões implícitas de um tipo numérico intrínseco em uma cadeia de caracteres durante o uso do operador `&`. O padrão para novos projetos é desativado.  
  
 ID: 42016  
  
### <a name="late-bound-method-invocation-and-overload-resolution-warning"></a>Aviso de invocação de método e resolução de sobrecarga com associação tardia  
 Gerado para instâncias de associação tardia. O padrão para novos projetos é desativado.  
  
 ID: 42017  
  
### <a name="operands-of-type-object-warnings"></a>Avisos de operandos de objeto de tipo  
 Gerados quando ocorrem operandos do tipo `Object` que criarão um erro com `Option Strict On`. O padrão para novos projetos é ativado.  
  
 ID: 42018 e 42019  
  
### <a name="declarations-require-as-clause-warnings"></a>Avisos de declarações que exigem a cláusula “As”  
 Gerados quando uma declaração da variável, função ou propriedade que não tem uma cláusula `As` cria um erro com `Option Strict On`. Variáveis que não têm um tipo atribuído a elas são consideradas como sendo do tipo `Object`. O padrão para novos projetos é ativado.  
  
 ID: 42020 (declaração da variável), 42021 (declaração da função) e 42022 (declaração da propriedade).  
  
### <a name="possible-null-reference-exception-warnings"></a>Avisos de possível exceção de referência nula  
 Gerados quando uma variável é usada antes de receber um valor. O padrão para novos projetos é ativado.  
  
 ID: 42104, 42030  
  
### <a name="unused-local-variable-warning"></a>Aviso de variável local não utilizada  
 Gerado quando uma variável local é declarada, mas nunca referenciada. O padrão é ativado.  
  
 ID: 42024  
  
### <a name="access-of-shared-member-through-instance-variable-warning"></a>Aviso de acesso de membro compartilhado por meio de variável de instância  
 Gerado quando o acesso a um membro compartilhado por meio de uma instância pode ter efeitos colaterais, ou quando o acesso a um membro compartilhado por meio de uma variável de instância não está do lado direito de uma expressão ou está sendo passado como um parâmetro. O padrão para novos projetos é ativado.  
  
 ID: 42025  
  
### <a name="recursive-operator-or-property-access-warnings"></a>Avisos de operador recursivo ou acesso de propriedade  
 Gerados quando o corpo de uma rotina usa o mesmo operador ou a mesma propriedade em que é definido. O padrão para novos projetos é ativado.  
  
 ID: 42004 (operador), 42026 (propriedade)  
  
### <a name="function-or-operator-without-return-value-warning"></a>Aviso de função ou operador sem o valor retornado  
 Gerado quando a função ou o operador não tem um valor retornado especificado. Isso inclui a omissão de um `Set` na variável local implícita com o mesmo nome da função. O padrão para novos projetos é ativado.  
  
 ID: 42105 (função), 42016 (operador)  
  
### <a name="overloads-modifier-used-in-a-module-warning"></a>Aviso de modificador de sobrecargas usado em um módulo  
 Gerado quando `Overloads` é usado em um `Module`. O padrão para novos projetos é ativado.  
  
 ID: 42028  
  
### <a name="duplicate-or-overlapping-catch-blocks-warnings"></a>Avisos de blocos de captura duplicados ou sobrepostos  
 Gerado quando um bloco `Catch` nunca é acessado devido à definição de sua relação com outros blocos `Catch`. O padrão para novos projetos é ativado.  
  
 ID: 42029, 42031  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Assistente de exceção](../debugger/exception-assistant-dialog-box.md)   
 [Tipos de Erro](http://msdn.microsoft.com/library/3048aabf-8c97-4e13-9150-853769cb5f6f)   
 [Instrução Try...Catch...Finally](http://msdn.microsoft.com/library/d6488026-ccb3-42b8-a810-0d97b9d6472b)   
 [/nowarn](http://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83)   
 [/warnaserror (Visual Basic)](http://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1)   
 [Página de Compilação, Designer de Projeto (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md)   
 [Avisos do compilador desativados por padrão](http://msdn.microsoft.com/library/69809cfb-a38a-4035-b154-283a61938df8)





