---
title: Usar o ClickOnce para implantar aplicativos multitarget
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: de3ca40696549ad9208ffd181f8dbc4e7f092b5d
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263197"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>Como: Usar o ClickOnce para implantar aplicativos que podem ser executados em várias versões do .NET Framework
Você pode implantar um aplicativo destinado a várias versões do .NET Framework usando a tecnologia de implantação do ClickOnce. Isso exige que você deseja gerar e atualizar os manifestos do aplicativo e implantação.

> [!NOTE]
> Antes de alterar o aplicativo para direcionar a várias versões do .NET Framework, você deve garantir que seu aplicativo é executado com várias versões do .NET Framework. O versão common language runtime é diferente entre [!INCLUDE[net_v40_short](../code-quality/includes/net_v40_short_md.md)] em comparação com o .NET Framework 2.0, .NET Framework 3.0 e 3.5 do .NET Framework.

 Esse processo exige as seguintes etapas:

1. Gere os manifestos de aplicativo e implantação.

2. Altere o manifesto de implantação para listar as várias versões do .NET Framework.

3. Alterar o *App. config* arquivo para listar as versões compatíveis do tempo de execução do .NET Framework.

4. Altere o manifesto do aplicativo para marcar os assemblies dependentes como assemblies do .NET Framework.

5. Assine o manifesto do aplicativo.

6. Atualizar e assinar o manifesto de implantação.

### <a name="to-generate-the-application-and-deployment-manifests"></a>Para gerar os manifestos de aplicativo e implantação

- Use o Assistente de publicação ou a página de publicação do Project Designer para publicar o aplicativo e gerar o aplicativo e os arquivos de manifesto de implantação. Para obter mais informações, confira [Como: Publicar um aplicativo ClickOnce usando o Assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md) ou [página de publicação, Designer de projeto](../ide/reference/publish-page-project-designer.md).

### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>Para alterar o manifesto de implantação para listar as várias versões do .NET Framework

1. No diretório de publicação, abra o manifesto de implantação usando o Editor de XML no Visual Studio. O manifesto de implantação tem a *. Application* extensão de nome de arquivo.

2. Substitua o código XML entre o `<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">` e `</compatibleFrameworks>` elementos com XML que lista as versões do .NET Framework com suporte para o seu aplicativo.

     A tabela a seguir mostra algumas das versões do .NET Framework disponíveis e o XML correspondente que você pode adicionar ao manifesto de implantação.

    |Versão do .NET Framework|XML|
    |----------------------------|---------|
    |4 Client|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|
    |4 Full|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|
    |3.5 Client|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|
    |3.5 Full|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|

### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>Para alterar o arquivo App. config para listar as versões de tempo de execução do .NET Framework compatíveis

1. No Gerenciador de soluções, abra o *App. config* arquivo usando o Editor de XML no Visual Studio.

2. Substituir (ou adicione) o código XML entre o `<startup>` e `</startup>` elementos com XML que lista os tempos de execução do .NET Framework com suporte para o seu aplicativo.

     A tabela a seguir mostra algumas das versões do .NET Framework disponíveis e o XML correspondente que você pode adicionar ao manifesto de implantação.

    |Versão de tempo de execução do .NET framework|XML|
    |------------------------------------|---------|
    |4 Client|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|
    |4 Full|\<versão de supportedRuntime = sku de "v4.0.30319" = ". NETFramework, versão = v4.0 "/ >|
    |3.5 Full|\<supportedRuntime version="v2.0.50727"/>|
    |3.5 Client|\<supportedRuntime version="v2.0.50727" sku="Client"/>|

### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>Para alterar o manifesto do aplicativo para marcar os assemblies dependentes como assemblies do .NET Framework

1. No diretório de publicação, abra o manifesto do aplicativo usando o Editor de XML no Visual Studio. O manifesto de implantação tem a *. manifest* extensão de nome de arquivo.

2. Adicione `group="framework"` para a dependência de XML para os assemblies de sentinela (`System.Core`, `WindowsBase`, `Sentinel.v3.5Client`, e `System.Data.Entity`). Por exemplo, o XML deve ser semelhante ao seguinte:

   ```xml
   <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">
   ```

3. Atualizar o número de versão a `<assemblyIdentity>` elemento para Microsoft.Windows.CommonLanguageRuntime ao número de versão para o .NET Framework que é o menor denominador comum. Por exemplo, se o aplicativo for destinado ao .NET Framework 3.5 e [!INCLUDE[net_v40_short](../code-quality/includes/net_v40_short_md.md)], use o 2.0.50727.0 número de versão e o XML devem ser semelhante ao seguinte:

   ```xml
   <dependency>
     <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
       <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />
     </dependentAssembly>
   </dependency>
   ```

### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>Para atualizar e assinar novamente o aplicativo e a implantação manifestos

- Atualizar e assinar novamente os manifestos de aplicativo e implantação. Para obter mais informações, confira [Como: Assinar novamente os manifestos de aplicativo e de implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md).

## <a name="see-also"></a>Consulte também
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [\<compatibleFrameworks > elemento](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [\<dependência > elemento](../deployment/dependency-element-clickonce-application.md)
- [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)
- [Esquema de arquivos de configuração](/dotnet/framework/configure-apps/file-schema/index)
