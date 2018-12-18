---
title: Criar uma instalação Offline | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- offline installation
- offline install
- ISO
ms.assetid: 85d65709-42be-449f-9663-914bf1045089
caps.latest.revision: 22
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: 0ac8f1c1d631e4d5f682fea5e1841e3914241d14
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53055232"
---
# <a name="create-an-offline-installation-of-visual-studio"></a>Criar uma instalação offline do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [instalar o Visual Studio 2017 em ambientes de rede não confiável ou de baixa largura de banda](https://docs.microsoft.com/visualstudio/install/install-vs-inconsistent-quality-network), ou [criar uma instalação de rede do Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio) e [Considerações especiais para instalar o Visual Studio 2017 em um ambiente offline](https://docs.microsoft.com/visualstudio/install/install-visual-studio-in-offline-environment).

Esta página descreve como instalar o Visual Studio 2015 quando você não está conectado à Internet. No entanto, para executar uma instalação "desconectada", primeiro você deve criar um layout de instalação offline usando um computador que está conectado à Internet. Veja como fazer isso.

> [!IMPORTANT]
>  Se seu computador offline estiver executando o Windows 7 SP1 ou Windows Server 2008 R2, consulte as instruções especiais a [solução de problemas de uma instalação offline](#BKMK_tshoot) seção deste tópico.  Você deve seguir estas instruções *antes de* instalar o Visual Studio 2015.

##  <a name="BKMK_Offline"></a> Instalar com a criação de uma instalação offline

#### <a name="to-create-an-offline-installation-layout"></a>Para criar um layout de instalação offline

1.  Escolha a edição do Visual Studio que você deseja instalar a partir de [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20Enterprise%202015) página de download.

2.  Depois de baixar o instalador para um local no sistema de arquivos, execute "\<nome executável > /layout".

     Por exemplo, execute: `vs_enterprise.exe /layout D:\VisualStudio2015`

     Usando o `/layout` switch, você pode baixar a quase todos os pacotes de instalação, não apenas aqueles que se aplicam ao computador de download. Essa abordagem fornece os arquivos que você precisa executar esse instalador em qualquer lugar e pode ser útil se você quiser instalar os componentes que não foram instalados originalmente.

3.  Depois de executar esse comando, uma caixa de diálogo será exibida que permite que você altere a pasta onde você deseja que o layout de instalação offline deve residir.   Em seguida, clique o **baixar** botão.

     Quando o download do pacote for bem-sucedida, você verá uma mensagem que diz **instalação bem-sucedida! Todos os componentes especificados foram adquiridos com êxito.**

4.  Localize a pasta que você especificou anteriormente. (Por exemplo, localize D:\VisualStudio2015). Esta pasta contém tudo o que você precisa para copiar para um local compartilhado ou a mídia de instalação.

    > [!CAUTION]
    >  Atualmente, o SDK do Android não dá suporte a uma experiência de instalação offline. Se você instalar itens de instalação do SDK do Android em um computador que não está conectado à Internet, a instalação poderá falhar. Para obter mais informações, consulte a seção "Solução de problemas de uma instalação offline" neste tópico.

5.  Execute a instalação do local do arquivo ou da mídia de instalação.

## <a name="updating-an-offline-installation"></a>Atualizando uma instalação offline
 Microsoft lançou várias atualizações para o Visual Studio 2015. Para atualizar sua instalação do Visual Studio, basta baixar a edição desejada da partir o [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20Enterprise%202015) página de download. Em seguida, siga as etapas descritas neste tópico para criar um novo layout de instalação offline e, em seguida, usá-lo para atualizar sua cópia do Visual Studio 2015.

##  <a name="BKMK_tshoot"></a> Solução de problemas de uma instalação offline
 Quando você faz instalação offline de seu cache de instalação offline, você pode ver mensagens de aviso sobre não ser possível instalar alguns componentes e pacotes. A tabela a seguir inclui soluções possíveis para esses cenários.


|                                                                                       Componente ou pacote                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                   Solução                                                                                                                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| O Dotfuscator e Analytics Community Edition 5.19.1 (para as edições Community, Professional e Enterprise do Visual Studio, como instalado em **Windows 7 SP1** e **Windows Server 2008 R2**) |                                                                                                                                       Se o computador offline estiver executando **Windows 7 SP1** ou **Windows Server 2008 R2**, você deve executar as etapas a seguir antes de instalar o Visual Studio 2015:<br /><br /> 1.  Configure um servidor web ou de arquivos para baixar os arquivos da CTL.<br /><br /> 2.    Redirecione a URL de atualização automática da Microsoft para um ambiente desconectado.<br /><br /> Para obter mais informações, consulte o [configurar raízes confiáveis e certificados não permitidos](https://technet.microsoft.com/library/dn265983.aspx) página no site do Microsoft TechNet.                                                                                                                                       |
|                                                                                  Instalação do SDK do Android (nível de API)                                                                                   |                                                                        Você deve ter uma conexão com a Internet para instalar os pacotes de SDK do Android (nível de API). Se você estiver em uma rede restrita, será necessário permitir o acesso às seguintes URLs ao instalar o Visual Studio:<br /><br /> -   http://dl.google.com:443<br />-   http://dl-ssl.google.com:443<br />-   https://dl-ssl.google.com/android/repository/*<br /> <br />Para obter mais informações de como solucionar possíveis problemas coma configurações de proxy, confira a postagem no blog [Visual Studio 2015 install failures (Android SDK Setup) behind a Proxy](https://blogs.msdn.microsoft.com/peterhauge/2016/09/22/visual-studio-2015-install-failures-android-sdk-setup-behind-a-proxy/) (Falhas de instalação do Visual Studio 2015 (instalação do SDK do Android) por trás de um proxy).                                                                         |
|                             Modelos de Item de extensibilidade do Visual Studio<br /><br /> Extensão do GitHub para Visual Studio<br /><br /> PowerShell Tools for Visual Studio                             | Se você não tiver uma conexão de internet quando você instala o Visual Studio 2015, você pode usar um feed offline para gerar o layout de instalação offline de especial. **Observação:**  Este feed especial inclui as atualizações mais recentes para o Visual Studio 2015. <br /><br /> Para criar especiais feed offline, execute o seguinte comando: /layout *unidade:* \VisualStudio2015 /overridefeeduri *URL do feed xml*<br /><br /> Por exemplo, para um idioma inglês especial feed offline do Visual Studio 2015 Enterprise, execute:<br /><br /> `vs_enterprise_ENU.exe /layout D:\VisualStudio2015 /overridefeeduri "http://go.microsoft.com/fwlink/?LinkID=785882&clcid0x409"`<br /><br /> Para obter uma lista completa de URLs que você pode usar para criar um feed offline de especial no idioma de sua escolha, consulte a tabela a seguir. |

 Use as URLs a seguir para criar um feed offline especial de idioma específico, conforme descrito na tabela acima.


|       Idioma        |                            URL                            |
|-----------------------|-----------------------------------------------------------|
| Chinês (simplificado)  | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x804 |
| Chinês (tradicional) | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x404 |
|         Tcheco         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x405 |
|        Alemão         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x407 |
|        Inglês        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x409 |
|        Espanhol        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0xC0A |
|        Francês         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x40C |
|        Italiano        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x410 |
|       Japonês        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x411 |
|        Coreano         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x412 |
|        Polonês         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x415 |
|      Português       | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x416 |
|        Russo        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x419 |
|        Turco        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x41F |

## <a name="see-also"></a>Consulte também
 [Instalar o Visual Studio]()