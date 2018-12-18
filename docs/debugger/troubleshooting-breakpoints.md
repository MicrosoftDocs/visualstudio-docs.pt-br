---
title: Solucionar problemas de pontos de interrupção no depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 01/23/2018
ms.technology: vs-ide-debug
ms.topic: troubleshooting
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e27d9dee1713b8d9e748ad13d75d809f2057f24a
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53052845"
---
# <a name="troubleshoot-breakpoints-in-the-visual-studio-debugger"></a>Solucionar problemas de pontos de interrupção no depurador do Visual Studio

## <a name="breakpoint-warnings"></a>Avisos de ponto de interrupção

Durante a depuração, um ponto de interrupção tem dois estados possíveis de visual: um círculo vermelho sólido e um vazio (branco preenchido) círculo. Se o depurador é capaz de definir com êxito um ponto de interrupção no processo de destino, ele permanecerá um círculo vermelho sólido. Se o ponto de interrupção é um círculo vazio, o ponto de interrupção está desabilitado ou aviso ocorreu ao tentar definir o ponto de interrupção. Para determinar a diferença, passe o mouse sobre o ponto de interrupção e ver se há um aviso.

As seções a seguir descrevem avisos proeminentes e como corrigi-los. 

### <a name="no-symbols-have-been-loaded-for-this-document"></a>"Nenhum símbolo foi carregado neste documento." 

Vá para o **módulos** janela (**Debug** > **Windows** > **módulos**) e verifique se o módulo é carregado.  
* Verifique se o módulo é carregado, o **Status do símbolo** coluna para ver se os símbolos foram carregados. 
  * Se os símbolos não são carregados, verifique o status do símbolo para diagnosticar o problema. No menu de contexto em um módulo na **módulos** janela, clique em **informações de carregamento de símbolo...**  para ver onde o depurador é examinado para tentar carregar símbolos. Para obter mais informações sobre o carregamento de símbolos, consulte [especificar arquivos de símbolo (. PDB) e código-fonte](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  * Se os símbolos foram carregados, o PDB não contém informações sobre os arquivos de origem. Estas são algumas causas possíveis: 
    * Se os arquivos de origem foram adicionados recentemente, confirme que uma versão atualizada do módulo está sendo carregada.  
    * É possível criar os PDBs removidos usando o **/PDBSTRIPPED** a opção de vinculador. Os PDBs não contêm informações do arquivo de origem. Confirme se que você estiver trabalhando com uma completa de PDB e não um PDB distribuído.  
    * O arquivo PDB parcialmente está corrompido. Exclua o arquivo e executar uma compilação limpa do módulo para tentar resolver o problema. 

* Se seu módulo não estiver carregado, verifique o seguinte para encontrar a causa: 
  * Confirme que você está depurando o processo certo. 
  * Verifique que você está depurando o tipo certo de código. Você pode descobrir que tipo de código que o depurador está configurado para depurar o **processos** janela (**Debug** > **Windows**  >  **Processos**). Por exemplo, se você está tentando depurar código c#, confirme se o depurador está configurado para o tipo apropriado do .NET Framework (por exemplo, gerenciado (v4\*) versus gerenciado (v2\*/v3\*) versus gerenciado (CoreCLR)). 

### <a name="-the-current-source-code-is-different-from-the-version-built-into"></a>"… o código-fonte atual é diferente da versão incorporada..." 

Se um arquivo de origem foi alterado e o código-fonte não coincide mais com o código que você está depurando, o depurador não definirá os pontos de interrupção no código por padrão. Normalmente, esse problema ocorre quando um arquivo de origem é alterado, mas o código-fonte não foi recriado. Para corrigir esse problema, recompile o projeto. Se achar que o sistema de compilação, o projeto já estiver atualizado, mesmo que ele não estiver, você pode forçar o sistema de projeto para recompilar por salvar o arquivo de origem novamente ou ao limpar o projeto compilar saída antes de compilar. 

Em raras situações, convém depurar sem a necessidade de código-fonte correspondente. Depuração sem correspondência de código-fonte pode levam a um confuso depuração experiência, portanto, certifique-se que isso é como você deseja continuar.  

Para desabilitar essas verificações de segurança, faça o seguinte: 
* Para modificar um único ponto de interrupção, passe o mouse sobre o ícone de ponto de interrupção no editor e clique no ícone de configurações (engrenagem). Uma janela de inspeção é adicionada ao editor. Na parte superior da janela Inspeção, há um hiperlink que indica o local do ponto de interrupção. Clique no hiperlink para permitir a modificação do local de ponto de interrupção e marque **permitir que o código-fonte seja diferente da original**.
* Para modificar essa configuração para todos os pontos de interrupção, vá para **Debug** > **opções e configurações**. Sobre o **depuração/geral** página, desmarque a **exigem arquivos de origem que correspondam exatamente à versão original** opção. Certifique-se de habilitar novamente essa opção quando tiver terminado de depuração. 

## <a name="the-breakpoint-was-successfully-set-no-warning-but-didnt-hit"></a>O ponto de interrupção foi definido com êxito (nenhum aviso), mas não foi atingido 

Esta seção fornece informações para solucionar problemas quando o depurador não estiver exibindo todos os avisos – o ponto de interrupção é um círculo vermelho durante a depuração ativamente, ainda que o ponto de interrupção não está sendo atingido. 

Aqui estão alguns itens a serem verificados: 
1. Se seu código é executado em mais de um processo ou mais de um computador, certifique-se de que você está depurando o processo certo ou computador.  
2. Confirme se o seu código está em execução. Para testar se o seu código está em execução, adicione uma chamada para `System.Diagnostics.Debugger.Break` (C# /VB) ou `__debugbreak` (C++) para a linha de código em que você está tentando definir o ponto de interrupção e, em seguida, recompile o projeto. 
3. Se você estiver depurando código otimizado, verifique se a função em que o ponto de interrupção é definido não está sendo embutido em outra função. O `Debugger.Break` teste descrito na verificação anterior pode trabalhar para testar esse problema também. 

## <a name="i-deleted-a-breakpoint-but-i-continue-to-hit-it-when-i-start-debugging-again"></a>Exclui um ponto de interrupção, mas continuar a ele durante a iniciar a depuração novamente 

Se você excluir um ponto de interrupção durante a depuração, você pode atingir o ponto de interrupção novamente na próxima vez que você iniciar a depuração. Para interromper a atingir esse ponto de interrupção, verifique se todas as instâncias do ponto de interrupção são removidas do **pontos de interrupção** janela.  
