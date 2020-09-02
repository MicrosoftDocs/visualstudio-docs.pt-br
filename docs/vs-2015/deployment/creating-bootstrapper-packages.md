---
title: Criando pacotes de bootstrapper | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
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
caps.latest.revision: 47
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: daf72a4466cd0f02eb6ef3a357276ed690fd26bf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "75845530"
---
# <a name="creating-bootstrapper-packages"></a>Criando pacotes de bootstrapper
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O programa de instalação é um instalador genérico que pode ser configurado para detectar e instalar componentes redistribuíveis como arquivos do Windows Installer (.msi) e programas executáveis. O instalador também é conhecido como bootstrapper. Ele é programado por um conjunto de manifestos XML que especificam os metadados para gerenciar a instalação do componente.  
  
 O bootstrapper primeiro detecta se qualquer um dos pré-requisitos já está instalado. Se os pré-requisitos não estiverem instalados, primeiro o bootstrapper mostra os contratos de licença. Em segundo lugar, depois que o usuário final aceita os contratos de licença, a instalação dos pré-requisitos começa. Caso contrário, se forem detectados todos os pré-requisitos, o bootstrapper apenas inicia o instalador do aplicativo.  
  
## <a name="creating-custom-packages"></a>Criando pacotes personalizados  
 É possível gerar manifestos usando o Editor de XML no Visual Studio. Para obter mais informações, consulte [como: criar um manifesto de pacote](../deployment/how-to-create-a-package-manifest.md) e [como criar um manifesto do produto](../deployment/how-to-create-a-product-manifest.md). Para ver um exemplo de criação de um pacote de bootstrapper, consulte [passo a passos: Criando um bootstrapper personalizado para mostrar um aviso de privacidade](../deployment/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt.md).  
  
 Para criar um pacote de bootstrapper, é necessário fornecer o redistribuível na forma de um arquivo EXE ou MSI ao Gerador de Manifesto do Bootstrapper. Em seguida, o Gerador de Manifesto do Bootstrapper cria os seguintes arquivos:  
  
- O manifesto do produto, product.xml, que contém todos os metadados de linguagem neutra para o pacote. Esse manifesto contém metadados comuns a todas as versões localizadas do componente redistribuível.  
  
- O manifesto do pacote, package.xml, que contém metadados específicos da linguagem. Esse manifesto geralmente contém mensagens de erro localizadas. Um componente deve ter, pelo menos, um pacote de manifesto para cada versão localizada desse componente.  
  
  Depois que esses arquivos são criados, coloque o arquivo de manifesto do produto em uma pasta indicada para o bootstrapper personalizado. O arquivo de manifesto do pacote vai para uma pasta nomeada de acordo com a localidade. Por exemplo, se o arquivo de manifesto do pacote for para redistribuição em inglês, coloque o arquivo em uma pasta chamada en. Repita esse processo para cada localidade, como ja para japonês e de para alemão. O pacote final de bootstrapper personalizado pode ter estrutura de pastas a seguir.  
  
  `CustomBootstrapperPackage`  
  
  `product.xml`  
  
  `CustomBootstrapper.msi`  
  
  `de`  
  
  `eula.rtf`  
  
  `package.xml`  
  
  `en`  
  
  `eula.rtf`  
  
  `package.xml`  
  
  `ja`  
  
  `eula.rtf`  
  
  `package.xml`  
  
  Por fim, copie os arquivos redistribuíveis para o local da pasta do bootstrapper. Para obter mais informações, consulte [como: criar um pacote de bootstrapper localizado](../deployment/how-to-create-a-localized-bootstrapper-package.md).  
  
```  
\Program Files\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages  
```  
  
 ou  
  
```  
\Program Files (x86)\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages  
```  
  
 Você também pode determinar a localização da pasta do bootstrapper no valor **Path** na seguinte chave do Registro:  
  
```  
HKLM\Software\Microsoft\GenericBootstrapper\11.0  
```  
  
 Em sistemas de 64 bits, use a seguinte chave de registro:  
  
```  
HKLM\Software\Wow6432Node\Microsoft\GenericBootstrapper\11.0  
```  
  
 Cada componente redistribuível aparece em sua própria subpasta no diretório de pacotes. Os arquivos redistribuíveis e o manifesto do produto são colocados nessa subpasta. As versões localizadas do componente e dos manifestos do pacote são colocadas em subpastas nomeadas de acordo com o nome da cultura.  
  
 Após esses arquivos serem copiados na pasta do bootstrapper, o pacote de bootstrapper aparece automaticamente na caixa de diálogo de pré-requisitos do Visual Studio. Se o seu pacote personalizado de bootstrapper não aparecer, feche e reabra a caixa de diálogo Pré-requisitos. Para obter mais informações, consulte a [caixa de diálogo pré-requisitos](../ide/reference/prerequisites-dialog-box.md).  
  
 A tabela a seguir mostra as propriedades que são preenchidas automaticamente pelo bootstrapper.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|ApplicationName|O nome do aplicativo.|  
|ProcessorArchitecture|O processador e bits por palavra da plataforma de destino de um executável. Os valores incluem o seguinte:<br /><br /> – Intel<br />– IA64<br />– AMD64|  
|[Version9x](https://msdn.microsoft.com/library/aa372490\(v=vs.140\).aspx)|O número de versão para os sistemas operacionais Microsoft Windows 95, Windows 98 ou Windows ME. A sintaxe da versão é Major.Minor.ServicePack.|  
|[VersionNT](/windows/desktop/Msi/versionnt)|O número de versão para os sistemas operacionais Windows NT, Windows 2000, Windows XP, Windows Vista, Windows Server 2008 ou Windows 7. A sintaxe da versão é Major.Minor.ServicePack.|  
|[VersionMSI](https://msdn.microsoft.com/library/aa372493\(v=vs.140\).aspx)|A versão de assembly do Windows Installer (msi.dll) executado durante a instalação.|  
|[AdminUser](https://msdn.microsoft.com/library/aa367545\(v=vs.140\).aspx)|Essa propriedade será definida se o usuário tiver privilégios de administrador. Os valores são verdadeiro ou falso.|  
|InstallMode|O modo de instalação indica de onde o componente precisa ser instalado. Os valores incluem o seguinte:<br /><br /> – HomeSite – os pré-requisitos são instalados do site do fornecedor.<br />– SpecificSite – os pré-requisitos são instalados da localização selecionada.<br />– SameSite – os pré-requisitos são instalados da mesma localização que o aplicativo.|  
  
## <a name="separating-redistributables-from-application-installations"></a>Separando redistribuíveis das instalações do aplicativo  
 Você pode evitar que seus arquivos redistribuíveis sejam implantados em projetos de instalação. Para fazer isso, crie uma lista redistribuível na pasta RedistList em seu diretório NET Framework:  
  
 `%ProgramFiles%\Microsoft.NET\RedistList`  
  
 A lista redistribuível é um arquivo XML que você deve nomear usando o seguinte formato: *nome da empresa*. *Nome do componente*.RedistList.xml. Assim, por exemplo, se o componente for chamado de Datawidgets feito por Acme, use Acme.DataWidgets.RedistList.xml. Um exemplo de conteúdo da lista redistribuível pode ser semelhante a:  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<FileList Redist="Acme.DataWidgets" >  
<File AssemblyName="Acme.DataGrid" Version="1.0.0.0" PublicKeyToken="b03f5f7f11d50a3a" Culture="neutral" ProcessorArchitecture="MSIL" InGAC="true" />  
</FileList>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Como: instalar pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [Caixa de diálogo pré-requisitos](../ide/reference/prerequisites-dialog-box.md)   
 [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)   
 [Use o bootstrapper do Visual Studio 2005 para iniciar sua instalação](https://msdn.microsoft.com/magazine/cc163899.aspx)
