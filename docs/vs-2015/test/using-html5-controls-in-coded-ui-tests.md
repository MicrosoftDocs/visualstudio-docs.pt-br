---
title: Uso de controles HTML5 em testes de IU codificados | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 2000b214-ae92-4334-b549-aa0eb4f45fe1
caps.latest.revision: 19
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 029b547102863f4798ad261deb678c4d98596916
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657197"
---
# <a name="using-html5-controls-in-coded-ui-tests"></a>Usando controles HTML5 em testes de IU codificados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os teste de IU codificados incluem suporte a alguns dos controles HTML5 incluídos no Internet Explorer 9 e no Internet Explorer 10.

 **Requirements**

- Visual Studio Enterprise

> [!WARNING]
> Em versões anteriores do Internet Explorer 10, era possível executar testes de UI codificados em um nível de privilégio mais alto em comparação do processo do Internet Explorer. Ao executar testes de UI codificados no Internet Explorer 10, o teste de IU codificado e o processo do Internet Explorer devem ser o mesmo nível de privilégio. Isso ocorre devido a recursos mais seguros do AppContainer no Internet Explorer 10.

> [!WARNING]
> Se você criar um teste de IU codificado no Internet Explorer 10, talvez eles não sejam executados no Internet Explorer 9 ou no Internet Explorer 8. Isso ocorre porque o Internet Explorer 10 inclui controles HTML5, como Audio, Video, ProgressBar e Slider. Esses controles HTML5 não são reconhecidos pelo Internet Explorer 9 ou pelo Internet Explorer 8. Da mesma forma, seu teste de IU codificado usando o Internet Explorer 9 pode incluir alguns controles do HTML5 que também não serão reconhecidos pelo Internet Explorer 8.

## <a name="supported-html5-controls"></a>Controles do HTML5 com suporte
 Testes de UI codificados incluem suporte para registro, reprodução e validação dos seguintes controles HTML5:

- [Controle de áudio](#audio-control)

- [Controle Video](#video-control)

- [Slider](#slider)

- [ProgressBar](#progressbar)

### <a name="audio-control"></a>Controle de áudio
 **Controle de áudio:** ações no controle do HTML5 áudio são registradas e reproduzidas corretamente.

 ![Controle do HTML5 áudio](../test/media/codedui-html5-audio.png)

|Ação|Gravando|Código gerado|
|------------|---------------|--------------------|
|**Reproduzir áudio**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Play \<name> Audio from 00:00:00|HtmlAudio.Play(TimeSpan)|
|**Busca em uma hora específica no áudio**|Seek \<name> Audio to 00:01:48|HtmlAudio.Seek(TimeSpan)|
|**Pausar áudio**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Pause \<name> Audio at 00:01:53|HtmlAudio.Pause(TimeSpan)|
|**Desativar áudio**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Mute \<name> Audio|HtmlAudio.Mute()|
|**Ativar áudio**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Unmute \<name> Audio|HtmlAudio.Unmute()|
|**Alterar volume de áudio**|Definir volume de \<name> Audio to 79%|HtmlAudio.SetVolume(float)|

 As seguintes propriedades estão disponíveis para HtmlAudio e você pode adicionar uma declaração todos eles:

```
string AutoPlay
string Controls
string CurrentSrc
string CurrentTime
string CurrentTimeAsString
string Duration
string DurationAsString
string Ended
string Loop
string Muted
string Paused
string PlaybackRate
string ReadyState
string Seeking
string Src
string Volume
```

 **Propriedades de pesquisa:** as propriedades de pesquisa para `HtmlAudio` são `Id`, `Name` e `Title`.

 **Propriedades de filtro:** as propriedades de filtro para `HtmlAudio` são `Src`, `Class`, `ControlDefinition` e `TagInstance`.

> [!NOTE]
> O tempo de busca de Seek e Pause pode ser significativo. Durante a reprodução, o teste de IU codificado aguardará até que o tempo especificado em `(TimeSpan)` antes da pausa do áudio. Se por alguma circunstância especial, o tempo especificado tiver passado antes de atingir o comando Pause, uma exceção será lançada.

### <a name="video-control"></a>Controle de vídeo
 **Controle de vídeo:** ações no controle de vídeo HTML5 são registradas e reproduzidas corretamente.

 ![Controle do HTML5 vídeo](../test/media/codedui-html5-video.png)

|Ação|Gravando|Código gerado|
|------------|---------------|--------------------|
|**Reproduzir vídeo**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Play \<name> Video  from 00:00:00|HtmlVideo.Play(TimeSpan)|
|**Busca em uma hora específica no vídeo**|Seek \<name> Video to 00:01:48|HtmlVideo.Seek(TimeSpan)|
|**Pausar vídeo**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Pause \<name> Video at 00:01:53|HtmlVideo.Pause(TimeSpan)|
|**Desativar vídeo**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Mute \<name> Video|HtmlVideo.Mute()|
|**Ativar vídeo**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Unmute \<name> Video|HtmlVideo.Unmute()|
|**Alterar volume de vídeo**|Definir volume de \<name> Video to 79%||

 Todas as propriedades do HtmlAudio estão disponíveis para HtmlVideo. Além disso, as três propriedades a seguir também estão disponíveis. A asserção pode ser adicionada a todos eles.

```
string Poster
string VideoHeight
string VideoWidth

```

 **Propriedades de pesquisa:** as propriedades de pesquisa para `HtmlVideo` são `Id`, `Name` e `Title`.

 **Propriedades de filtro:** as propriedades de filtro para `HtmlVideo` são `Src`, `Poster`, `Class`, `ControlDefinition` e `TagInstance`.

> [!NOTE]
> Se você Avançar ou retroceder rapidamente o vídeo usando rótulos-30s ou +30s, isso será agregado para buscar o momento apropriado.

### <a name="slider"></a>Controle deslizante
 **Controle deslizante:** ações no controle deslizante de HTML5 são registradas e reproduzidas corretamente.

 ![Controle deslizante do HTML5](../test/media/codedui-html5-slider.png)

|Ação|Gravando|Código gerado|
|------------|---------------|--------------------|
|**Definir uma posição no controle deslizante**|Definir posição como \<x> in \<name> slider|HtmlSlider.ValueAsNumber=\<x>|

 As seguintes propriedades estão disponíveis para HtmlSlider e asserção pode ser adicionada em todos eles:

```
string Disabled
string Max
string Min
string Required
string Step
string ValueAsNumber
```

### <a name="progressbar"></a>ProgressBar
 **Controle de ProgressBar:** a ProgressBar é um controle não interagível. Você pode adicionar asserções nas propriedades `Value` e `Max` desse controle.

 ![Controle ProgressBar do HTML5](../test/media/codedui-html5-progressbar.png)

## <a name="see-also"></a>Consulte também

- [Elementos HTML](https://www.w3schools.com/HTML/html_elements.asp)
- [Usar automação de interface do usuário para testar código](../test/use-ui-automation-to-test-your-code.md)
- [Criando testes de IU codificados](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)
- [Personalizando o teste de IU codificado](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeCUITModify)
- [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
