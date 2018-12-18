---
title: 'Como: criar um pacote de Bootstrapper localizado | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
helpviewer_keywords:
- localized bootstrapper packages
- dependencies, creating localized bootstrapper packages
- prerequisites, creating localized bootstrapper packages
ms.assetid: 66a1bc7e-6540-4164-963d-557196a69d8a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1083633410c42c63f8c3e9a2ff341a2278f0b63a
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39153209"
---
# <a name="how-to-create-a-localized-bootstrapper-package"></a>Como: criar um pacote de bootstrapper localizado
Depois de criar um pacote de bootstrapper, você pode criar versões localizadas do pacote de bootstrapper, criando mais dois arquivos para cada localidade: arquivo de termos de uma licença de software (como uma *EULA. rtf*) e um manifesto de pacote (*Package. XML*).  
  
 Por padrão, o Visual Studio 2010 inclui pacotes de bootstrapper localizados apenas para os .NET Framework 4, .NET Framework 4 Client Profile, F# Runtime 2.0 e F# Runtime 4.0. Você pode criar pacotes localizados para outros bootstrappers concluindo três etapas.  
  
1.  Crie uma pasta que é nomeada após o nome da localidade na *\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages\\\<Nomepacotebootstrapper >*.  
  
2.  Crie um arquivo que contém os termos de licença de software para o pacote de bootstrapper e coloque-o na nova pasta.  
  
3.  Criar um manifesto de pacote denominado *Package*, atualize as cadeias de caracteres e a cultura e colocar o arquivo na nova pasta. Se você já tiver criado um bootstrapper do Visual Studio no idioma de destino, você pode copiar o Visual Studio *Package* de arquivo e modificá-lo nesta etapa.  
  
> [!NOTE]
>  Se você estiver usando um projeto de instalação para implantar aplicativos, você pode localizar seu aplicativo, alterando a **localização** propriedade.  
  
 [!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]  
  
### <a name="to-create-a-localized-bootstrapper-package"></a>Para criar um pacote de bootstrapper localizado  
  
1.  Crie uma pasta com o nome da localidade.  
  
     Em computadores de 32 bits, crie a pasta na *\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages\\\<Nomepacotebootstrapper >\\*  pasta.  
  
     Em computadores de 64 bits, crie a pasta na *\Program Files (86) \Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages\\\<Nomepacotebootstrapper >\\*  pasta.  
  
     A tabela a seguir mostra os nomes das pastas que você pode usar para estabelecer uma localidade correspondente.  
  
    |Localidade|Nome da pasta|  
    |------------|-----------------|  
    |Chinês (simplificado)|zh-Hans|  
    |Chinês (tradicional)|zh-Hant|  
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
  
2.  Crie um arquivo que contém os termos de licença de software para o pacote de bootstrapper e coloque-o na nova pasta.  
  
3.  Criar um manifesto de pacote denominado *Package* e coloque-o na nova pasta. Para obter mais informações, consulte [como: criar um manifesto de pacote](../deployment/how-to-create-a-package-manifest.md).  
  
4.  Atualize a seção `<Strings>` do manifesto do pacote, para que as cadeias de caracteres fiquem no idioma correto para a localidade.  
  
5.  Altere o valor `<String Name="Culture">` para corresponder ao nome da pasta.  
  
6.  Salvar a *Package* arquivo.  
  
### <a name="to-create-a-bootstrapper-package-for-net-framework-35-service-pack-1-localized-in-french"></a>Para criar um pacote de bootstrapper para o .NET Framework 3.5 Service Pack 1 localizado em francês  
  
1.  Crie uma pasta denominada *fr*. O nome da pasta deve corresponder ao nome da localidade.  
  
     Em computadores de 32 bits, crie a pasta na *\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages\DotNetFX35SP1\\*  pasta.  
  
     Em computadores de 64 bits, crie a pasta na *\Program Files (86) \Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages\DotNetFX35SP1\\*  pasta.  
  
2.  Coloque uma versão localizada dos termos de licença de software para o *fr* pasta.  
  
3.  Cópia de *\Program arquivos (x86) \Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages\DotNetFX35SP1\en\package.xml* do arquivo para o *fr* pasta e abra o arquivo no XML Designer.  
  
4.  Atualize a seção `<Strings>` do pacote do manifesto para que as cadeias de caracteres de erro fiquem em francês.  
  
5.  Alterar o `<String Name="Culture">` de valor para *fr*.  
  
6.  Salvar a *Package* arquivo.  
  
## <a name="see-also"></a>Consulte também  
 [Criar pacotes de bootstrapper](../deployment/creating-bootstrapper-packages.md)   
 [Pré-requisitos de implantação de aplicativo](../deployment/application-deployment-prerequisites.md)   
 [Como criar um manifesto de pacote](../deployment/how-to-create-a-package-manifest.md)