---
title: Erro-não é possível definir o ponto de interrupção de dados | Microsoft Docs
ms.date: 12/3/2019
ms.topic: error-reference
f1_keywords:
- vs.debug.error.unable_to_set_data_breakpoint
dev_langs:
- CSharp
helpviewer_keywords:
- debugging [Visual Studio], managed
- debugging managed code, data breakpoint
ms.assetid: b06b5d65-424b-490f-bf58-97583cd7006a
author: wardengnaw
ms.author: waan
manager: caslan
ms.workload:
- multiple
ms.openlocfilehash: dab5e146d510601c6e93582b6b128abcd964b4a7
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85459929"
---
# <a name="troubleshooting-data-breakpoint-errors"></a>Solucionando problemas de erros de ponto de interrupção de dados
Esta página orientará você na resolução de erros comuns vistos ao usar "interromper quando o valor for alterado"

## <a name="diagnosing-unable-to-set-data-breakpoint-errors"></a>Diagnosticando erros de "não é possível definir o ponto de interrupção de dados"
> [!IMPORTANT]
> Os pontos de interrupção de dados gerenciados têm suporte no .NET Core 3,0 e em cima. Você pode baixar o mais recente [aqui](https://dotnet.microsoft.com/download).

Abaixo está uma lista de erros que podem ocorrer ao usar pontos de interrupção de dados gerenciados. Eles contêm uma explicação adicional sobre por que o erro está ocorrendo e possíveis soluções ou soluções alternativas para resolver erros.

- *"A versão do .NET usada pelo processo de destino não oferece suporte a pontos de interrupção de dados. Os pontos de interrupção de dados exigem o .NET Core 3.0 + em execução em x86 ou x64. "*

    - O suporte para pontos de interrupção de dados gerenciados começou no .NET Core 3,0. No momento, não há suporte para ele no .NET Framework ou na versão do .NET Core em 3,0. 
    
    - **Solução**: a solução para isso seria atualizar seu projeto para o .net Core 3,0.

- *"O valor não pode ser encontrado no heap gerenciado e não pode ser acompanhado."*
    - Variável declarada na pilha.
        - Não há suporte para definir pontos de interrupção de dados para variáveis criadas na pilha, pois essa variável será inválida quando a função for encerrada.
        - **Solução alternativa**: defina os pontos de interrupção nas linhas em que a variável é usada.

    - "Interromper quando o valor é alterado" em uma variável que não é expandida de uma lista suspensa.
        - O depurador internamente precisa saber o objeto que contém o campo que você deseja rastrear. O coletor de lixo pode mover seu objeto no heap para que o depurador precise saber o objeto que está mantendo a variável que você deseja rastrear. 
        - **Solução alternativa**: se você estiver em um método dentro do objeto do qual deseja definir um ponto de interrupção de dados, vá um quadro e use a `locals/autos/watch` janela para expandir o objeto e definir um ponto de interrupção de dados no campo desejado.

- *"Os pontos de interrupção de dados não têm suporte para campos estáticos ou propriedades estáticas."*
    
    - Não há suporte para campos e propriedades estáticos no momento. Se você estiver interessado nesse recurso, forneça [comentários](#provide-feedback).

- *"Não é possível rastrear campos e propriedades de structs."*

    - Não há suporte para campos e propriedades de structs no momento. Se você estiver interessado nesse recurso, forneça [comentários](#provide-feedback).

- *"O valor da propriedade foi alterado e não pode mais ser acompanhado."*

    - Uma propriedade pode alterar como ela é calculada durante o tempo de execução e, se isso acontecer, o número de variáveis que a propriedade depende aumentará e poderá exceder a limitação de hardware. Veja `"The property is dependent on more memory than can be tracked by the hardware."` abaixo.

- *"A propriedade depende de mais memória do que pode ser controlada pelo hardware."*
    
    - Cada arquitetura tem um número definido de bytes e pontos de interrupção de dados de hardware que ele pode dar suporte e a propriedade para a qual você deseja definir um ponto de interrupção de dados excedeu esse limite. Consulte a tabela [limitações de hardware de ponto de interrupção de dados](#data-breakpoint-hardware-limitations) para descobrir quantos pontos de interrupção e bytes de dados com suporte de hardware estão disponíveis para a arquitetura que você está usando. 
    - **Solução alternativa**: defina um ponto de interrupção de dados em um valor que possa ser alterado dentro da propriedade.

- *"Não há suporte para pontos de interrupção de dados ao usar o avaliador de expressão C# herdado".*

    - Os pontos de interrupção de dados só têm suporte no avaliador de expressão C# não herdado. 
    - **Solução**: você desabilita o avaliador de expressão C# herdado acessando em `Debug -> Options` `Debugging -> General` desmarcar `"Use the legacy C# and VB expression evaluators"` .

## <a name="data-breakpoint-hardware-limitations"></a>Limitações de hardware de ponto de interrupção de dados

A arquitetura (configuração de plataforma) em que seu programa é executado tem um número limitado de pontos de interrupção de dados de hardware que ele pode usar. A tabela a seguir indica quantos registros estão disponíveis para uso por arquitetura.

| Arquitetura | Número de pontos de interrupção de dados com suporte de hardware | Tamanho máximo de bytes|
| :-------------: |:-------------:| :-------------:|
| x86 | 4 | 4 |
| x64 | 4 | 8 |
| ARM | 1 | 4 |
| ARM64 | 2 | 8 |

## <a name="provide-feedback"></a>Fornecer comentários
Para quaisquer problemas ou sugestões sobre esse recurso, informe-nos por meio da ajuda > enviar comentários > [relatar um problema](../ide/how-to-report-a-problem-with-visual-studio.md) no IDE ou na [comunidade de desenvolvedores](https://developercommunity.visualstudio.com/).

## <a name="see-also"></a>Veja também
- [Usando "interromper quando o valor for alterado" no .NET Core 3,0](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus).
- [DevBlog: quebra quando o valor é alterado: pontos de interrupção de dados para .NET Core no Visual Studio 2019](https://devblogs.microsoft.com/visualstudio/break-when-value-changes-data-breakpoints-for-net-core-in-visual-studio-2019/)
