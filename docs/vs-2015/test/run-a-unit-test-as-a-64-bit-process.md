---
title: Executar um teste de unidade como um processo de 64 bits | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- unit tests, creating
- unit tests, running
ms.assetid: d23a9ee7-58e3-4e8b-a38c-b2207ea73fea
caps.latest.revision: 27
ms.author: gewarren
manager: douge
ms.openlocfilehash: 32f85c68756368f2b2ee2d5b9a1d842497102f41
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49259020"
---
# <a name="run-a-unit-test-as-a-64-bit-process"></a>Executar um teste de unidade como um processo de 64 bits
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você tiver um computador de 64 bits, você poderá executar testes de unidade e capturar informações de cobertura de código como um processo de 64 bits.  
  
## <a name="running-a-unit-test-as-a-64-bit-process"></a>Executar um teste de unidade como um processo de 64 bits  
  
#### <a name="to-run-a-unit-test-as-a-64-bit-process"></a>Para executar de um teste de unidade como um processo de 64 bits  
  
1.  Se seu código ou testes foram compilados como 32-bit/x86, mas agora você deseja executá-los como um processo de 64 bits, recompile-os como **Qualquer CPU** ou, opcionalmente, como **64-bit**.  
  
    > [!TIP]
    >  Para a máxima flexibilidade, você deve compilar seus projetos de teste com a configuração **Qualquer CPU**. Em seguida, você poderá executar os agentes de 32 bits e de 64 bits. Não há vantagem em compilar projetos de teste com a configuração de **64 bits**.  
  
2.  No menu do Visual Studio, escolha **Teste**, em seguida, escolha **Configurações**e, em seguida, escolha **Arquitetura de Processador**. Escolha **x64** para executar os testes como um processo de 64 bits.  
  
     \- ou -  
  
     Especifique `<TargetPlatform>x64</TargetPlatform>` em um arquivo .runsettings. Uma vantagem desse método é que você pode especificar grupos de configurações em arquivos diferentes e mudar rapidamente entre diferentes configurações. Você também pode copiar as configurações entre soluções. Para obter mais informações, consulte [Configurar testes de unidade usando um arquivo .runsettings](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md).  
  
## <a name="see-also"></a>Consulte também  
 [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md)   
 [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)   
 [Especificando configurações de teste para testes do Visual Studio](http://msdn.microsoft.com/library/0c15317e-80c6-4317-aed3-82b8e15e3901)



