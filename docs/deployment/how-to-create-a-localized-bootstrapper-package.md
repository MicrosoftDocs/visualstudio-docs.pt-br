---
title: Criar um pacote bootstrapper localizado | Microsoft Docs
description: Saiba como criar versões localizadas do pacote de bootstrapper no ClickOnce criando mais dois arquivos para cada localidade.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- localized bootstrapper packages
- dependencies, creating localized bootstrapper packages
- prerequisites, creating localized bootstrapper packages
ms.assetid: 66a1bc7e-6540-4164-963d-557196a69d8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2a9d1fc91dcb385a9250dde3adb47c0d9553147f
ms.sourcegitcommit: 6aa55db5e1fe19d4d17886e0bfe140dbd186f8ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111877709"
---
# <a name="how-to-create-a-localized-bootstrapper-package"></a>Como criar um pacote de bootstrapper localizado
Depois de criar um pacote de bootstrapper, você pode criar versões localizadas desse pacote criando mais dois arquivos para cada localidade: um arquivo de termos de licença de software (como um *eula.rtf*) e um manifesto do pacote (*package.xml*).

 Por padrão, o Visual Studio 2010 inclui pacotes de bootstrapper localizados apenas para os .NET Framework 4, .NET Framework 4 Client Profile, F# Runtime 2.0 e F# Runtime 4.0. Você pode criar pacotes localizados para outros bootstrappers concluindo três etapas.

1. Crie uma pasta chamada após o nome da localidade em \Arquivos de Programas *(x86)\Microsoft \\ \<BootstrapperPackageName> SDKs\ClickOnce Bootstrapper\Packages*.

2. Crie um arquivo que contém os termos de licença de software para o pacote de bootstrapper e coloque-o na nova pasta.

3. Crie um manifesto do pacote com o nome *package.xml*, atualize as cadeias de caracteres e cultura e coloque o arquivo na nova pasta. Se você já criou um bootstrapper do Visual Studio no idioma de destino, você pode copiar o arquivo *package.xml* do Visual Studio e modificá-lo nesta etapa.

> [!NOTE]
> Se você estiver usando um projeto de instalação para implantar aplicativos, você poderá localizar o aplicativo alterando a propriedade **Localização**.

 [!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-a-localized-bootstrapper-package"></a>Para criar um pacote de bootstrapper localizado

1. Crie uma pasta com o nome da localidade.

     Em computadores de 32 bits, crie a pasta na pasta \Arquivos de *Programas\Microsoft SDKs\ClickOnce Bootstrapper\Packages. \\ \<BootstrapperPackageName> \\*

     Em computadores de 64 bits, crie a pasta na pasta \Arquivos de *Programas (x86)\Microsoft SDKs\ClickOnce Bootstrapper\Packages. \\ \<BootstrapperPackageName> \\*

     A tabela a seguir mostra os nomes das pastas que você pode usar para estabelecer uma localidade correspondente.

    |Locale|Nome da pasta|
    |------------|-----------------|
    |Chinês (Simplificado)|zh-Hans|
    |Chinês (Tradicional)|zh-Hans|
    |Tcheco|cs|
    |Alemão|de|
    |Inglês|en|
    |Espanhol|es|
    |Francês|fr|
    |Italiano|it|
    |Coreano|ko|
    |Japonês|ja|
    |Polonês|pl|
    |Português (Brasil)|pt-BR|
    |Russo|ru|
    |Turco|tr|

2. Crie um arquivo que contém os termos de licença de software para o pacote de bootstrapper e coloque-o na nova pasta.

3. Crie um manifesto do pacote *chamadopackage.xml* e coloque-o na nova pasta. Para obter mais informações, [consulte Como criar um manifesto do pacote](../deployment/how-to-create-a-package-manifest.md).

4. Atualize a seção `<Strings>` do manifesto do pacote, para que as cadeias de caracteres fiquem no idioma correto para a localidade.

5. Altere o valor `<String Name="Culture">` para corresponder ao nome da pasta.

6. Salve o arquivo *package.xml*.

### <a name="to-create-a-bootstrapper-package-for-net-framework-35-service-pack-1-localized-in-french"></a>Para criar um pacote de bootstrapper para o .NET Framework 3.5 Service Pack 1 localizado em francês

1. Crie uma pasta chamada *fr*. O nome da pasta deve corresponder ao nome da localidade.

     Em computadores de 32 bits, crie a pasta na pasta \Arquivos de *Programas\Microsoft SDKs\ClickOnce Bootstrapper\Packages\DotNetFX35SP1. \\*

     Em computadores de 64 bits, crie a pasta na pasta \Arquivos de Programas *(x86)\Microsoft SDKs\ClickOnce Bootstrapper\Packages\DotNetFX35SP1. \\*

2. Coloque uma versão localizada dos termos de licença de software na *pasta* fr.

3. Copie o arquivo \Arquivos de *Programas (x86)\Microsoft SDKs\ClickOnce Bootstrapper\Packages\DotNetFX35SP1\en\package.xml* para a pasta *fr* e abra o arquivo no Designer XML.

4. Atualize a seção `<Strings>` do pacote do manifesto para que as cadeias de caracteres de erro fiquem em francês.

5. Altere `<String Name="Culture">` o valor para *fr.*

6. Salve o arquivo *package.xml*.

>[!NOTE]
> A partir do Visual Studio 2019 Atualização 7, os pacotes de bootstrapper também serão descobertos no caminho *<VS Install Path> \MSBuild\Microsoft\VisualStudio\BootstrapperPackages*.

## <a name="see-also"></a>Confira também
- [Criar pacotes de bootstrapper](../deployment/creating-bootstrapper-packages.md)
- [Pré-requisitos de implantação do aplicativo](../deployment/application-deployment-prerequisites.md)
- [Como criar um manifesto de pacote](../deployment/how-to-create-a-package-manifest.md)