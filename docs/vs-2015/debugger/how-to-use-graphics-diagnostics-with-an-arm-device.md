---
title: 'Como: usar o diagnóstico de gráficos com um dispositivo ARM | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 346fd3c0-9e92-4ab8-bb3b-1aa9000a2483
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4c5122cb009b3624388ff8825b34cae8ca44a546
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51728668"
---
# <a name="how-to-use-graphics-diagnostics-with-an-arm-device"></a>Como usar diagnóstico de gráficos com um dispositivo ARM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Diagnóstico de Gráficos oferece suporte à depuração remota de aplicativos Direct3D em dispositivos baseados em ARM que executam o Windows RT 8.1 ou Windows Phone 8.1. É possível capturar informações de gráficos do aplicativo Direct3D enquanto ele é executado no dispositivo ou usar o dispositivo como computador de reprodução para obter informações de gráficos capturadas anteriormente.  
  
## <a name="using-graphics-diagnostics-with-an-arm-based-device"></a>Usando o Diagnóstico de Gráficos com um dispositivo baseado em ARM  
 Como o Visual Studio não é executado em dispositivos baseados em ARM, é preciso usar o depurador remoto para analisar um aplicativo executado neles. O depurador remoto oferece suporte à captura e reprodução de gráficos para que seja possível diagnosticar erros de renderização e avaliar o desempenho dos gráficos nesses dispositivos de maneira tão fácil quanto depurar seu aplicativo neles.  
  
 Para usar recursos de diagnóstico de gráficos, primeiro habilite a depuração remota em seu dispositivo.  
  
#### <a name="to-enable-remote-debugging-on-your-arm-based-device"></a>Para habilitar a depuração remota em seu dispositivo baseado em ARM  
  
1.  Instalar o [política de Kits ARM](http://msdn.microsoft.com/windows/desktop/dn469188) em seu dispositivo baseado em ARM.  
  
2.  Instalar o [ferramentas de depuração remota](http://go.microsoft.com/fwlink/?LinkId=393086) em seu dispositivo baseado em ARM.  
  
> [!IMPORTANT]
>  No caso de dispositivos do Windows Phone 8.1, pode ser preciso registrar seu telefone para o desenvolvimento. Para fazer isso, você deve ser um desenvolvedor registrado. Para obter mais informações, consulte [como implantar e executar um aplicativo para Windows Phone 8](http://msdn.microsoft.com/library/windowsphone/develop/ff402565.aspx).  
  
 Após habilitar a depuração remota em seu dispositivo, torne-o seu destino de depuração e inicie o Diagnóstico de Gráficos.  
  
#### <a name="to-configure-and-start-graphics-diagnostics-on-your-device"></a>Para configurar e iniciar o Diagnóstico de Gráficos em seu dispositivo  
  
1.  Sobre o **plataformas de solução** lista suspensa, selecione **ARM** para que seu dispositivo baseado em ARM estará disponível como um destino de depuração remoto.  
  
2.  Sobre o **destino de depuração** lista suspensa, selecione seu dispositivo ARM.  
  
3.  No menu, escolha **Debug**, **gráficos**, **iniciar diagnóstico**. (Teclado: Alt + F5)  
  
## <a name="see-also"></a>Consulte também  
 [Executar aplicativos da Store do Windows em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md)   
 [Como alterar o computador de reprodução de diagnóstico de gráficos](../debugger/how-to-change-the-graphics-diagnostics-playback-machine.md)



