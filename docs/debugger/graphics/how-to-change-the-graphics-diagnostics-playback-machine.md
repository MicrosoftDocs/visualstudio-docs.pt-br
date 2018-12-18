---
title: 'Como: alterar a máquina de reprodução de diagnóstico de gráficos | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 1b9aa3ea-29a0-4e21-bc57-936f33537b5c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 143ae65b8d7db584546c250bf5d032450bf220aa
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31473865"
---
# <a name="how-to-change-the-graphics-diagnostics-playback-machine"></a>Como alterar a máquina de reprodução de diagnóstico de gráficos
Você pode reproduzir informações de gráficos usando seu computador local, ou usando um computador ou dispositivo remoto.  
  
## <a name="choosing-a-playback-machine"></a>Escolhendo uma máquina de reprodução  
 A máquina de reprodução é um computador ou dispositivo que é usado para reproduzir eventos de gráficos de um log de elementos gráficos. Geralmente, o computador local é a opção mais conveniente, mas um problema de processamento não pode reproduzir em um computador que tenha um hardware diferente ou versões de driver da máquina em que ele foi capturado; Quando isso acontece, você pode escolher uma máquina de reprodução remota que melhor reproduza o problema e ainda usar sua máquina de desenvolvimento para diagnóstico.  
  
#### <a name="to-use-the-local-machine-to-play-back-graphics-information"></a>Para usar o computador local para reproduzir informações de gráficos  
  
1.  Na janela do documento de Log de gráficos, escolha o **máquina de reprodução** link. O **conexões remotas do depurador** caixa de diálogo é exibida.  
  
2.  Em **Configuração Manual**, no **endereço** propriedade, digite `localhost`.  
  
3.  Definir o **modo de autenticação** propriedade **nenhum**.  
  
4.  Escolha o **selecione** botão.  
  
#### <a name="to-use-a-remote-machine-to-play-back-graphics-information"></a>Para usar um computador remoto para reproduzir informações de gráficos  
  
1.  Na janela do documento de Log de gráficos, escolha o **máquina de reprodução** link. O **conexões remotas do depurador** caixa de diálogo é exibida.  
  
2.  Em **Configuração Manual**, no **endereço** propriedade, digite o nome de domínio do Windows ou o endereço IP do computador ou dispositivo que você deseja usar para reproduzir informações de gráficos.  
  
3.  Especifique o tipo de autorização que você deseja usar para proteger a conexão para a máquina de reprodução.  
  
    -   Para autenticação do Windows, defina o **modo de autenticação** propriedade **Windows**.  
  
    -   Para sem autenticação, defina o **modo de autenticação** propriedade **nenhum**.  
  
4.  Escolha o **selecione** botão.  
  
> [!NOTE]
>  O **conexões remotas do depurador** caixa de diálogo também pode exibir os destinos de depuração remotos que estão diretamente conectados à sua máquina de desenvolvimento ou que estão na mesma sub-rede. Você pode usar um desses destinos de depuração remotos da máquina de reprodução de diagnóstico de gráficos sem configurá-la manualmente. No **conexões remotas do depurador** caixa de diálogo, selecione o destino desejado e, em seguida, escolha o **selecione** botão.  
  
## <a name="see-also"></a>Consulte também  
 [Documento de log de gráficos](graphics-log-document.md)