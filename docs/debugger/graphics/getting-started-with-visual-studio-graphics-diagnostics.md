---
title: Introdução ao diagnóstico de gráficos | Microsoft Docs
ms.custom: seodec18
ms.date: 05/26/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 422a0fa4ea44cb3a605b8905282a5fe2a7e71e4c
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53055459"
---
# <a name="getting-started-with-visual-studio-graphics-diagnostics"></a>Introdução ao Diagnóstico de Gráficos do Visual Studio
Nesta seção você irá se preparar para usar o diagnóstico de gráficos pela primeira vez, em seguida, você irá capturar quadros de um aplicativo Direct3D e examiná-los no analisador de gráficos.  
  
## <a name="requirements"></a>Requisitos  
 Para usar o diagnóstico de gráficos no Visual Studio, você deve usar o Visual Studio Enterprise, Visual Studio Professional ou Visual Studio Community.  Outras edições, incluindo o código do Visual Studio, não contêm esse recurso.
 
 [!INCLUDE[downloadvs](../includes/downloadvs_md.md)]  
  
### <a name="windows-10-prerequisites"></a>Pré-requisitos do Windows 10  
 O recurso opcional do Windows *as ferramentas de gráficos* fornece a infraestrutura de captura e reprodução que é exigida pelo diagnóstico de gráficos no Windows 10.  
  
 Para obter informações sobre como instalar as ferramentas de gráficos, consulte [instalar ferramentas de gráficos para 10 Windows](#InstallGraphicsTools).  
  
##  <a name="InstallGraphicsTools"></a> Instalar as ferramentas de gráficos para Windows 10  
 No Windows 10, a infraestrutura de diagnóstico de gráficos é fornecida por um recurso opcional do Windows chamado *as ferramentas de gráficos*. Esse recurso é necessário para capturar e reproduzir informações de gráficos no Windows 10, independentemente se o aplicativo que está sendo capturado destinos de uma versão anterior do windows ou de qual versão do Direct3D que ele usa. Você pode optar por instalar o recurso ferramentas de gráficos antecipadamente; Caso contrário, será hora instalado sob demanda na primeira que iniciar uma sessão de diagnóstico de gráficos do Visual Studio.  
  
#### <a name="to-install-graphics-tools-for-windows-10"></a>Para instalar as ferramentas de gráficos para o Windows 10  
  
1. Na pesquisa, digite **aplicativos e recursos** e, em seguida, abra o **aplicativos e recursos** configurações.
  
2. No lado direito dos **aplicativos e recursos** caixa de diálogo, escolha **gerenciar recursos opcionais** (sob **aplicativos e recursos**).

   O **gerenciar recursos opcionais** caixa de diálogo é exibida.
  
3. No **gerenciar recursos opcionais** caixa de diálogo, escolha **adicionar um recurso**. É exibida uma lista de recursos opcionais que você pode instalar.  
  
4. Selecione **as ferramentas de gráficos** na lista de recursos, em seguida, escolha **instalar**.  
  
   O recurso ferramentas de gráficos também é instalado automaticamente quando você instala o SDK do Windows 10.  
  
> [!TIP]
>  O recurso opcional de ferramentas de gráficos do Windows 10 fornece a funcionalidade de captura e reprodução leve — como o programa de linha de comando de captura **dxcap.exe**— que podem ser usados em suporte, teste e cenários de diagnóstico em computadores nos quais ferramentas de desenvolvedor não estiverem instaladas. Para obter mais informações, consulte o [ferramenta de captura de linha de comando](command-line-capture-tool.md) tópico.  
  
## <a name="using-graphics-diagnostics-for-the-first-time"></a>Usando o diagnóstico de gráficos pela primeira vez  
 Agora que você tem tudo o que você precisa, você está pronto para começar a usar o diagnóstico de gráficos. Siga estas etapas.  
  
### <a name="1---create-a-direct3d-app"></a>1 - criar um aplicativo Direct3D  
 Se você já tem seu próprio aplicativo Direct3D para explorar os diagnósticos de gráficos, muito bem! Caso contrário, use um dos seguintes:

- O **aplicativo do DirectX 11 (Universal Windows)** ou **aplicativo do DirectX 12 (Universal Windows)** modelos de projeto para o Windows 10.
- [Exemplo de Direct3D 12 UAP](https://code.msdn.microsoft.com/Direct3D-12-UAP-Sample-ecb1779f) para Windows 10.  
  
  Verifique se que você pode compilar o aplicativo antes de prosseguir.  
  
### <a name="2---start-a-graphics-diagnostics-session"></a>2 - iniciar uma sessão de diagnóstico de gráficos  
 Agora você está pronto para começar a primeira sessão de diagnóstico de gráficos. No Visual Studio, no menu principal, escolha **depurar, elementos gráficos, iniciar depuração de gráficos**, ou apenas pressione **ALT+F5**. Isso inicia o aplicativo em Diagnóstico de gráficos e exibe as janelas de sessão de diagnóstico no Visual Studio.  
  
> [!IMPORTANT]
>  Se você estiver executando o aplicativo no Windows 10 e ainda não tiver instalado o recurso opcional de ferramentas de gráficos, você será solicitado a fazê-lo agora. Você deve instalá-lo antes de poder usar o diagnóstico de gráficos no Windows 10.  
  
### <a name="3---capture-frames"></a>3 - capturar quadros  
 Você está pronto para capturar quadros assim que seu aplicativo for iniciado.  
  
#### <a name="to-capture-single-frames"></a>Para capturar quadros únicos  
  
-   No Visual Studio, escolha o **capturar quadro** botão da janela de sessão de diagnóstico ou de barra de ferramentas gráficos. Ou, se seu aplicativo tem o foco, basta pressionar o **Print Screen** em seu teclado.
  
#### <a name="to-capture-a-sequence-of-frames"></a>Para capturar uma sequência de quadros  
  
- No Visual Studio, na janela de sessão de diagnóstico, defina **quadros a serem capturados** para o número de quadros que você deseja capturar na sequência, em seguida, capturar a sequência de usando qualquer um dos métodos descritos acima para capturar quadros únicos.  
  
   Para capturar quadros únicos novamente, defina **quadros a serem capturados** à *1*.  
  
  Quando você terminar apenas a captura de quadros sair do aplicativo ou escolha o **parar** botão da barra de ferramentas de gráficos ou janela de sessão de diagnóstico.  
  
### <a name="4---examine-captured-frames-in-the-graphics-analyzer"></a>4 - examine os quadros capturados no analisador de gráficos  
 Agora você está pronto para examinar os quadros capturada. Para começar a analisar um quadro, escolha o número de quadro do quadro que você deseja examinar da janela de sessão de diagnóstico. Isso abre o quadro na **analisador de gráficos**, onde você pode usar as ferramentas de diagnóstico de gráficos para examinar como o seu aplicativo usa o Direct3D para rastrear problemas de renderização, ou usar o **análise de quadros** ferramenta para Entenda seu desempenho.  
  
 Se você selecionou o errado quadro da janela de sessão de diagnóstico ou você deseja examinar um quadro diferente, você pode selecionar um novo do analisador de gráficos. Sobre o **renderizar destino** guia da janela de log de gráficos, abaixo da imagem de destino de renderização, expanda o **lista de quadros** e, em seguida, escolha um quadro diferente para examinar.  
  
 Para saber mais sobre como usar as ferramentas do analisador de gráficos em conjunto, consulte o [exemplos](graphics-diagnostics-examples.md).  
  
## <a name="see-also"></a>Consulte também  
 [Direct3D 12 gráficos](/windows/desktop/direct3d12/direct3d-12-graphics)