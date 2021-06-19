---
title: Solucionar problemas de pontos de interrupção no depurador | Microsoft Docs
description: Se um ponto de interrupção estiver desabilitado ou não puder ser definido, ele será exibido como um círculo vazio. Veja aqui informações sobre problemas que podem ocorrer ao definir pontos de interrupção.
ms.custom: SEO-VS-2020
ms.date: 01/23/2018
ms.topic: troubleshooting
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0801a687529b5e0f8cdf34030460f0b5fe45bc91
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386378"
---
# <a name="troubleshoot-breakpoints-in-the-visual-studio-debugger"></a>Solucionar problemas de pontos de interrupção no depurador do Visual Studio

## <a name="breakpoint-warnings"></a>Avisos de ponto de interrupção

Durante a depuração, um ponto de interrupção tem dois estados visuais possíveis: um círculo vermelho sólido e um círculo vazio (preenchido em branco). Se o depurador for capaz de definir com êxito um ponto de interrupção no processo de destino, ele permanecerá um círculo vermelho sólido. Se o ponto de interrupção for um círculo vazio, o ponto de interrupção será desabilitado ou ocorrerá um aviso ao tentar definir o ponto de interrupção. Para determinar a diferença, passe o mouse sobre o ponto de interrupção e veja se há um aviso.

As duas seções a seguir descrevem os avisos proeminentes e como corrigi-los.

### <a name="no-symbols-have-been-loaded-for-this-document"></a>"Nenhum símbolo foi carregado neste documento."

Vá para a janela **módulos** (**depurar**  >    >  **módulos** do Windows) e verifique se o módulo está carregado.
* Se o módulo estiver carregado, verifique a coluna **status do símbolo** para ver se os símbolos foram carregados.
  * Se os símbolos não forem carregados, verifique o status do símbolo para diagnosticar o problema. No menu de contexto de um módulo na janela **módulos** , clique em **informações de carregamento de símbolo...** para ver onde o depurador procurou e carregou símbolos. Para obter mais informações sobre como carregar símbolos, consulte [especificar símbolo (. pdb) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).
  * Se os símbolos forem carregados, o PDB não conterá informações sobre seus arquivos de origem. Essas são algumas causas possíveis:
    * Se os arquivos de origem foram adicionados recentemente, confirme se uma versão atualizada do módulo está sendo carregada.
    * É possível criar PDBs retirados usando a opção de vinculador **/PDBSTRIPPED** . PDBs removidos não contêm informações de arquivo de origem. Confirme que você está trabalhando com um PDB completo e não um PDB removido.
    * O arquivo PDB está parcialmente corrompido. Exclua o arquivo e execute uma compilação limpa do módulo para tentar resolver o problema.

* Se o módulo não estiver carregado, verifique o seguinte para encontrar a causa:
  * Confirme que você está depurando o processo correto.
  * Verifique se você está depurando o tipo certo de código. Você pode descobrir que tipo de código o depurador está configurado para depurar na janela **processos** (**depurar**  >    >  **processos** do Windows). Por exemplo, se você estiver tentando depurar o código C#, confirme se o depurador está configurado para o tipo e a versão apropriados do .NET (por exemplo, gerenciado (v4 \* ) versus gerenciado (v2 \* /v3 \* ) versus gerenciado (CoreCLR)).

### <a name="-the-current-source-code-is-different-from-the-version-built-into"></a>"… o código-fonte atual é diferente da versão interna do... "

Se um arquivo de origem tiver sido alterado e a origem não corresponder mais ao código que você está Depurando, o depurador não definirá pontos de interrupção no código por padrão. Normalmente, esse problema ocorre quando um arquivo de origem é alterado, mas o código-fonte não foi recriado. Para corrigir esse problema, recompile o projeto. Se o sistema de compilação considerar que o projeto já está atualizado, mesmo que não seja, você pode forçar o sistema de projeto a recriar salvando o arquivo de origem novamente ou limpando a saída de Build do projeto antes de Compilar.

Em casos raros, talvez você queira depurar sem ter o código-fonte correspondente. A depuração sem o código-fonte correspondente pode levar a uma experiência de depuração confusa, portanto, certifique-se de que é assim que você deseja continuar.

Para desabilitar essas verificações de segurança, siga um destes procedimentos:
* Para modificar um único ponto de interrupção, passe o mouse sobre o ícone de ponto de interrupção no editor e clique no ícone configurações (engrenagem). Uma janela de inspeção é adicionada ao editor. Na parte superior da janela Peek, há um hiperlink que indica o local do ponto de interrupção. Clique no hiperlink para permitir a modificação do local do ponto de interrupção e marque **permitir que o código-fonte seja diferente do original**.
* Para modificar essa configuração para todos os pontos de interrupção, vá para  >  **Opções de depuração e configurações**. Na página **depuração/geral** , desmarque a opção **exigir arquivos de origem que correspondem exatamente à versão original** . Certifique-se de habilitar novamente essa opção quando terminar a depuração.

## <a name="the-breakpoint-was-successfully-set-no-warning-but-didnt-hit"></a>O ponto de interrupção foi definido com êxito (sem aviso), mas não foi atingido

Esta seção fornece informações para solucionar problemas quando o depurador não está exibindo nenhum aviso – o ponto de interrupção é um círculo vermelho sólido enquanto está depurando ativamente, mas o ponto de interrupção não está sendo atingido.

Aqui estão algumas coisas para verificar:
1. Se o seu código for executado em mais de um processo ou em mais de um computador, verifique se você está depurando o processo ou computador certo.
2. Confirme se o código está em execução. Para testar se o código está em execução, adicione uma chamada para `System.Diagnostics.Debugger.Break` (C#/vb) ou `__debugbreak` (C++) à linha de código em que você está tentando definir o ponto de interrupção e, em seguida, recompile o projeto.
3. Se você estiver depurando código otimizado, verifique se a função em que o ponto de interrupção está definido não está sendo embutida em outra função. O `Debugger.Break` teste descrito na verificação anterior também pode funcionar para testar esse problema.

## <a name="i-deleted-a-breakpoint-but-i-continue-to-hit-it-when-i-start-debugging-again"></a>Excluí um ponto de interrupção, mas continue a clicar quando eu iniciar a depuração novamente

Se você excluiu um ponto de interrupção durante a depuração, pode atingir o ponto de interrupção novamente na próxima vez que iniciar a depuração. Para parar de atingir esse ponto de interrupção, verifique se todas as instâncias do ponto de interrupção foram removidas da janela **pontos de interrupção** .
