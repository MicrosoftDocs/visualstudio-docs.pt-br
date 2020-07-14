---
title: Usar o ClickOnce para implantar aplicativos de multidirecionamento
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, multiple .NET Framework versions
- ClickOnce deployment, multiple .NET Framework versions
- deploying applications [ClickOnce], multiple .NET Framework versions
ms.assetid: e0a8c330-21bc-4eb2-b936-fd0f3c3221f1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 7ede1cb4faa437d9cff8bd1239f9c271112ccf72
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381698"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>Como usar o ClickOnce para implantar aplicativos que podem ser executados em várias versões do .NET Framework
Você pode implantar um aplicativo que tem como alvo várias versões do .NET Framework usando a tecnologia de implantação do ClickOnce. Isso requer que você gere e atualize os manifestos de implantação e de aplicativo.

> [!NOTE]
> Antes de alterar o aplicativo para direcionar várias versões do .NET Framework, você deve garantir que seu aplicativo seja executado com várias versões do .NET Framework. A versão Common Language Runtime é diferente entre .NET Framework 4 versus .NET Framework 2,0, .NET Framework 3,0 e .NET Framework 3,5.

 Esse processo exige as seguintes etapas:

1. Gere o aplicativo e os manifestos de implantação.

2. Altere o manifesto de implantação para listar as várias versões de .NET Framework.

3. Altere o arquivo de *app.config* para listar as versões de tempo de execução .NET Framework compatíveis.

4. Altere o manifesto do aplicativo para marcar assemblies dependentes como .NET Framework assemblies.

5. Assinar o manifesto do aplicativo.

6. Atualize e assine o manifesto de implantação.

### <a name="to-generate-the-application-and-deployment-manifests"></a>Para gerar os manifestos de aplicativo e implantação

- Use o assistente de publicação ou a página publicar do designer de projeto para publicar o aplicativo e gerar os arquivos de manifesto de aplicativo e implantação. Para obter mais informações, consulte [como publicar um aplicativo ClickOnce usando o assistente de publicação ou a](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md) [página publicar, designer de projeto](../ide/reference/publish-page-project-designer.md).

### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>Para alterar o manifesto de implantação para listar as várias versões de .NET Framework

1. No diretório de publicação, abra o manifesto de implantação usando o editor de XML no Visual Studio. O manifesto de implantação tem a extensão de nome de arquivo *. Application* .

2. Substitua o código XML entre os `<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">` `</compatibleFrameworks>` elementos e com XML que lista as versões de .NET Framework com suporte para seu aplicativo.

     A tabela a seguir mostra algumas das versões .NET Framework disponíveis e o XML correspondente que você pode adicionar ao manifesto de implantação.

    |Versão do .NET Framework|XML|
    |----------------------------|---------|
    |4 Client|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|
    |4 Full|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|
    |3.5 Client|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|
    |3.5 Full|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|

### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>Para alterar o arquivo de app.config para listar as versões compatíveis do .NET Framework Runtime

1. No Gerenciador de Soluções, abra o arquivo de *app.config* usando o editor de XML no Visual Studio.

2. Substitua (ou adicione) o código XML entre os `<startup>` `</startup>` elementos e com XML que lista os tempos de execução de .NET Framework com suporte para seu aplicativo.

     A tabela a seguir mostra algumas das versões .NET Framework disponíveis e o XML correspondente que você pode adicionar ao manifesto de implantação.

    |.NET Framework versão do tempo de execução|XML|
    |------------------------------------|---------|
    |4 Client|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|
    |4 Full|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|
    |3.5 Full|\<supportedRuntime version="v2.0.50727"/>|
    |3.5 Client|\<supportedRuntime version="v2.0.50727" sku="Client"/>|

### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>Para alterar o manifesto do aplicativo para marcar assemblies dependentes como .NET Framework assemblies

1. No diretório de publicação, abra o manifesto do aplicativo usando o editor de XML no Visual Studio. O manifesto de implantação tem a extensão de nome de arquivo *. manifest* .

2. Adicione `group="framework"` ao XML de dependência para os assemblies do Sentinel ( `System.Core` , `WindowsBase` , `Sentinel.v3.5Client` e `System.Data.Entity` ). Por exemplo, o XML deve ser semelhante ao seguinte:

   ```xml
   <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">
   ```

3. Atualize o número de versão do `<assemblyIdentity>` elemento para Microsoft. Windows. CommonLanguageRuntime para o número de versão do .NET Framework que é o denominador comum mais baixo. Por exemplo, se o aplicativo tiver como destino .NET Framework 3,5 e .NET Framework 4, use o número de versão 2.0.50727.0 e o XML deverá ser semelhante ao seguinte:

   ```xml
   <dependency>
     <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
       <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />
     </dependentAssembly>
   </dependency>
   ```

### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>Para atualizar e assinar novamente o aplicativo e os manifestos de implantação

- Atualize e assine novamente os manifestos de aplicativo e implantação. Para obter mais informações, consulte [como: assinar novamente manifestos de aplicativo e implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md).

## <a name="see-also"></a>Veja também
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [\<compatibleFrameworks>elementos](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [\<dependency>elementos](../deployment/dependency-element-clickonce-application.md)
- [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)
- [Esquema do arquivo de configuração](/dotnet/framework/configure-apps/file-schema/index)
