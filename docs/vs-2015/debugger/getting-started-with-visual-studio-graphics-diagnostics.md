---
title: Introdução ao diagnóstico de gráficos do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59131181-1caa-4b7f-be4b-e84709634edf
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5f6b6bbb10113ab6bd97767f41991219e014d39a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725568"
---
# <a name="getting-started-with-visual-studio-graphics-diagnostics"></a>Introdução ao Diagnóstico de Gráficos do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Nesta seção você irá se preparar para usar o diagnóstico de gráficos pela primeira vez, em seguida, você irá capturar quadros de um aplicativo Direct3D e examiná-los no analisador de gráficos.  
  
## <a name="requirements"></a>Requisitos  
 Para usar o diagnóstico de gráficos no Visual Studio 2015, você deve ter uma destas edições:  
  
- Visual Studio 2015 Enterprise  
  
- Visual Studio 2015 Professional  
  
- Visual Studio 2015 Community  
  
  [!INCLUDE[downloadvs](../includes/downloadvs-md.md)]  
  
### <a name="windows-10-prerequisites"></a>Pré-requisitos do Windows 10  
 O recurso opcional do Windows *as ferramentas de gráficos* fornece a infraestrutura de captura e reprodução que é exigida pelo diagnóstico de gráficos no Windows 10.  
  
 Para obter informações sobre como instalar as ferramentas de gráficos, consulte [instalar ferramentas de gráficos para 10 Windows](#InstallGraphicsTools).  
  
### <a name="windows-81-prerequisites"></a>Pré-requisitos do Windows 8.1  
 O Windows Software Development Kit (SDK) para Windows 8.1 fornece a infraestrutura de captura e reprodução que é exigida pelo diagnóstico de gráficos no Windows 8.1 e dá suporte ao desenvolvimento para Windows 8.1 e Windows 8.  
  
 [Baixe o Windows Software Development Kit (SDK) para Windows 8.1](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)  
  
 Para usar um computador de reprodução remoto que esteja executando o Windows 10 de um computador de desenvolvimento executando o Windows 8.1, você deve instalar o SDK do Windows 10 no computador de desenvolvimento e o recurso opcional de ferramentas de gráficos no computador de reprodução.  
  
##  <a name="InstallGraphicsTools"></a> Instalar as ferramentas de gráficos para Windows 10  
 No Windows 10, a infraestrutura de diagnóstico de gráficos é fornecida por um recurso opcional do Windows chamado *as ferramentas de gráficos*. Esse recurso é necessário para capturar e reproduzir informações de gráficos no Windows 10, independentemente se o aplicativo que está sendo capturado destinos de uma versão anterior do windows ou de qual versão do Direct3D que ele usa. Você pode optar por instalar o recurso ferramentas de gráficos antecipadamente; Caso contrário, será hora instalado sob demanda na primeira que iniciar uma sessão de diagnóstico de gráficos do Visual Studio.  
  
#### <a name="to-install-graphics-tools-for-windows-10"></a>Para instalar as ferramentas de gráficos para o Windows 10  
  
1. Sobre o **iniciar** menu, escolha **configurações**. O **configurações** caixa de diálogo é exibida.  
  
2. No **as configurações** caixa de diálogo, escolha **sistema**, em seguida, selecione **aplicativos instalados** na lista de configurações do sistema.  
  
3. No lado direito dos **as configurações** caixa de diálogo, escolha **gerenciar recursos opcionais** sob **aplicativos e recursos instalados**. O **gerenciar recursos opcionais** caixa de diálogo é exibida.  
  
4. No **gerenciar recursos opcionais** caixa de diálogo, escolha **adicionar um recurso**. É exibida uma lista de recursos opcionais que você pode instalar.  
  
5. Selecione **as ferramentas de gráficos** na lista de recursos, em seguida, escolha **instalar**.  
  
   O recurso ferramentas de gráficos também é instalado automaticamente quando você instala o SDK do Windows 10.  
  
> [!TIP]
>  O recurso opcional de ferramentas de gráficos do Windows 10 fornece a funcionalidade de captura e reprodução leve — como o programa de linha de comando de captura **dxcap.exe**— que podem ser usados em suporte, teste e cenários de diagnóstico em computadores nos quais ferramentas de desenvolvedor não estiverem instaladas. Para obter mais informações, consulte o [ferramenta de captura de linha de comando](../debugger/command-line-capture-tool.md) tópico.  
  
## <a name="using-graphics-diagnostics-for-the-first-time"></a>Usando o diagnóstico de gráficos pela primeira vez  
 Agora que você tem tudo o que você precisa, você está pronto para começar a usar o diagnóstico de gráficos. Basta seguir estas etapas.  
  
### <a name="1---create-a-direct3d-app"></a>1 - criar um aplicativo Direct3D  
 Se você já tem seu próprio aplicativo Direct3D para explorar os diagnósticos de gráficos, muito bem! Caso contrário, você pode usar um dos exemplos de Direct3D disponíveis na Galeria de códigos.  
  
- Para experimentar o diagnóstico de gráficos com 12, Direct3D no Windows 10 usando o Visual Studio 2015, tente as [amostra Direct3D 12 UAP](https://code.msdn.microsoft.com/Direct3D-12-UAP-Sample-ecb1779f) para Windows 10.  
  
- Para experimentar o diagnóstico de gráficos com o Direct3D 11 no Windows 10 ou Windows 8.1, você pode usar o **DirectX App (Windows Universal)** ou **DirectX App (Windows 8.1)** modelos de projeto. Ou, para algo mais interessante, experimente o [exemplo do jogo marble maze DirectX](https://code.msdn.microsoft.com/windowsapps/DirectX-Marble-Maze-Game-e4806345) para Windows 8.1.  
  
  Verifique se que você pode compilar o aplicativo antes de prosseguir.  
  
### <a name="2---start-a-graphics-diagnostics-session"></a>2 - iniciar uma sessão de diagnóstico de gráficos  
 Agora você está pronto para começar a primeira sessão de diagnóstico de gráficos. No Visual Studio, no menu principal, escolha **depurar, elementos gráficos, iniciar diagnóstico**, ou apenas pressione **ALT+F5**. Isso inicia o aplicativo em Diagnóstico de gráficos e exibe as janelas de sessão de diagnóstico no Visual Studio.  
  
> [!IMPORTANT]
>  Se você estiver executando o aplicativo no Windows 10 e ainda não tiver instalado o recurso opcional de ferramentas de gráficos, você será solicitado a fazê-lo agora. Você deve instalá-lo antes de poder usar o diagnóstico de gráficos no Windows 10.  
  
### <a name="3---capture-frames"></a>3 - capturar quadros  
 Você está pronto para capturar quadros assim que seu aplicativo for iniciado.  
  
##### <a name="to-capture-single-frames"></a>Para capturar quadros únicos  
  
-   No Visual Studio, escolha o **capturar quadro** botão da janela de sessão de diagnóstico ou de barra de ferramentas gráficos. Ou, se seu aplicativo tem o foco, basta pressionar **Print Screen**.  
  
##### <a name="to-capture-a-sequence-of-frames"></a>Para capturar uma sequência de quadros  
  
- No Visual Studio, na janela de sessão de diagnóstico, defina **quadros a serem capturados** para o número de quadros que você deseja capturar na sequência, em seguida, capturar a sequência de usando qualquer um dos métodos descritos acima para capturar quadros únicos.  
  
   Para capturar quadros únicos novamente, defina **quadros a serem capturados** para `1`.  
  
  Quando você terminar apenas a captura de quadros sair do aplicativo ou escolha o **parar** botão da barra de ferramentas de gráficos ou janela de sessão de diagnóstico.  
  
### <a name="4--examine-captured-frames-in-the-graphics-analyzer"></a>4 – examinar os quadros capturados no analisador de gráficos  
 Agora você está pronto para examinar os quadros capturada. Para começar a analisar um quadro, escolha o número de quadro do quadro que você deseja examinar da janela de sessão de diagnóstico. Isso abre o quadro na **analisador de gráficos**, onde você pode usar as ferramentas de diagnóstico de gráficos para examinar como o seu aplicativo usa o Direct3D para rastrear problemas de renderização, ou usar o **análise de quadros** ferramenta para Entenda seu desempenho.  
  
 Se você selecionou o errado quadro da janela de sessão de diagnóstico ou você deseja examinar um quadro diferente, você pode selecionar um novo do analisador de gráficos. Sobre o **renderizar destino** guia da janela de log de gráficos, abaixo da imagem de destino de renderização, expanda o **lista de quadros** e, em seguida, escolha um quadro diferente para examinar.  
  
 Para saber mais sobre como usar as ferramentas do analisador de gráficos em conjunto, consulte o [exemplos](../debugger/graphics-diagnostics-examples.md).  
  
## <a name="see-also"></a>Consulte também  
 [Direct3D 12 gráficos](http://msdn.microsoft.com/en-us/52094ae3-3b44-4689-9ee7-1ba1b3a779cb)






