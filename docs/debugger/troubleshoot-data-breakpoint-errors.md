---
title: Não é possível definir o ponto de interrupção de dados | Microsoft Docs
description: Encontre explicações, soluções e soluções alternativas para "Não é possível definir erros de ponto de interrupção de dados" que ocorrem ao usar "Break when Value Changes".
ms.custom: SEO-VS-2020
ms.date: 5/19/2020
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
ms.openlocfilehash: 73e7e02d90e2a89c81b5e690718c95fe7efe0fb3
ms.sourcegitcommit: 6e27b1238a8aa704b127eac34f4173e9d56690c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2021
ms.locfileid: "110231959"
---
# <a name="troubleshooting-data-breakpoint-errors"></a>Solução de problemas de erros de ponto de interrupção de dados
Esta página explica como resolver erros comuns vistos ao usar "Break when Value Changes"

## <a name="diagnosing-unable-to-set-data-breakpoint-errors"></a>Diagnosticando erros "Não é possível definir o ponto de interrupção de dados"
> [!IMPORTANT]
> Os pontos de interrupção de dados gerenciados são suportados no .NET Core 3.0 e acima e no .NET 5.0.3 e acima. Você pode baixar o mais recente [aqui.](https://dotnet.microsoft.com/download)

Abaixo está uma lista de erros que podem ocorrer ao usar pontos de interrupção de dados gerenciados. Eles contêm mais explicações sobre por que o erro está ocorrendo e possíveis soluções ou soluções alternativas para resolver o erro.

- *"A versão do .NET usada pelo processo de destino não dá suporte a pontos de interrupção de dados. Os pontos de interrupção de dados exigem o .NET Core 3.x ou o .NET 5.0.3+, em execução no x86 ou x64."*

  - O suporte para pontos de interrupção de dados gerenciados começou no .NET Core 3.0. Atualmente, não há suporte para ele no .NET Framework, versões do .NET Core na versão 3.0 ou versões do .NET na versão 5.0.3. 
    
  - **Solução:** a solução para isso seria atualizar seu projeto para o .NET Core 3.0.

- *"O valor não pode ser encontrado no heap gerenciado e não pode ser rastreado."*
  - Variável declarada na pilha.
    - Não damos suporte à configuração de pontos de interrupção de dados para variáveis criadas na pilha, pois essa variável será inválida quando a função sair.
    - **Solução alternativa:** de definir pontos de interrupção em linhas em que a variável é usada.

  - "Break when Value changes" em uma variável que não é expandida de um menu suspenso.
    - O depurador precisa saber internamente o objeto que contém o campo que você deseja acompanhar. O Coletor de Lixo pode mover seu objeto no heap para que o depurador precise saber o objeto que está mantendo a variável que você deseja acompanhar. 
    - **Solução** alternativa: se você estiver em um método dentro do objeto no qual deseja definir um ponto de interrupção de dados, vá para cima um quadro e use a janela para expandir o objeto e definir um ponto de interrupção de dados no campo `locals/autos/watch` que você deseja.

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

- *"A classe **X** tem uma exibição de depurador personalizada que bloqueia o uso de pontos de interrupção de dados em dados específicos apenas para ele."*
  
  - Os pontos de interrupção de dados só têm suporte na memória que é criada pelo processo de destino (o aplicativo que está sendo depurado). A memória em que o ponto de interrupção de dados está sendo definido foi sinalizada como possivelmente sendo de propriedade de um objeto criado por um [atributo DebuggerTypeProxy](using-debuggertypeproxy-attribute.md) ou outra coisa que não faz parte do processo de destino.
  - **Solução alternativa:** expanda a "Exibição Bruta" dos objetos em vez de expandir a exibição DebuggerTypeProxy dos objetos e, em seguida, de definir o ponto de interrupção de dados. Isso garantirá que o ponto de interrupção de dados não está na memória pertencente a um objeto criado por um atributo DebuggerTypeProxy.

## <a name="data-breakpoint-hardware-limitations"></a>Limitações de hardware do ponto de interrupção de dados

A arquitetura (configuração de plataforma) em que seu programa é executado tem um número limitado de pontos de interrupção de dados de hardware que ele pode usar. A tabela a seguir indica quantos registros estão disponíveis para uso por arquitetura.

| Arquitetura | Número de pontos de interrupção de dados com suporte de hardware | Tamanho máximo de byte|
| :-------------: |:-------------:| :-------------:|
| x86 | 4 | 4 |
| x64 | 4 | 8 |
| ARM | 1 | 4 |
| ARM64 | 2 | 8 |

## <a name="provide-feedback"></a>Fornecer comentários

Para problemas ou sugestões sobre esse recurso, informe-nos por meio da Ajuda > Enviar comentários > [relatar](../ide/how-to-report-a-problem-with-visual-studio.md) um problema no IDE ou no [Developer Community](https://aka.ms/feedback/suggest?space=8).

## <a name="see-also"></a>Consulte também

- [Usando "Break when Value changes" no .NET Core 3.0](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus).
- [DevBlog: break when value changes: Data Breakpoints for .NET Core in Visual Studio 2019](https://devblogs.microsoft.com/visualstudio/break-when-value-changes-data-breakpoints-for-net-core-in-visual-studio-2019/)
