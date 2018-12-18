---
title: 'Como: assinar novamente os manifestos de aplicativo e implantação | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Office applications, signing manifests
- deploying applications [ClickOnce], signing manifests
- deploying applications, signing manifests
- ClickOnce deployment, signing manifests
- Office development in Visual Studio, signing manifests
ms.assetid: d53bceb9-4d3b-4c22-b909-8f370e7231fb
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 734258871e72e6272abcd61c4efa1a00765f8a32
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49185712"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>Como assinar manifestos de aplicativo e implantação novamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depois de fazer alterações às propriedades de implantação no manifesto do aplicativo para aplicativos do Windows Forms, aplicativos do Windows Presentation Foundation (xbap) ou soluções do Office, você deve reassinar o aplicativo e manifestos de implantação com um certificado. Esse processo ajuda a garantir que arquivos violados não sejam instalados nos computadores dos usuários finais.  
  
 Outro cenário em que você pode assinar novamente os manifestos é quando desejam que seus clientes assinar o aplicativo e manifestos de implantação com seu próprio certificado.  
  
## <a name="re-signing-the-application-and-deployment-manifests"></a>Manifestos de assinar novamente o aplicativo e implantação  
 Este procedimento pressupõe que você já tem algumas alterações ao arquivo de manifesto de aplicativo (. manifest). Para obter mais informações, consulte [como: alterar as propriedades de implantação](http://msdn.microsoft.com/en-us/66052a3a-8127-4964-8147-2477ef5d1472).  
  
#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Para assinar novamente o aplicativo e a implantação de manifestos com Mage.exe  
  
1.  Abra uma **Prompt de comando do Visual Studio** janela.  
  
2.  Altere os diretórios para a pasta que contém os arquivos de manifesto que você deseja assinar.  
  
3.  Digite o seguinte comando para assinar o arquivo de manifesto do aplicativo. Substitua ManifestFileName com o nome do arquivo de manifesto e a extensão. Substitua o certificado com o caminho totalmente qualificado ou relativo do arquivo de certificado e senha com a senha do certificado.  
  
    ```  
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password  
    ```  
  
     Por exemplo, você pode executar o comando a seguir para assinar um manifesto de aplicativo para um suplemento, um aplicativo de formulário do Windows ou um aplicativo de navegador do Windows Presentation Foundation. Certificados temporários criados pelo Visual Studio não são recomendados para implantação em ambientes de produção.  
  
    ```  
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
4.  Digite o seguinte comando para atualizar e assinar o arquivo de manifesto de implantação, substituindo os nomes de espaço reservado como na etapa anterior.  
  
    ```  
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password  
    ```  
  
     Por exemplo, você pode executar o comando a seguir para atualizar e assinar um manifesto de implantação para um suplemento do Excel, um aplicativo do Windows Forms ou um aplicativo de navegador do Windows Presentation Foundation.  
  
    ```  
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
5.  Como opção, copie o manifesto de implantação mestre (publique\\*appname*. Application) para seu diretório de implantação da versão (arquivos publish\Application\\*appname*_ *versão*).  
  
## <a name="updating-and-re-signing-the-application-and-deployment-manifests"></a>Atualizando e assinar novamente o aplicativo e manifestos de implantação  
 Este procedimento pressupõe que você já fez alterações no seu aplicativo (. manifest) do arquivo de manifesto, mas que há outros arquivos que foram atualizados. Quando arquivos são atualizados, o hash que representa o arquivo também deve ser atualizado.  
  
#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Para atualizar e assinar novamente o aplicativo e a implantação de manifestos com Mage.exe  
  
1.  Abra uma **Prompt de comando do Visual Studio** janela.  
  
2.  Altere os diretórios para a pasta que contém os arquivos de manifesto que você deseja assinar.  
  
3.  Remova a extensão de arquivo. Deploy dos arquivos na pasta de saída de publicação.  
  
4.  Digite o seguinte comando para atualizar o manifesto do aplicativo com os hashes de novo para os arquivos atualizados e assinar o arquivo de manifesto do aplicativo. Substitua ManifestFileName com o nome do arquivo de manifesto e a extensão. Substitua o certificado com o caminho totalmente qualificado ou relativo do arquivo de certificado e senha com a senha do certificado.  
  
    ```  
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password  
    ```  
  
     Por exemplo, você pode executar o comando a seguir para assinar um manifesto de aplicativo para um suplemento, um aplicativo de formulário do Windows ou um aplicativo de navegador do Windows Presentation Foundation. Certificados temporários criados pelo Visual Studio não são recomendados para implantação em ambientes de produção.  
  
    ```  
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
5.  Digite o seguinte comando para atualizar e assinar o arquivo de manifesto de implantação, substituindo os nomes de espaço reservado como na etapa anterior.  
  
    ```  
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password  
    ```  
  
     Por exemplo, você pode executar o comando a seguir para atualizar e assinar um manifesto de implantação para um suplemento do Excel, um aplicativo do Windows Forms ou um aplicativo de navegador do Windows Presentation Foundation.  
  
    ```  
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
6.  Adicione a extensão de arquivo. Deploy volta para os arquivos, exceto os arquivos de manifesto de aplicativo e implantação.  
  
7.  Como opção, copie o manifesto de implantação mestre (publique\\*appname*. Application) para seu diretório de implantação da versão (arquivos publish\Application\\*appname*_ *versão*).  
  
## <a name="see-also"></a>Consulte também  
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)   
 [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md)   
 [Visão geral da implantação de aplicativos confiáveis](../deployment/trusted-application-deployment-overview.md)   
 [Como habilitar configurações de segurança do ClickOnce](../deployment/how-to-enable-clickonce-security-settings.md)   
 [Como definir uma zona de segurança para um aplicativo ClickOnce](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)   
 [Como definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [Como depurar um aplicativo ClickOnce com permissões restritas](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [Como: adicionar um fornecedor confiável a um computador cliente para aplicativos ClickOnce](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)   
 [Como configurar o comportamento do prompt confiável do ClickOnce](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)



