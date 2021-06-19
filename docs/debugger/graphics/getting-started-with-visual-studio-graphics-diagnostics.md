---
title: Guia de início do diagnóstico de gráficos | Microsoft Docs
description: Prepare-se para Diagnóstico de Gráficos pela primeira vez, capture quadros de um aplicativo Direct3D e examine-os no Analisador de Gráficos.
ms.custom: SEO-VS-2020
ms.date: 06/08/2020
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 70512b4df3be7f11973af244c336b22c59c90f8f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387600"
---
# <a name="getting-started-with-visual-studio-graphics-diagnostics"></a>Introdução ao Diagnóstico de Gráficos do Visual Studio
Nesta seção, você se preparará para usar Diagnóstico de Gráficos pela primeira vez e, em seguida, capturará quadros de um aplicativo Direct3D e os examinará no Analisador de Gráficos.

## <a name="requirements"></a>Requisitos
 Para usar Diagnóstico de Gráficos em Visual Studio, você deve usar Visual Studio Enterprise, Visual Studio Professional ou Visual Studio Community.  Outras edições, incluindo Visual Studio Code, não contêm esse recurso.

 [!INCLUDE[downloadvs](../includes/downloadvs_md.md)]

### <a name="windows-10-prerequisites"></a>Pré-requisitos do Windows 10
 O recurso opcional Ferramentas *de Gráficos* do Windows fornece a infraestrutura de captura e reprodução exigida pelo Diagnóstico de Gráficos no Windows 10.

 Para obter informações sobre como instalar o Graphics Tools, consulte [Install Graphics Tools for Windows 10](#InstallGraphicsTools).

## <a name="install-graphics-tools-for-windows-10"></a><a name="InstallGraphicsTools"></a> Instalar ferramentas gráficas para Windows 10
 No Windows 10, a infraestrutura Diagnóstico de Gráficos é fornecida por um recurso opcional do Windows chamado *Ferramentas de Gráficos*. Esse recurso é necessário para capturar e reproduzir informações gráficas no Windows 10 independentemente se o aplicativo que está sendo capturado tem como alvo uma versão anterior do Windows ou qual versão do Direct3D ele usa. Você pode optar por instalar o recurso Ferramentas de Gráficos com antecedência; caso contrário, ele será instalado sob demanda na primeira vez que você iniciar uma sessão Diagnóstico de Gráficos de Visual Studio.

#### <a name="to-install-graphics-tools-for-windows-10"></a>Para instalar as Ferramentas gráficas para Windows 10

1. Em Pesquisar, digite **Aplicativos e recursos e** abra as **configurações aplicativos & recursos.**

2. No lado direito das configurações aplicativos **&** recursos, escolha Recursos opcionais **(em** Aplicativos **& recursos**).

   As **configurações Recursos** opcionais são exibidas.

3. Nas **configurações Recursos** opcionais, escolha **Adicionar um recurso**. Uma lista de recursos opcionais que você pode instalar é exibida.

4. Selecione **Ferramentas gráficas** na lista de recursos e, em seguida, **escolha Instalar**.

   O recurso Ferramentas de Gráficos também é instalado automaticamente quando você instala o SDK do Windows 10.

> [!TIP]
> O recurso opcional de Ferramentas gráficas do Windows 10 fornece funcionalidade leve de captura e reprodução, como o programa de captura de linha de comando **dxcap.exe,** que pode ser usado em cenários de suporte, teste e diagnóstico em máquinas em que as ferramentas de desenvolvedor não estão instaladas. Para obter mais informações, consulte o tópico Ferramenta de Captura [de Linha de](command-line-capture-tool.md) Comando.

## <a name="using-graphics-diagnostics-for-the-first-time"></a>Usando Diagnóstico de Gráficos pela primeira vez
 Agora que você tem tudo de que precisa, está pronto para começar a usar Diagnóstico de Gráficos. Basta seguir estas etapas.

### <a name="1---create-a-direct3d-app"></a>1 – Criar um aplicativo Direct3D

Se você já tiver seu próprio aplicativo Direct3D para explorar Diagnóstico de Gráficos, ótimo! Caso contrário, use um dos seguintes:

::: moniker range=">=vs-2019"
Baixe um exemplo do [Direct3D Game Sample](/samples/microsoft/windows-universal-samples/simple3dgamedx/).
::: moniker-end
::: moniker range="vs-2017"
- Os modelos de projeto do Aplicativo **DirectX 11 (Universal do Windows)** ou do **Aplicativo DirectX 12 (Universal** do Windows) para Windows 10.
- [Exemplo de UAP do Direct3D 12](https://code.msdn.microsoft.com/Direct3D-12-UAP-Sample-ecb1779f) para Windows 10.
::: moniker-end

Certifique-se de que você pode criar e executar o aplicativo antes de continuar. Escolha **Criar**  >  **Solução de Build** para garantir que ela seja construída sem erros. Em seguida, **escolha Depurar** Iniciar sem  >  **Depuração** (**Ctrl + F5**) para garantir que ele seja executado corretamente. Dependendo de qual computador você está testando com a ferramenta, talvez seja necessário ajustar a plataforma e o destino de depuração para o exemplo. Por exemplo, para testar na plataforma x64 em seu computador host Visual Studio, escolha **x64** como a Plataforma de Solução e o Computador **Local** como seu destino de depuração. 

### <a name="2---start-a-graphics-diagnostics-session"></a>2 - Iniciar uma sessão Diagnóstico de Gráficos sessão
 Agora você está pronto para iniciar sua primeira sessão de diagnóstico de gráficos. No Visual Studio, no menu principal, escolha **Depurar, Gráficos,** Iniciar Depuração de Gráficos ou pressione **Alt+F5.** Isso inicia seu aplicativo em Diagnóstico de Gráficos e exibe as janelas de sessão de diagnóstico Visual Studio.

> [!IMPORTANT]
> Se você estiver executando seu aplicativo no Windows 10 e ainda não tiver instalado o recurso opcional de Ferramentas de Gráficos, será solicitado que você faça isso agora. Você deve instalá-lo antes de usar Diagnóstico de Gráficos no Windows 10.

### <a name="3---capture-frames"></a>3 – Capturar quadros
 Você estará pronto para capturar quadros assim que seu aplicativo for iniciado.

#### <a name="to-capture-single-frames"></a>Para capturar quadros individuais

- No Visual Studio, escolha o botão **Capturar Quadro** na barra de ferramentas Gráficos ou na janela de sessão de diagnóstico. Ou, se seu aplicativo tiver foco, basta pressionar a **tecla Imprimir Tela** no teclado.

#### <a name="to-capture-a-sequence-of-frames"></a>Para capturar uma sequência de quadros

- No Visual Studio, na janela de sessão de diagnóstico, de definido **Quadros** para capturar para o número de quadros que você deseja capturar em sequência e, em seguida, capture a sequência usando qualquer um dos métodos descritos acima para capturar quadros individuais.

   Para capturar quadros individuais novamente, de definir **Quadros para capturar** como *1*.

  Quando terminar de capturar quadros, basta sair  do aplicativo ou escolher o botão Parar na barra de ferramentas gráficos ou na janela de sessão de diagnóstico.

### <a name="4---examine-captured-frames-in-the-graphics-analyzer"></a>4 – Examinar quadros capturados no Analisador de Gráficos
 Agora você está pronto para examinar os quadros que acabou de capturar. Para começar a analisar um quadro, escolha o número do quadro que você deseja examinar na janela de sessão de diagnóstico. Isso abre o quadro no Analisador de **Gráficos,** em que você pode usar as ferramentas do Diagnóstico de Gráficos para  examinar como seu aplicativo usa o Direct3D para rastrear problemas de renderização ou usar a ferramenta Análise de Quadros para entender seu desempenho.

 Se você tiver selecionado o quadro errado na janela de sessão de diagnóstico ou quiser examinar um quadro diferente, poderá selecionar um novo no Analisador de Gráficos. Na guia **Renderizar Destino** da janela de log de gráficos, na imagem de destino de renderização, expanda a Lista de Quadros e escolha um quadro diferente a ser examinado. 

 Para saber mais sobre como usar as ferramentas do Analisador de Gráficos juntas, consulte [Exemplos.](graphics-diagnostics-examples.md)

## <a name="see-also"></a>Confira também
- [Elementos gráficos do Direct3D 12](/windows/desktop/direct3d12/direct3d-12-graphics)