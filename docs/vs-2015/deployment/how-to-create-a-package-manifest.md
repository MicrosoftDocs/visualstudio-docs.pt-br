---
title: 'Como: criar um manifesto de pacote | Microsoft Docs'
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
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- package files [Windows Installer]
- package files [ClickOnce]
- prerequisites, custom bootstrapper package
- dependencies, custom bootstrapper packages
ms.assetid: 5aecc507-2764-42f2-ae6f-c227971cf0af
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 2941000e9fa2c6f1d9fd4835c9fd0b8fa1fd1b4f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49182423"
---
# <a name="how-to-create-a-package-manifest"></a>Como criar um manifesto de pacote
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para implantar o pré-requisitos para o seu aplicativo, você pode usar um pacote de bootstrapper. Um pacote de bootstrapper contém um arquivo de manifesto de produto único, mas um manifesto de pacote para cada localidade. Funcionalidade compartilhada entre diferentes versões localizadas deve ir para o manifesto do produto.  
  
 Para obter mais informações sobre manifestos de pacote, consulte [como: criar um manifesto de produto](../deployment/how-to-create-a-product-manifest.md).  
  
## <a name="creating-the-package-manifest"></a>Criando o manifesto do pacote  
  
#### <a name="to-create-the-package-manifest"></a>Para criar o manifesto do pacote  
  
1.  Crie um diretório para o pacote de bootstrapper. Este exemplo usa C:\package.  
  
2.  Crie um subdiretório com o nome da localidade, como en para inglês.  
  
3.  No Visual Studio, crie um arquivo XML que é denominado `package.xml`e salve-o para a pasta C:\package\en.  
  
4.  Adicione o XML para listar o nome do pacote de bootstrapper, a cultura para esse manifesto de pacote localizado e o contrato de licença opcional. O XML a seguir usa as variáveis `DisplayName` e `Culture`, que é definido em um elemento posterior.  
  
    ```  
    <Package  
        xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
        Name="DisplayName"  
        Culture="Culture"  
        LicenseAgreement="eula.txt">  
    ```  
  
5.  Adicione o XML para listar todos os arquivos que estão no diretório específica de localidade. O XML a seguir usa um arquivo chamado EULA é aplicável para o **en** localidade.  
  
    ```  
    <PackageFiles>  
      <PackageFile Name="eula.txt"/>  
    </PackageFiles>  
    ```  
  
6.  Adicione o XML para definir as cadeias de caracteres localizáveis para o pacote de bootstrapper. O XML a seguir adiciona cadeias de caracteres de erro para a localidade en.  
  
    ```  
      <Strings>  
        <String Name="DisplayName">Custom Bootstrapper Package</String>  
        <String Name="CultureName">en</String>  
        <String Name="NotAnAdmin">You must be an administrator to install   
    this package.</String>  
        <String Name="GeneralFailure">A general error has occurred while   
    installing this package.</String>  
    </Strings>  
    ```  
  
7.  Copie a pasta de C:\package para o diretório de bootstrapper do Visual Studio. Para Visual Studio 2010, isso é o diretório \Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages.  
  
## <a name="example"></a>Exemplo  
 O manifesto de pacote contém informações específicas de localidade, como mensagens de erro, termos de licença de software e pacotes de idiomas.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<Package  
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
  Name="DisplayName"  
  Culture="Culture"  
  LicenseAgreement="eula.txt">  
  
  <PackageFiles>  
    <PackageFile Name="eula.txt"/>  
  </PackageFiles>  
  
  <Strings>  
    <String Name="DisplayName">Custom Bootstrapper Package</String>  
    <String Name="Culture">en</String>  
    <String Name="NotAnAdmin">You must be an administrator to install this package.</String>  
    <String Name="GeneralFailure">A general error has occurred while   
installing this package.</String>  
  </Strings>  
</Package>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)



