---
title: Executar um teste de unidade como um processo de 64 bits
ms.date: 03/10/2020
ms.topic: how-to
helpviewer_keywords:
- unit tests, creating
- unit tests, running
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 04895e3dd72a7cb4f0373c970db0f12582506ef9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285550"
---
# <a name="run-a-unit-test-as-a-64-bit-process"></a>Executar um teste de unidade como um processo de 64 bits

Se você tiver um computador de 64 bits, você poderá executar testes de unidade e capturar informações de cobertura de código como um processo de 64 bits.

## <a name="to-run-a-unit-test-as-a-64-bit-process"></a>Para executar de um teste de unidade como um processo de 64 bits

1. Se seu código ou testes foram compilados como 32-bit/x86, mas agora você deseja executá-los como um processo de 64 bits, recompile-os como **qualquer CPU**.

   ::: moniker range="vs-2017"
   Como alternativa, no Visual Studio 2017, você também pode compilar seu projeto como **64 bits**.
   ::: moniker-end

    > [!TIP]
    > Para a máxima flexibilidade, compile seus projetos de teste com a configuração **Qualquer CPU**. Em seguida, você poderá executar os agentes de 32 bits e de 64 bits. Não há vantagem em compilar projetos de teste com a configuração de **64 bits**.

2. Defina os testes de unidade a serem executados como um processo de 64 bits.

   ::: moniker range=">=vs-2019"
   No menu do Visual Studio, escolha **teste**e, em seguida, escolha **arquitetura do processador para projetos anycpu**. Escolha **x64** para executar os testes como um processo de 64 bits.
   ::: moniker-end
   ::: moniker range="vs-2017"
   No menu do Visual Studio, escolha **testar**, escolha **configurações de teste**e, em seguida, escolha **arquitetura do processador**. Escolha **x64** para executar os testes como um processo de 64 bits.
   ::: moniker-end

   \- ou –

   Especifique `<TargetPlatform>x64</TargetPlatform>` em um arquivo *. RunSettings* . Uma vantagem desse método é que você pode especificar grupos de configurações em arquivos diferentes e mudar rapidamente entre diferentes configurações. Você também pode copiar as configurações entre soluções. Para obter mais informações, consulte [Configurar testes de unidade usando um arquivo .runsettings](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md).

## <a name="see-also"></a>Veja também

- [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md)
- [Teste de unidade em seu código](../test/unit-test-your-code.md)
