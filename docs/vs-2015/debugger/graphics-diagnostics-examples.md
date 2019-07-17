---
title: Exemplos de diagnóstico de gráficos | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 45dd86b2-801e-4b07-a8c4-7bd25641d7f8
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 14b4ac689109e29baa4ee06c668b208d0d5227b0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159713"
---
# <a name="graphics-diagnostics-examples"></a>Exemplos de diagnóstico do gráfico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esses exemplos mostram como depurar problemas de renderização em aplicativos baseados em DirectX usando o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]Diagnóstico de Gráficos.  
  
## <a name="capturing-graphics-information"></a>Capturando informações de gráficos  
 Antes de usar o Diagnóstico de Gráficos para diagnosticar problemas de renderização no aplicativo, você deve capturar informações de gráficos do aplicativo durante sua execução. As informações de gráficos podem ser capturadas de um aplicativo que está em execução localmente, ou em um computador ou outro dispositivo remoto. Esses passo a passos demonstram como você pode capturar informações de gráficos de um aplicativo de forma programática ou manual:  
  
- [Passo a passo: Como capturar informações de gráficos](../debugger/walkthrough-capturing-graphics-information.md)  
  
- [Passo a passo: Como capturar informações de gráficos de forma programática](../debugger/walkthrough-capturing-graphics-information-programmatically.md)  
  
## <a name="use-graphics-diagnostics-with-an-arm-based-device"></a>Usar o Diagnóstico de Gráficos com um dispositivo baseado em ARM  
 Você pode usar o Diagnóstico de Gráficos para depurar seu aplicativo Direct3D em um dispositivo baseado em ARM usando a depuração remota. Confira mais informações em [Como Usar o Diagnóstico de Gráficos com um dispositivo ARM](../debugger/how-to-use-graphics-diagnostics-with-an-arm-device.md).  
  
## <a name="playing-back-graphics-information"></a>Reproduzindo informações sobre gráficos  
 Após capturar informações de gráficos de um aplicativo em execução, você pode reproduzir os eventos capturados para diagnosticar problemas de renderização. Para reproduzir, é possível usar seu computador de desenvolvimento, um computador ou dispositivo remoto ao qual esteja conectado. Para obter mais informações, confira [Como: Alterar o computador de reprodução de Diagnóstico de Gráficos](../debugger/how-to-change-the-graphics-diagnostics-playback-machine.md).  
  
## <a name="debugging-missing-objects"></a>Depurando objetos ausentes  
 Um objeto (ou objetos) ausente é um dos problemas mais comuns de renderização que os desenvolvedores de gráfico enfrentam. Esse tipo de problema pode ser difícil de diagnosticar porque diversos tipos de erros diferentes podem fazer com que um objeto aparentemente desapareça. As causas típicas para objetos ausentes incluem um estado de dispositivo configurado inadequadamente, problemas na transformação da geometria do objeto ou um pipeline de gráfico mal configurado.  
  
 Esses cenários demonstram como você pode usar o Diagnóstico de Gráficos para determinar por que um objeto está ausente e localizar o código responsável.  
  
- [Passo a passo: Objetos ausentes devido ao estado do dispositivo](../debugger/walkthrough-missing-objects-due-to-device-state.md)  
  
- [Passo a passo: Objetos ausentes devido ao sombreamento de vértice](../debugger/walkthrough-missing-objects-due-to-vertex-shading.md)  
  
- [Passo a passo: Objetos ausentes devido a configuração incorreta do pipeline](../debugger/walkthrough-missing-objects-due-to-misconfigured-pipeline.md)  
  
## <a name="debugging-rendering-errors"></a>Depurando erros de renderização  
 Um objeto (ou objetos) que não tem a aparência correta é outro problema comum enfrentado pelos desenvolvedores de gráfico. Esse tipo de problema pode ser difícil de diagnosticar porque a aparência incorreta e sua causa podem ser bastante óbvias, como a associação da textura errada, ou bastante sutis, como um bug no código do sombreador ou uma interação inesperada entre sombreadores. Alguns problemas podem ser causados por uma combinação de erros.  
  
 Segue um cenário que demonstra como usar o Diagnóstico de Gráficos para identificar um problema de renderização não tão sutil causado por um pequeno bug no sombreador:  
  
- [Passo a passo: Como depurar erros de renderização devido ao sombreamento](../debugger/walkthrough-debugging-rendering-errors-due-to-shading.md)  
  
## <a name="debugging-compute-shaders"></a>Depurando sombreadores de cálculo  
 Você pode usar o Diagnóstico de Gráficos para depurar kernels do sombreador de cálculo do DirectCompute que geram resultados incorretos. Com o DirectCompute, você pode usar a potência computacional da GPU para realizar cálculos em um grande número de elementos de dados paralelos. Para determinados tipos de problemas, utilizar a GPU pode ter um desempenho muitas vezes mais rápido que até mesmo um código de CPU bem-otimizado. No entanto, depuradores tradicionais não são capazes de detectar códigos executados na GPU. Depurar esse tipo de código requer ferramentas especializadas, que geralmente são específicas do fornecedor e podem não se integrar bem com o Visual Studio. Para tornar a depuração de sombreadores de cálculo mais consistente entre uma série de GPUs, o Diagnóstico de Gráficos captura eventos de expedição do DirectCompute, além de eventos de renderização do Direct3D, para que você possa usar ferramentas familiares para depurar problemas no código do sombreador de cálculo.  
  
 Para um cenário que demonstra como depurar um problema de simulação é causado por um bug em um sombreador de cálculo, consulte [passo a passo: Usando o diagnóstico de gráficos para depurar um sombreador de cálculo](../debugger/walkthrough-using-graphics-diagnostics-to-debug-a-compute-shader.md).
