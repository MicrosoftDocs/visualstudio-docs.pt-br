---
title: Usando controles HTML5 em testes de IU codificados
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: a603a662c9007ab3ee0e66df0b23959bfdce83fb
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896179"
---
# <a name="using-html5-controls-in-coded-ui-tests"></a>Usando controles HTML5 em testes de IU codificados

Os teste de IU codificados incluem suporte a alguns dos controles HTML5 incluídos no Internet Explorer 9 e no Internet Explorer 10.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

 **Requisitos**

-   Visual Studio Enterprise

> [!WARNING]
> Em versões anteriores do Internet Explorer 10, era possível executar testes de UI codificados em um nível de privilégio mais alto em comparação do processo do Internet Explorer. Ao executar testes de UI codificados no Internet Explorer 10, o teste de IU codificado e o processo do Internet Explorer devem ser o mesmo nível de privilégio. Isso ocorre devido a recursos mais seguros do AppContainer no Internet Explorer 10.

> [!WARNING]
> Se você criar um teste de IU codificado no Internet Explorer 10, talvez eles não sejam executados no Internet Explorer 9 ou no Internet Explorer 8. Isso ocorre porque o Internet Explorer 10 inclui controles HTML5, como Audio, Video, ProgressBar e Slider. Esses controles HTML5 não são reconhecidos pelo Internet Explorer 9 ou pelo Internet Explorer 8. Da mesma forma, seu teste de IU codificado usando o Internet Explorer 9 pode incluir alguns controles do HTML5 que também não serão reconhecidos pelo Internet Explorer 8.

## <a name="audio-control"></a>Controle de áudio

**Controle de áudio:** ações no controle do HTML5 áudio são registradas e reproduzidas corretamente.

![Controle do HTML5 áudio](../test/media/codedui_html5_audio.png)

|Ação|Gravando|Código gerado|
|-|---------------|-|
|**Reproduzir áudio**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Play \<name> Audio from 00:00:00|HtmlAudio.Play(TimeSpan)|
|**Busca em uma hora específica no áudio**|Seek \<name> Audio to 00:01:48|HtmlAudio.Seek(TimeSpan)|
|**Pausar áudio**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Pause \<name> Audio at 00:01:53|HtmlAudio.Pause(TimeSpan)|
|**Desativar áudio**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Mute \<name> Audio|HtmlAudio.Mute()|
|**Ativar áudio**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Unmute \<name> Audio|HtmlAudio.Unmute()|
|**Alterar volume de áudio**|Definir volume de \<name> Audio to 79%|HtmlAudio.SetVolume(float)|

Confira [HTMLAudioElement](https://developer.mozilla.org/docs/Web/API/HTMLAudioElement) para obter uma lista de propriedades às quais você pode adicionar uma declaração.

 **Propriedades de pesquisa:** as propriedades de pesquisa para `HtmlAudio` são `Id`, `Name` e `Title`.

 **Propriedades de filtro:** as propriedades de filtro para `HtmlAudio` são `Src`, `Class`, `ControlDefinition` e `TagInstance`.

> [!NOTE]
> O tempo de busca de Seek e Pause pode ser significativo. Durante a reprodução, o teste de IU codificado aguardará até que o tempo especificado em `(TimeSpan)` antes da pausa do áudio. Se por alguma circunstância especial, o tempo especificado tiver passado antes de atingir o comando Pause, uma exceção será lançada.


## <a name="video-control"></a>Controle de vídeo
 **Controle de vídeo:** ações no controle de vídeo HTML5 são registradas e reproduzidas corretamente.

 ![Controle do HTML5 vídeo](../test/media/codedui_html5_video.png)

|Ação|Gravando|Código gerado|
|-|---------------|-|
|**Reproduzir vídeo**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Play \<name> Video  from 00:00:00|HtmlVideo.Play(TimeSpan)|
|**Busca em uma hora específica no vídeo**|Seek \<name> Video to 00:01:48|HtmlVideo.Seek(TimeSpan)|
|**Pausar vídeo**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Pause \<name> Video at 00:01:53|HtmlVideo.Pause(TimeSpan)|
|**Desativar vídeo**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Mute \<name> Video|HtmlVideo.Mute()|
|**Ativar vídeo**<br /><br /> Diretamente do controle ou do menu de contexto de controles.|Unmute \<name> Video|HtmlVideo.Unmute()|
|**Alterar volume de vídeo**|Definir volume de \<name> Video to 79%||

Confira [HTMLVideoElement](https://developer.mozilla.org/docs/Web/HTML/Element/video) para obter uma lista de propriedades às quais você pode adicionar uma declaração.

 **Propriedades de pesquisa:** as propriedades de pesquisa para `HtmlVideo` são `Id`, `Name` e `Title`.

 **Propriedades de filtro:** as propriedades de filtro para `HtmlVideo` são `Src`, `Poster`, `Class`, `ControlDefinition` e `TagInstance`.

> [!NOTE]
> Se você Avançar ou retroceder rapidamente o vídeo usando rótulos-30s ou +30s, isso será agregado para buscar o momento apropriado.

## <a name="progressbar"></a>ProgressBar
 **Controle de ProgressBar:** a ProgressBar é um controle não interagível. Você pode adicionar asserções nas propriedades `Value` e `Max` desse controle. Para obter mais informações, confira [HTMLProgressElement](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress).

 ![Controle ProgressBar do HTML5](../test/media/codedui_html5_progressbar.png)

## <a name="see-also"></a>Consulte também

- [Elementos HTML](https://developer.mozilla.org/docs/Web/HTML/Element)
- [Usar a automação de interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md)
- [Criar testes de IU codificados](../test/use-ui-automation-to-test-your-code.md)
- [Configurações e plataformas compatíveis para testes de IU codificados e gravações de ação](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
