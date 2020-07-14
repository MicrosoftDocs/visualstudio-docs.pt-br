---
title: Como assinar novamente os manifestos de aplicativo e implantação | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1905ea32a9899a1262e146f264e0a1179f0e8c6e
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382192"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>Como assinar manifestos de aplicativo e implantação novamente
Depois de fazer alterações nas propriedades de implantação no manifesto do aplicativo para Windows Forms aplicativos, XBAP (aplicativos Windows Presentation Foundation) ou soluções do Office, você deve assinar novamente os manifestos de aplicativo e de implantação com um certificado. Esse processo ajuda a garantir que arquivos violados não sejam instalados nos computadores dos usuários finais.

 Outro cenário em que você pode assinar novamente os manifestos é quando seus clientes desejam assinar o aplicativo e os manifestos de implantação com seu próprio certificado.

## <a name="re-sign-the-application-and-deployment-manifests"></a>Assinar novamente os manifestos de aplicativo e de implantação
 Este procedimento pressupõe que você já fez alterações no arquivo de manifesto do aplicativo (*. manifest*). Para obter mais informações, consulte [como alterar propriedades de implantação](https://msdn.microsoft.com/library/66052a3a-8127-4964-8147-2477ef5d1472).

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Para assinar novamente o aplicativo e os manifestos de implantação com o Mage.exe

1. Abra uma janela de **prompt de comando do Visual Studio** .

2. Altere os diretórios para a pasta que contém os arquivos de manifesto que você deseja assinar.

3. Digite o comando a seguir para assinar o arquivo de manifesto do aplicativo. Substitua *ManifestFileName* pelo nome do seu arquivo de manifesto mais a extensão. Substitua o *certificado* pelo caminho relativo ou totalmente qualificado do arquivo de certificado e substitua a *senha* pelo certificado.

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     Por exemplo, você pode executar o comando a seguir para assinar um manifesto de aplicativo para um suplemento, um aplicativo do Windows Form ou um aplicativo de navegador Windows Presentation Foundation. Certificados temporários criados pelo Visual Studio não são recomendados para implantação em ambientes de produção.

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. Digite o seguinte comando para atualizar e assinar o arquivo de manifesto de implantação, substituindo os nomes de espaço reservado como na etapa anterior.

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     Por exemplo, você pode executar o seguinte comando para atualizar e assinar um manifesto de implantação para um suplemento do Excel, um aplicativo Windows Forms ou um aplicativo de navegador Windows Presentation Foundation.

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. Opcionalmente, copie o manifesto de implantação mestre (*Publish \\ \<appname> . Application*) para seu diretório de implantação de versão (*publish\Application files \\ \<appname> _ \<version> *).

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>Atualizar e assinar novamente os manifestos de aplicativo e implantação
 Este procedimento pressupõe que você já fez alterações no arquivo de manifesto do aplicativo (*. manifest*), mas que há outros arquivos que foram atualizados. Quando os arquivos são atualizados, o hash que representa o arquivo também deve ser atualizado.

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Para atualizar e assinar novamente o aplicativo e os manifestos de implantação com o Mage.exe

1. Abra uma janela de **prompt de comando do Visual Studio** .

2. Altere os diretórios para a pasta que contém os arquivos de manifesto que você deseja assinar.

3. Remova a extensão de arquivo *. Deploy* dos arquivos na pasta de saída de publicação.

4. Digite o seguinte comando para atualizar o manifesto do aplicativo com os novos hashes para os arquivos atualizados e assinar o arquivo de manifesto do aplicativo. Substitua *ManifestFileName* pelo nome do seu arquivo de manifesto mais a extensão. Substitua o *certificado* pelo caminho relativo ou totalmente qualificado do arquivo de certificado e substitua a *senha* pelo certificado.

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     Por exemplo, você pode executar o comando a seguir para assinar um manifesto de aplicativo para um suplemento, um aplicativo do Windows Form ou um aplicativo de navegador Windows Presentation Foundation. Certificados temporários criados pelo Visual Studio não são recomendados para implantação em ambientes de produção.

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. Digite o seguinte comando para atualizar e assinar o arquivo de manifesto de implantação, substituindo os nomes de espaço reservado como na etapa anterior.

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     Por exemplo, você pode executar o seguinte comando para atualizar e assinar um manifesto de implantação para um suplemento do Excel, um aplicativo Windows Forms ou um aplicativo de navegador Windows Presentation Foundation.

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. Adicione a extensão de arquivo *. Deploy* de volta aos arquivos, exceto os arquivos de manifesto de implantação e de aplicativo.

7. Opcionalmente, copie o manifesto de implantação mestre (*Publish \\ \<appname> . Application*) para seu diretório de implantação de versão (*publish\Application files \\ \<appname> _ \<version> *).

## <a name="see-also"></a>Veja também
- [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)
- [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md)
- [Visão geral da implantação de aplicativos confiáveis](../deployment/trusted-application-deployment-overview.md)
- [Como habilitar as configurações de segurança do ClickOnce](../deployment/how-to-enable-clickonce-security-settings.md)
- [Como definir uma zona de segurança em um aplicativo ClickOnce](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [Como definir permissões personalizadas em um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [Como depurar um aplicativo ClickOnce com permissões restritas](securing-clickonce-applications.md)
- [Como adicionar um fornecedor confiável a um computador cliente em aplicativos ClickOnce](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [Como configurar o comportamento do prompt confiável do ClickOnce](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)