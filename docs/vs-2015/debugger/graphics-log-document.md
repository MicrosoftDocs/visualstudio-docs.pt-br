---
title: Documento de Log de elementos gráficos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.graphics.vsglog.error
- vs.graphics.experiment
- vs.graphics.vsglog
ms.assetid: 6ccb1269-d55f-49c4-920d-baedf7de2888
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 097f431446ed2148e2a61c6f85266843fe7ada44
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745164"
---
# <a name="graphics-log-document"></a>Documentos de log de gráfico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O documento de Log de gráficos é o registro de eventos de gráficos que ocorreu enquanto o aplicativo foi executado em uma sessão de diagnóstico de gráficos. Após ser gravado, você pode examinar o log no analisador de gráficos do Visual Studio para diagnosticar problemas de desempenho e renderização.  
  
 Este é o que um documento de log gráficos é semelhante no analisador de gráficos:  
  
 ![Um log de gráficos que contém dois quadros capturados. ](../debugger/media/gfx-diag-demo-graphics-log-orientation.png "gfx_diag_demo_graphics_log_orientation")  
  
## <a name="understanding-graphics-log-documents"></a>Entendendo os documentos de log de gráficos  
 Usando o analisador de gráficos para examinar um documento de log de gráficos, você pode visualizar os efeitos de eventos do Direct3D no destino de renderização que ocorreram durante a captura. É possível indicar as áreas exatas do destino de renderização com saídas inesperadas. Ao selecionar um pixel na área afetada, você pode usar os diagnósticos gráficos para inspecioná-la e inspecionar seus sombreadores, os eventos do Direct3D que a afetaram, a pilha de chamadas do aplicativo que resultou nesses eventos e os objetos do DirectX compatíveis com esses eventos. Você pode usar essas informações para diagnosticar problemas de renderização em seu jogo ou aplicativo.  
  
 A parte superior da janela (**Graphics experiment**) exibe a saída de destino de renderização atual do quadro selecionado e a parte inferior exibe uma **lista de quadros** que contém imagens em miniatura das quadros capturados.  
  
#### <a name="to-inspect-a-frame"></a>Para inspecionar um quadro  
  
-   No **lista de quadros**, selecione o quadro que você deseja inspecionar. A saída do destino de renderização que aparece na parte superior do documento de log de gráficos é atualizada para exibir o quadro selecionado.  
  
#### <a name="to-inspect-a-pixel"></a>Para inspecionar um pixel  
  
-   Na parte superior do documento de log de gráficos, selecione o pixel desejado da saída do destino de renderização. Quando um pixel é selecionado, você pode usar o **histórico de Pixel de gráficos** janela para exibir informações detalhadas sobre o pixel selecionado. Para obter mais informações, consulte [histórico de Pixel](../debugger/graphics-pixel-history.md).  
  
## <a name="playback-machine"></a>Máquina de reprodução  
 Também é exibido no canto superior direito dos **lista de quadros** é o **máquina de reprodução**. O computador de reprodução é um computador ou dispositivo usado para reproduzir eventos de gráficos de um arquivo de log de gráficos em uma sessão de diagnóstico posterior. Ao usar outro dispositivo para reproduzir eventos capturados no lugar de seu computador de desenvolvimento, você pode reproduzir com mais precisão o ambiente de execução no qual o problema ocorreu. Por exemplo, você pode usar um computador com drivers ou hardwares gráficos que seu computador de desenvolvimento não usa ou outros tipos de dispositivos, como um tablet Windows RT baseado em ARM ou um dispositivo com Windows Phone.  
  
 Para obter informações sobre como especificar um computador de reprodução, consulte [como: alterar o computador de reprodução de diagnóstico de gráficos](../debugger/how-to-change-the-graphics-diagnostics-playback-machine.md).  
  
## <a name="graphics-log-summary-information"></a>Informações de resumo do log de elementos gráficos  
 Quando um arquivo de log de gráficos é o documento ativo, o **propriedades** janela exibe informações sobre o ambiente que hospedou a sessão de captura de diagnóstico de gráficos. Essa janela exibe informações de diversas categorias.  
  
 **Informações do Direct3D**  
 Apresenta informações sobre os recursos de hardware e driver da placa de vídeo usada durante a sessão de captura.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Formato 10 bits XR High Color**|**Verdadeiro** se o formato XR high-color de 10 bits for compatível; caso contrário, **falso**.|  
|**DirectCompute CS 4. x**|**Verdadeiro** se Compute Shader 4.0 for compatível; caso contrário, **falso**.|  
|**Sombreadores de precisão dupla**|**Verdadeiro** se o adaptador de vídeo dá suporte a valores de ponto flutuante de precisão dupla (64 bits); caso contrário, **falso**.|  
|**Listas de comando do driver**|**Verdadeiro** se o driver dá suporte a listas de comando; caso contrário, **falso**.|  
|**Driver com criações concorrentes**|**Verdadeiro** se o driver dá suporte à criação simultânea de (assíncrona); caso contrário, **falso**.|  
|**Formatos estendidos (BGRA, etc.)**|**Verdadeiro** se formatos estendidos como BGRA forem compatíveis; caso contrário, **falso**.|  
|**Nível máximo de recursos de HW**|Exibe o mais alto nível de recursos permitido pela placa de vídeo.|  
  
 **Exibir informações**  
 Apresenta informações sobre a placa de vídeo usada durante a sessão de captura.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Descrição**|A cadeia de caracteres de descrição da placa de vídeo.|  
|**Memória de vídeo**|A quantidade de memória instalada no adaptador gráfico.|  
|**Nome do driver**|O nome do driver do adaptador gráfico.|  
|**Versão do driver**|A versão do driver do adaptador gráfico.|  
|**Nome**|O nome do adaptador gráfico.|  
  
 **Arquivo de experimento**  
 Apresenta informações sobre o arquivo de experimento associado à sessão de captura.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Path**|O caminho do arquivo .vsglog. **Observação:** em capturas herdadas, essa propriedade não é usada.|  
  
 **Informações de módulo**  
 Apresenta o nome e a versão das DLLs (bibliotecas de vínculo dinâmico) que foram carregadas pelo aplicativo durante a sessão de captura.  
  
 **Informações do sistema**  
 Apresenta informações sobre o hardware e o sistema operacional que hospedou o aplicativo durante a sessão de captura.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Memória**|A quantidade de memória instalada no computador.|  
|**Arquitetura do sistema operacional**|A arquitetura da CPU de destino do sistema operacional.|  
|**Versão do sistema operacional**|A versão do sistema operacional.|  
|**Processador**|O processador instalado no computador.|  
|**Arquitetura de aplicativo de destino**|A arquitetura da CPU de destino do aplicativo. Isso pode ser diferente de **arquitetura do sistema operacional**.|  
  
 **Aplicativo de destino**  
 Apresenta informações sobre o aplicativo que passou pela sessão de captura.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Data/hora da última modificação**|A data e hora em que o aplicativo foi compilado.|  
|**Path**|O caminho do aplicativo.|  
|**ID do Processo**|A ID do processo atribuída ao aplicativo.|  
|**Versão**|A versão do aplicativo.|  
  
 **Arquivo de Log VSG**  
 Apresenta informações sobre o documento de log de gráficos.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Criado por**|O nome do aplicativo que criou o documento de log de gráficos. Por exemplo, se a sessão de captura foi iniciada no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (captura manual), o valor dessa propriedade será [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|  
|**Hora de início de sessão**|A data e hora em que a sessão de captura começou.|  
|**Size**|O tamanho do documento de log de gráficos.|  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Objetos ausentes devido ao sombreamento de vértice](../debugger/walkthrough-missing-objects-due-to-vertex-shading.md)   
 [Passo a passo: depurando erros de renderização devido ao sombreamento](../debugger/walkthrough-debugging-rendering-errors-due-to-shading.md)



