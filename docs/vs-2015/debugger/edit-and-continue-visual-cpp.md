---
title: Editar e continuar (Visual C++) | Microsoft Docs
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
helpviewer_keywords:
- Edit and Continue [C++]
- debugging [C++], Edit and Continue
- C/C++, Edit and Continue
ms.assetid: 1815251e-a877-433e-9e5e-69bd9ba254c7
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6e1dc97af70f575632629a13ea67e905f2ad0815
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51748357"
---
# <a name="edit-and-continue-visual-c"></a>Editar e continuar (Visual C++)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar Editar e continuar em projetos do Visual C++. Ver [alterações de código com suporte (C++)](../debugger/supported-code-changes-cpp.md) para obter informações sobre as limitações de editar e continuar.  
  
 A partir do Visual Studio 2015 atualização 1, agora você pode usar Editar e continuar em aplicativos da Windows Store C++ e aplicativos de DirectX, porque agora ela dá suporte a **/ZI** opção de compilador com **/bigobj** alternar. Você também pode usar Editar e continuar com os binários compilados com o **/FASTLINK** alternar.  
  
 Outros aprimoramentos de atualização 1 incluem uma caixa de diálogo de espera cancelável, novo e notificação quando um arquivo não suporta editar e continuar. Para obter mais informações sobre as melhorias de atualização 1, consulte [melhorias de C++ Edit e Continue no Visual Studio 2015 atualização 1](http://blogs.msdn.com/b/vcblog/archive/2015/11/30/improvements-for-c-edit-and-continue-in-visual-studio-2015-update-1.aspx).  
  
 O [/Zo (aprimorar otimizado de depuração)](http://msdn.microsoft.com/library/eea8d89a-7fe0-4fe1-86b2-7689bbebbd7f) opção de compilador que foi introduzida no Visual Studio 2013 atualização 3 adiciona informações adicionais para arquivos. PDB (símbolo) para binários compilados sem a [/Od (desabilitar (Depurar)) ](http://msdn.microsoft.com/library/aafb762y.aspx) opção.  
  
 **/Zo** desabilita editar e continuar. Ver [como: depurar o código otimizado](../debugger/how-to-debug-optimized-code.md).  
  
##  <a name="BKMK_Enable_or_disable_automatic_invocation_of_Edit_and_Continue"></a> Habilitar ou desabilitar editar e continuar  
 Talvez você queira desabilitar a invocação automática de editar e continuar, se você estiver fazendo edições ao código que você deseja não aplicado durante a sessão de depuração atual. Você também pode habilitar novamente automática editar e continuar.  
  
1. No menu **Ferramentas**, escolha **Opções**.  
  
2. No **opções** caixa de diálogo, selecione **depuração / geral**.  
  
3. No **editar e continuar** grupo, marque ou desmarque as **habilitar nativo editar e continuar** caixa de seleção.  
  
   Alterar essa configuração afeta todos os projetos que você trabalha em. Você não precisa recriar seu aplicativo após alterar essa configuração. Você pode alterar a configuração mesmo enquanto você está depurando. Se você criar seu aplicativo de linha de comando ou de um makefile, mas depurar no ambiente do Visual Studio, você ainda pode usar Editar e continuar se você definir a **/ZI** opção.  
  
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
  
 No Visual C++, uma caixa de diálogo informa quando o ponto de execução é alterado. Você deve verificar se o local está correto antes de continuar a depuração. Se não estiver correto, use o **definir próxima instrução** comando. Para obter mais informações, consulte [definir a próxima instrução para executar](http://msdn.microsoft.com/library/y740d9d3.aspx#BKMK_Set_the_next_statement_to_execute).  
  
##  <a name="BKMK_How_to_work_with_stale_code"></a> Como trabalhar com código obsoleto  
 Em alguns casos, Editar e Continuar não pode aplicar imediatamente alterações de código ao executável, mas talvez consiga aplicá-las posteriormente se você continuar a depuração. Isso ocorre se você editar uma função que chama a função atual ou se adicionar mais de 64 bytes de novas variáveis a uma função na pilha de chamadas  
  
 Nesses casos, o depurador continua executando o código original até que as alterações podem ser aplicadas. O código obsoleto aparece como uma janela temporária do arquivo de origem em uma janela separada de origem, com um título como, por exemplo, `enc25.tmp`. A origem editada continuará aparecendo na janela do original. Se você tentar editar o código obsoleto, será exibida uma mensagem de aviso.  
  
## <a name="see-also"></a>Consulte também  
 [Alterações de código com suporte (C++)](../debugger/supported-code-changes-cpp.md)



