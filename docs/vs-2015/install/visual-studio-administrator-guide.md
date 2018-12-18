---
title: Guia do administrador do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
caps.latest.revision: 76
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: 25d6655969245adf1b2a28df2b3327561d149983
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722814"
---
# <a name="visual-studio-administrator-guide"></a>Guia do Administrador do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte o [guia do administrador do Visual Studio 2017](/visualstudio/install/visual-studio-administrator-guide).

Você pode implantar o Visual Studio 2015 em uma rede desde que cada computador de destino atende o [requisitos mínimos de instalação](http://www.microsoft.com/visualstudio/eng/products/2013-editions). Você pode criar um compartilhamento de rede, executando o arquivo de instalação com o argumento /layout (conforme descrito na [criar uma instalação Offline do Visual Studio](../install/create-an-offline-installation-of-visual-studio.md) página) e, em seguida, copiá-lo do computador local para o compartilhamento de rede. Se você estiver usando um arquivo ISO, você pode montar o ISO e compartilhá-lo ou copiar o ISO em um compartilhamento de rede.  
  
 Observe que as instalações de um compartilhamento de rede "lembrar" local de origem que de onde vieram. Isso significa que um reparo de um computador cliente pode ter que retornar para o compartilhamento de rede do qual o cliente foi instalado originalmente. Escolha seu local de rede com cuidado para que ele se alinhe com o tempo de vida que você espera que os clientes do Visual Studio 2015 em execução em sua organização.  
  
## <a name="detection-and-servicing-keys"></a>Chaves de detecção e de serviço  
 Você pode usar subchaves de detecção no registro para determinar se um produto do Visual Studio já está instalado em um computador. Você usaria essas chaves de detecção para determinar se ele foi necessário para continuar com uma instalação em uma implantação automatizada.  Ver [detectar os requisitos de sistema](../extensibility/internals/detecting-system-requirements.md)[requisitos do sistema de detecção].  
  
## <a name="avoiding-reboots"></a>Evitando reinicializações  
 Você pode reduzir as reinicializações, certificando-se de que você atender aos pré-requisitos apropriados do Visual Studio antes de implantar o Visual Studio. Para o .NET Framework, você talvez precise reinicializar computadores que executam o Windows 8 se você implantar o Visual Studio 2015 neles sem instalar primeiro o .NET Framework 4.6.  
  
 Para a emulação de dispositivo do Windows e Android, você talvez precise reinicializar computadores, se você ainda não tiver recursos do Windows que Hyper-V ativado. Para o desenvolvimento da Web, você talvez precise reinicializar computadores, se você ainda não tiver o recurso de Windows no que servidor Web ativado. Para o desenvolvimento do Office, você talvez precise reinicializar computadores, se você ainda não tiver recursos do Windows que Foundation identificar do Windows é ativado. Reinicialize computadores, se você ainda não tiver o recurso de Windows no que servidor Web ativado. Para o desenvolvimento do Office, você talvez precise reinicializar computadores, se você ainda não tiver recursos do Windows que Foundation identificar do Windows é ativado. Para saber mais sobre como automatizar a detecção e instalação dos recursos do Windows, consulte [instalando uma função de servidor em um servidor que executa uma instalação Server Core do Windows Server 2008 R2](https://technet.microsoft.com/library/ee441260(v=ws.10).aspx).  
  
## <a name="error-return-codes"></a>Códigos de Retorno de Erro  
 A tabela a seguir lista os códigos de erro importantes. Você pode usar esses códigos de erro na sua automação para decidir se uma reinicialização é necessária e se a instalação foi bem-sucedida. Se você receber um código de erro, considere as etapas de solução de problemas sobre o [instalar o Visual Studio](../install/install-visual-studio-2015.md) página.  
  
|Status da instalação|Reinicialização não necessária|Reinicialização necessária|Descrição|  
|------------------|--------------------------|----------------------|-----------------|  
|Êxito|0x00000000 [0]|0x00000bc2 [3010]|Instalação bem-sucedida.|  
|Bloco|0x80044000 [-2147205120]|0x8004C000 [-2147172352]|Se o único bloco a ser relatado for "Reinicialização Pendente", o valor retornado será o valor Reinicialização Incompleta Necessária (0x80048bc7).|  
|Cancelar|0x00000642 [1602]|0x80048642 [-2147187134]|Quando o valor de reinicialização é retornado, o código de retorno é 1602.|  
|Reinicialização incompleta necessária|N/D|0x80048bc7 [-2147185721]|A reinicialização é necessária antes de continuar a instalação.|  
|Falha|0x00000643 [1603]|0x80048643 [-2147187133]|Quando o valor de reinicialização é retornado, o código de retorno é 1603.|  
  
## <a name="interactive-administrator-installer"></a>Instalador de administrador interativo  
 Se você estiver criando um instalador interativo sobre a instalação do Visual Studio, você pode exibir o progresso do instalador do Visual Studio. O Visual Studio 2015 instalador baseia-se no software livre de tecnologia de encadeador do Windows Installer XML (WiX), também conhecido como "a gravação." A tecnologia de gravação dá suporte a dois protocolos de comunicação: netfx4 e gravar em. Para obter uma referência em breve, consulte a descrição do atributo na documentação para o elemento ExePackage no protocolo [wixtoolset.org](http://wixtoolset.org/). Uma revisão da implementação de código-fonte aberto do WiX desse atributo do protocolo pode ser necessária para integração.  
  
## <a name="controlling-what-is-installed"></a>Controlar o que está instalado  
 Se você deseja controlar o que o usuário final pode instalar, há duas opções: o administrador do arquivo de instalação e as opções de linha de comando. Se seu objetivo é restringir o que o usuário final pode escolher entre sua experiência de instalador do Visual Studio, selecione a instalação do arquivo de administrador. Se você quiser criar uma configuração inicial, mas permitir que seu usuário final escolher sua própria experiência de instalador do Visual Studio, selecione os parâmetros de linha de comando.  
  
 Para obter mais informações sobre a experiência de administrador de arquivos, consulte [como: criar e executar uma autônoma instalação do Visual Studio](../install/how-to-create-and-run-an-unattended-installation-of-visual-studio.md) e [como: aplicar as chaves de produto durante a implantação do Visual Studio](../install/how-to-automatically-apply-product-keys-when-deploying-visual-studio.md).  Para obter mais informações sobre os controles de linha de comando, consulte o [Use parâmetros de linha de comando para instalar o Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md) página.  
  
## <a name="specifying-customer-feedback-settings"></a>Especificar as configurações de comentários do cliente  
 Por padrão, a instalação do Visual Studio habilita os comentários do cliente. Você pode configurar o Visual Studio para desabilitar os comentários do cliente em computadores individuais, alterando o valor da chave do registro para a cadeia de caracteres "0":  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SQM**  
**OptIn**  
  
 (Por exemplo, alterá-lo para HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SQM OptIn = "0")  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Como instalar uma versão específica do Visual Studio](../install/how-to-install-a-specific-release-of-visual-studio.md)|Descreve como instalar configurações específicas da versão atual do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|  
|[Como criar e executar uma instalação autônoma do Visual Studio](../install/how-to-create-and-run-an-unattended-installation-of-visual-studio.md)|Descreve como instalar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no modo autônomo.|  
|[Como aplicar as chaves de produto automaticamente durante a implantação do Visual Studio](../install/how-to-automatically-apply-product-keys-when-deploying-visual-studio.md)|Descreve como aplicar chaves de produto durante a implantação em vários computadores.|  
|[Guia do administrador do Help Viewer](../ide/help-viewer-administrator-guide.md)|Fornece informações sobre como gerenciar as instalações da Ajuda local para ambientes de rede que têm ou não tem acesso à internet.|  
|[Instalar o Visual Studio](../install/install-visual-studio-2015.md)|Fornece instruções e links para tópicos que descrevem como instalar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|