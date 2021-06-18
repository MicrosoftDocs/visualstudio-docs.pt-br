---
title: Instalar certificados para uma instalação offline
description: Saiba como instalar certificados para instalação offline do Visual Studio.
ms.date: 03/29/2021
ms.custom: seodec18, SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 9750A3F3-89C7-4A8F-BA75-B0B06BD772C2
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 6dc4137157e2fa5136a0b8c86c5cf72f284a9eb7
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307370"
---
# <a name="install-certificates-required-for-visual-studio-offline-installation"></a>Instalar os certificados necessários para instalação offline do Visual Studio

O Visual Studio é projetado principalmente para instalação em um computador conectado à Internet, pois muitos componentes são atualizados regularmente. No entanto, com algumas etapas adicionais, é possível implantar o Visual Studio em um ambiente em que uma conexão com a Internet operacional não está disponível.

O mecanismo de instalação do Visual Studio instalará apenas conteúdo confiável. Ele faz isso ao conferir as assinaturas Authenticode do conteúdo que está sendo baixado e verificar se todo o conteúdo é confiável antes de instalá-lo. Isso mantém seu ambiente seguro contra ataques nos quais o local de download está comprometido. Portanto, a instalação do Visual Studio requer que vários certificados raiz e intermediários padrão da Microsoft sejam instalados e atualizados no computador de um usuário. Se o computador foi mantido atualizado com o Windows Update, os certificados de autenticação geralmente estão atualizados. Se o computador está conectado à Internet, durante a instalação, o Visual Studio poderá atualizar os certificados, conforme o necessário para verificar as assinaturas de arquivo. Se o computador estiver offline, os certificados deverão ser atualizados de outra maneira.

## <a name="how-to-refresh-certificates-when-offline"></a>Como atualizar certificados quando estiver offline

Há três opções para instalar ou atualizar certificados em um ambiente offline.

### <a name="option-1---manually-install-certificates-from-a-layout-folder"></a>Opção 1 – Instalar manualmente os certificados de uma pasta de layout

::: moniker range="vs-2017"

Quando você cria um [layout de rede](../install/create-a-network-installation-of-visual-studio.md) ou um [cache offline local](../install/create-an-offline-installation-of-visual-studio.md), os certificados necessários são baixados na pasta certificados. Depois, você pode instalar manualmente os certificados clicando duas vezes em cada um dos arquivos de certificado e clicando no assistente Gerenciador de Certificados. Se for solicitado a fornecer uma senha, deixe-a em branco.

**Atualização**: no caso do Visual Studio 2017 versão 15.8 versão prévia 2 ou posterior, é possível instalar manualmente os certificados; para isso, basta clicar com o botão direito do mouse em cada um dos arquivos de certificado, selecionar Instalar Certificado e clicar no assistente do Gerenciador de Certificados.

::: moniker-end

::: moniker range=">=vs-2019"

Quando você cria um [layout de rede](../install/create-a-network-installation-of-visual-studio.md) ou um [cache offline local](../install/create-an-offline-installation-of-visual-studio.md), os certificados necessários são baixados na pasta certificados. É possível instalar os certificados manualmente clicando com o botão direito do mouse em cada um dos arquivos de certificado, selecionando Instalar Certificado e, em seguida, clicando no assistente do Gerenciador de Certificados. Se for solicitado a fornecer uma senha, deixe-a em branco.

::: moniker-end

### <a name="option-2---distribute-trusted-root-certificates-in-an-enterprise-environment"></a>Opção 2 – Distribuir certificados raiz confiáveis em um ambiente empresarial

Para empresas com computadores offline sem os certificados raiz mais recentes, um administrador poderá usar as instruções na página [Configurar raízes confiáveis e certificados não permitidos](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265983(v=ws.11)) para atualizá-los.

### <a name="option-3---install-certificates-as-part-of-a-scripted-deployment-of-visual-studio"></a>Opção 3 – Instalar certificados como parte de um script de implantação do Visual Studio

Se estiver usando o script de implantação do Visual Studio em um ambiente offline para estações de trabalho cliente, você deverá seguir estas etapas:

1. Copie a [ferramenta Gerenciador de certificados](/dotnet/framework/tools/certmgr-exe-certificate-manager-tool) (certmgr.exe) para o local de instalação do cache local ou do layout de rede. Certmgr.exe não está incluído como parte do Windows em si, mas está disponível como parte do [SDK do Windows](https://developer.microsoft.com/windows/downloads/windows-10-sdk).

2. Crie um arquivo em lotes com os seguintes comandos:

   ```shell
   certmgr.exe -add [layout path]\certificates\manifestRootCertificate.cer -n "Microsoft Root Certificate Authority 2011" -s -r LocalMachine root

   certmgr.exe -add [layout path]\certificates\manifestCounterSignRootCertificate.cer -n "Microsoft Root Certificate Authority 2010" -s -r LocalMachine root

   certmgr.exe -add [layout path]\certificates\vs_installer_opc.RootCertificate.cer -n "Microsoft Root Certificate Authority 2010" -s -r LocalMachine root
   ```
   
   Como alternativa, crie um arquivo em lotes que usa certutil.exe, que é fornecido com o Windows, com os seguintes comandos:
   
      ```shell
   certutil.exe -addstore -f "Root" "[layout path]\certificates\manifestRootCertificate.cer"

   certutil.exe -addstore -f "Root" "[layout path]\certificates\manifestCounterSignRootCertificate.cer"

   certutil.exe -addstore -f "Root" "[layout path]\certificates\vs_installer_opc.RootCertificate.cer"
   ```

3. Implante o arquivo em lotes para o cliente. Este comando deve ser executado de um processo elevado.

## <a name="what-are-the-certificates-files-in-the-certificates-folder"></a>Quais são os arquivos de certificados na pasta Certificados?

* **manifestRootCertificate. cer** contém:
  * Certificado raiz: **Autoridade de Certificação Raiz da Microsoft 2011**
* **manifestCounterSignRootCertificate. cer** e **vs_installer_opc. RootCertificate. cer** contém:
  * Certificado raiz: **Autoridade de Certificação Raiz da Microsoft 2010**
 
O Instalador do Visual Studio exige apenas a instalação dos certificados raiz no sistema. Todos esses certificados são necessários para os sistemas do Windows 7 Service Pack 1 que não têm as atualizações mais recentes do Windows instaladas.

## <a name="why-are-the-certificates-from-the-certificates-folder-not-installed-automatically"></a>Por que os certificados da pasta Certificados não são instalados automaticamente?

Quando uma assinatura é verificada em um ambiente online, as APIs do Windows são usadas para baixar e adicionar os certificados no sistema. A verificação de que o certificado é confiável e permitido por meio de configurações administrativas ocorre durante esse processo. Esse processo de verificação não pode ocorrer na maioria dos ambientes offline. Instalar certificados manualmente permite aos administradores de empresa garantir que eles sejam confiáveis e atendam à política de segurança de suas organizações.

## <a name="checking-if-certificates-are-already-installed"></a>Verificando se os certificados já estão instalados

Uma maneira de verificar no sistema de instalação é seguir estas etapas:

1. Execute **mmc.exe**.<br/>
  a. Clique em **Arquivo** e selecione **Adicionar/Remover Snap-in**.<br/>
  b. Clique duas vezes em **Certificados**, selecione **Conta do computador** e clique em **Avançar**.<br/>
  c. Selecione **Computador local**, clique em **Concluir** e depois em **OK**.<br/>
  d. Expanda **Certificados (Computador Local)**.<br/>
  e. Expanda **Autoridades de Certificação Confiáveis** e selecione **Certificados**.<br/>
    * Verifique os certificados raiz necessários para esta lista.<br/>

   f. Expanda **Autoridades de Certificação Intermediárias** e selecione **Certificados**.<br/>
    * Verifique os certificados intermediários necessários desta lista.<br/>

2. Clique em **Arquivo** e selecione **Adicionar/Remover Snap-in**.<br/>
  a. Clique duas vezes em **Certificados**, selecione **Minha conta de usuário**, clique em **Concluir** e em **OK**.<br/>
  b. Expandir **certificados – usuário atual**.<br/>
  c. Expanda **Autoridades de Certificação Intermediárias** e selecione **Certificados**.<br/>
    * Verifique os certificados intermediários necessários desta lista.<br/>

Se os nomes dos certificados não estiverem na coluna **Emitido Para**, eles terão que ser instalados.  Se um certificado intermediário estiver apenas no repositório de certificados intermediários do **Usuário Atual**, ele só estará disponível para o usuário que estiver conectado. Talvez ele precise ser instalado para outros usuários.

## <a name="install-visual-studio"></a>Instalar o Visual Studio

Depois de instalar os certificados no computador cliente, você estará pronto para instalar o [Visual Studio do cache local](../install/create-an-offline-installation-of-visual-studio.md#step-3---install-visual-studio-from-the-local-cache)ou [implantar o Visual Studio por meio do compartilhamento de layout de rede](create-a-network-installation-of-visual-studio.md#deploy-from-a-network-installation) no computador cliente.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Criar uma instalação de rede do Visual Studio](../install/create-a-network-installation-of-visual-studio.md)
* [Criar uma instalação offline do Visual Studio](../install/create-an-offline-installation-of-visual-studio.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)

