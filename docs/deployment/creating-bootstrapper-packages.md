---
title: Criar pacotes de bootstrapper
ms.custom: ''
ms.date: 05/02/2018
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [Visual Studio], prerequisites
- deploying applications [Visual Studio], custom prerequisites
- prerequisites, custom
- RedistList file
- custom prerequisites
- redistributables list
ms.assetid: ba1a785b-693d-446b-bcae-b88cadee73d1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a16044657b197229253f93fc6aea6130a4522f64
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39512178"
---
# <a name="create-bootstrapper-packages"></a>Criar pacotes de bootstrapper
O programa de instalação é um instalador genérico que pode ser configurado para detectar e instalar componentes redistribuíveis, como o Windows Installer (*. msi*) arquivos e programas executáveis. O instalador também é conhecido como bootstrapper. Ele é programado por um conjunto de manifestos XML que especificam os metadados para gerenciar a instalação do componente.  Cada componente redistribuível, ou o pré-requisito, que aparece na **pré-requisitos** caixa de diálogo do ClickOnce é um pacote de bootstrapper. Um pacote de bootstrapper é um grupo de diretórios e arquivos que contém arquivos de manifesto que descrevem como o pré-requisito deve ser instalado. 
  
O bootstrapper primeiro detecta se qualquer um dos pré-requisitos já está instalado. Se os pré-requisitos não estiverem instalados, primeiro o bootstrapper mostra os contratos de licença. Em segundo lugar, depois que o usuário final aceita os contratos de licença, a instalação dos pré-requisitos começa. Caso contrário, se forem detectados todos os pré-requisitos, o bootstrapper apenas inicia o instalador do aplicativo.  
  
## <a name="create-custom-bootstrapper-packages"></a>Criar pacotes de bootstrapper personalizado  
Você pode gerar os manifestos do bootstrapper usando o Editor de XML no Visual Studio. Para ver um exemplo de como criar um pacote de bootstrapper, consulte [instruções passo a passo: criar um bootstrapper personalizado com um prompt de privacidade](../deployment/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt.md).  
  
Para criar um pacote de bootstrapper, você precisa criar um manifesto de produto e, para cada versão localizada de um componente, um manifesto de pacote.
  
* O manifesto do produto *Product*, contém todos os metadados com neutralidade de idioma para o pacote. Esse manifesto contém metadados comuns a todas as versões localizadas do componente redistribuível.  Para criar esse arquivo, consulte [como: criar um manifesto de produto](../deployment/how-to-create-a-product-manifest.md).
  
* O manifesto de pacote *Package*, contém metadados específicos do idioma; geralmente contém mensagens de erro localizada. Um componente deve ter, pelo menos, um pacote de manifesto para cada versão localizada desse componente. Para criar esse arquivo, consulte [como: criar um manifesto de pacote](../deployment/how-to-create-a-package-manifest.md).
  
Depois que esses arquivos são criados, coloque o arquivo de manifesto do produto em uma pasta indicada para o bootstrapper personalizado. O arquivo de manifesto do pacote vai para uma pasta nomeada de acordo com a localidade. Por exemplo, se o arquivo de manifesto do pacote for para redistribuição em inglês, coloque o arquivo em uma pasta chamada en. Repita esse processo para cada localidade, como ja para japonês e de para alemão. O pacote final de bootstrapper personalizado pode ter estrutura de pastas a seguir.  

    ```xml
    CustomBootstrapperPackage
      product.xml
      CustomBootstrapper.msi
      de
        eula.rtf
        package.xml
      en
        eula.rtf
        package.xml
      ja
        eula.rtf
        package.xml
    ```
  
Em seguida, copie os arquivos redistribuíveis para o local de pasta do bootstrapper. Para obter mais informações, consulte [como: criar um pacote de bootstrapper localizado](../deployment/how-to-create-a-localized-bootstrapper-package.md).
 
    *\Program Files\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages*
    
ou  
    
    *\Program Files (x86)\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages*
  
Você também pode determinar o local da pasta do bootstrapper para o **caminho** valor na seguinte chave do registro:  
  
    *HKLM\Software\Microsoft\GenericBootstrapper\11.0*
  
Em sistemas de 64 bits, use a seguinte chave do registro:  
  
    *HKLM\Software\Wow6432Node\Microsoft\GenericBootstrapper\11.0*
  
Cada componente redistribuível aparece em sua própria subpasta no diretório de pacotes. O produto de manifesto e redistribuível arquivos devem ser colocados nessa subpasta. Versões localizadas dos manifestos do componente e de pacote devem ser colocadas em subpastas nomeadas de acordo com o nome de cultura.  
  
Depois que esses arquivos são copiados na pasta do bootstrapper, o pacote de bootstrapper aparece automaticamente no Visual Studio **pré-requisitos** caixa de diálogo. Se o seu pacote de bootstrapper personalizado não aparecer, feche e reabra o **pré-requisitos** caixa de diálogo. Para obter mais informações, consulte [caixa de diálogo de pré-requisitos](../ide/reference/prerequisites-dialog-box.md).  
  
A tabela a seguir mostra as propriedades que são preenchidas automaticamente pelo bootstrapper.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|ApplicationName|O nome do aplicativo.|  
|ProcessorArchitecture|O processador e bits por palavra da plataforma de destino de um executável. Os valores incluem o seguinte:<br /><br /> -Intel<br />-IA64<br />-AMD64|  
|[Version9x](/windows/desktop/Msi/version9x)|O número de versão para os sistemas operacionais Microsoft Windows 95, Windows 98 ou Windows ME. A sintaxe da versão é Major.Minor.ServicePack.|  
|[VersionNT](/windows/desktop/Msi/versionnt)|O número de versão para os sistemas operacionais Windows NT, Windows 2000, Windows XP, Windows Vista, Windows Server 2008 ou Windows 7. A sintaxe da versão é Major.Minor.ServicePack.|  
|[VersionMSI](/windows/desktop/Msi/versionmsi)|A versão do assembly do Windows Installer (MSI) para ser executado durante a instalação.|  
|[AdminUser](/windows/desktop/Msi/adminuser)|Essa propriedade será definida se o usuário tiver privilégios de administrador. Os valores são verdadeiro ou falso.|  
|InstallMode|O modo de instalação indica de onde o componente precisa ser instalado. Os valores incluem o seguinte:<br /><br /> -HomeSite - pré-requisitos são instalados a partir do site do fornecedor.<br />-SpecificSite - pré-requisitos são instalados no local que você selecionar.<br />-SameSite - pré-requisitos são instalados no mesmo local que o aplicativo.|  
  
## <a name="separate-redistributables-from-application-installations"></a>Pacotes redistribuíveis separado das instalações do aplicativo  
Você pode evitar que seus arquivos redistribuíveis sejam implantados em projetos de instalação. Para fazer isso, crie uma lista redistribuível na pasta RedistList em seu diretório NET Framework:  
  
`%ProgramFiles%\Microsoft.NET\RedistList`  
  
A lista redistribuível é um arquivo XML que você deve nomear usando o seguinte formato:  *\<nome da empresa >.\< Nome do componente >. Redistlist*. Assim, por exemplo, se o componente é chamado de DataWidgets feito por Acme, use *datawidgets*. Um exemplo de conteúdo da lista redistribuível pode ser semelhante a:  
  
```xml  
<?xml version="1.0" encoding="UTF-8"?>  
<FileList Redist="Acme.DataWidgets" >  
<File AssemblyName="Acme.DataGrid" Version="1.0.0.0" PublicKeyToken="b03f5f7f11d50a3a" Culture="neutral" ProcessorArchitecture="MSIL" InGAC="true" />  
</FileList>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Como: instalar pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [Caixa de diálogo de pré-requisitos](../ide/reference/prerequisites-dialog-box.md)   
 [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)   
 [Usar o bootstrapper do Visual Studio 2005 para iniciar a instalação](http://go.microsoft.com/fwlink/?LinkId=107537)
