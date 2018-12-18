---
title: Editar e continuar (Visual C++) | Microsoft Docs
ms.custom: ''
ms.date: 05/31/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C++]
- debugging [C++], Edit and Continue
- C/C++, Edit and Continue
ms.assetid: 1815251e-a877-433e-9e5e-69bd9ba254c7
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 7e468f75abbadbe46ea973a5c04d2e286fcfaca5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49867696"
---
# <a name="edit-and-continue-visual-c"></a>Editar e continuar (Visual C++)
Você pode usar Editar e continuar em projetos do Visual C++. Ver [alterações de código com suporte (C++)](../debugger/supported-code-changes-cpp.md) para obter informações sobre as limitações de editar e continuar.
  
Para obter mais informações sobre as melhorias do Visual Studio 2015 atualização 3, consulte [C++ Edit e Continue no Visual Studio 2015 atualização 3](https://blogs.msdn.microsoft.com/vcblog/2016/07/01/c-edit-and-continue-in-visual-studio-2015-update-3/).  
  
 O [/Zo (aprimorar otimizado de depuração)](/cpp/build/reference/zo-enhance-optimized-debugging) opção de compilador que foi introduzida no Visual Studio 2013 atualização 3 adiciona informações adicionais para arquivos. PDB (símbolo) para binários compilados sem a [/Od (desabilitar (Depurar)) ](https://msdn.microsoft.com/library/aafb762y.aspx) opção.  
  
 **/Zo** desabilita editar e continuar. Ver [como: depurar o código otimizado](../debugger/how-to-debug-optimized-code.md).  
  
##  <a name="BKMK_Enable_or_disable_automatic_invocation_of_Edit_and_Continue"></a> Habilitar ou desabilitar editar e continuar  
 Talvez você queira desabilitar a invocação automática de editar e continuar, se você estiver fazendo edições ao código que você deseja não aplicado durante a sessão de depuração atual. Você também pode habilitar novamente automática editar e continuar.

> [!IMPORTANT]
> Para configurações de compilação necessários e outras informações sobre compatibilidade de recursos, consulte [C++ Edit e Continue no Visual Studio 2015 atualização 3] (https://blogs.msdn.microsoft.com/vcblog/2016/07/01/c-edit-and-continue-in-visual-studio-2015-update-3/.
  
1. Se você estiver em uma sessão de depuração, pare a depuração (**Shift + F5**).

2. No menu **Ferramentas**, escolha **Opções**.
  
3. No **opções** caixa de diálogo, selecione **depuração > geral**.

4. Para habilitar, selecione **habilitar editar e continuar**. Para desabilitar, desmarque a caixa de seleção.
  
5. No **editar e continuar** grupo, marque ou desmarque as **habilitar nativo editar e continuar** caixa de seleção.  
  
   Alterar essa configuração afeta todos os projetos que você trabalha em. Você não precisa recriar seu aplicativo após alterar essa configuração. Se você criar seu aplicativo de linha de comando ou de um makefile, mas depurar no ambiente do Visual Studio, você ainda pode usar Editar e continuar se você definir a **/ZI** opção.  
  
##  <a name="BKMK_How_to_apply_code_changes_explicitly"></a> Como aplicar as alterações de código explicitamente  
 No Visual C++, editar e continuar podem aplicar alterações de código de duas maneiras. Alterações de código podem ser aplicadas implicitamente, quando você escolhe um comando de execução, ou explicitamente, usando o **aplicar alterações de código** comando.  
  
 Quando você aplica as alterações de código explicitamente, o programa permanece no modo de interrupção – nenhuma execução ocorre.  
  
-   Para aplicar alterações de código explicitamente, sobre o **depurar** menu, escolha **aplicar alterações de código**.  
  
##  <a name="BKMK_How_to_stop_code_changes"></a> Como parar as alterações de código  
 Quando Editar e Continuar estiver no processo de aplicar alterações de código, você poderá interromper a operação.  
  
 Para parar de aplicar alterações de código:  
  
- Sobre o **Debug** menu, escolha **parar de aplicar alterações de código**.  
  
  Este item de menu está visível apenas quando as alterações de código estão sendo aplicadas.  
  
  Se você escolher esta opção, nenhuma das alterações de código serão confirmadas.  
  
##  <a name="BKMK_How_to_reset_the_point_of_execution"></a> Como redefinir o ponto de execução  
 Algumas alterações de código podem fazer o ponto de execução ser movido para um novo local quando Editar e Continuar aplicar as alterações. Editar e Continuar coloca o ponto de execução o mais exatamente possível, mas os resultados podem não estar corretos em todos os casos.  
  
 No Visual C++, uma caixa de diálogo informa quando o ponto de execução é alterado. Você deve verificar se o local está correto antes de continuar a depuração. Se não estiver correto, use o **definir próxima instrução** comando. Para obter mais informações, consulte [definir a próxima instrução para executar](https://msdn.microsoft.com/library/y740d9d3.aspx#BKMK_Set_the_next_statement_to_execute).  
  
##  <a name="BKMK_How_to_work_with_stale_code"></a> Como trabalhar com código obsoleto  
 Em alguns casos, Editar e Continuar não pode aplicar imediatamente alterações de código ao executável, mas talvez consiga aplicá-las posteriormente se você continuar a depuração. Isso ocorre se você editar uma função que chama a função atual ou se adicionar mais de 64 bytes de novas variáveis a uma função na pilha de chamadas  
  
 Nesses casos, o depurador continua executando o código original até que as alterações podem ser aplicadas. O código obsoleto aparece como uma janela temporária do arquivo de origem em uma janela separada de origem, com um título como, por exemplo, `enc25.tmp`. A origem editada continuará aparecendo na janela do original. Se você tentar editar o código obsoleto, será exibida uma mensagem de aviso.  
  
## <a name="see-also"></a>Consulte também  
 [Alterações de código com suporte (C++)](../debugger/supported-code-changes-cpp.md)