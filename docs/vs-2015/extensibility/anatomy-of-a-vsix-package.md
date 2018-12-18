---
title: Anatomia de um pacote VSIX | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- visual studio extension
- vsix
- packages
ms.assetid: 8b86d62f-c274-4e91-82e0-38cdb9a423d5
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e1534c13c6c09a95fab21582ba0016153d1a6992
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51806978"
---
# <a name="anatomy-of-a-vsix-package"></a>Anatomia de um pacote do VSIX
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um pacote VSIX é um arquivo. VSIX que contém um ou mais extensões do Visual Studio, junto com o Visual Studio usa para classificar e instalar as extensões de metadados. Se os metadados está contido no arquivo [Content_Types]. XML e de manifesto do VSIX. Um pacote VSIX também pode conter um ou mais arquivos Extension.vsixlangpack para fornecer um texto de instalação localizada e pode conter outros pacotes VSIX para instalar dependências.  
  
 O formato de pacote VSIX segue o padrão Open Packaging Conventions (OPC). O pacote contém binários e arquivos de suporte, juntamente com um arquivo de [Content_Types]. XML e um. VSIX arquivo de manifesto. Um pacote VSIX pode conter a saída de vários projetos, ou até mesmo vários pacotes que têm seus próprios manifestos.  
  
> [!NOTE]
>  Os nomes dos arquivos incluídos em pacotes VSIX não devem incluir espaços nem caracteres reservados em identificadores de URI (Uniform Resource), como definido em [ \[RFC2396\]](http://go.microsoft.com/fwlink/?LinkId=90339).  
  
## <a name="the-vsix-manifest"></a>O manifesto do VSIX  
 O manifesto do VSIX contém informações sobre a extensão a ser instalado e segue o esquema de VSX. Para obter mais informações, consulte [1.0 referência do esquema de extensão do VSIX](http://msdn.microsoft.com/en-us/76e410ec-b1fb-4652-ac98-4a4c52e09a2b). Para um manifesto do VSIX de exemplo, consulte [PackageManifest elemento (elemento raiz, o esquema de VSX)](http://msdn.microsoft.com/en-us/f8ae42ba-775a-4d2b-976a-f556e147f187).  
  
 O manifesto do VSIX deve ser nomeado `extension.vsixmanifest` quando ele é incluído em um arquivo. VSIX.  
  
## <a name="the-content"></a>O conteúdo  
 Um pacote VSIX pode conter itens de caixa de ferramentas, modelos, VSPackages ou qualquer outro tipo de extensão com suporte pelo Visual Studio.  
  
## <a name="language-packs"></a>Pacotes de Idiomas  
 Um pacote VSIX pode conter uma vez ou mais arquivos Extension.vsixlangpack para fornecer o texto localizado durante a instalação. Para obter mais informações, consulte [Localizando os pacotes VSIX](../extensibility/localizing-vsix-packages.md).  
  
## <a name="dependencies-and-references"></a>Dependências e referências  
 Um pacote VSIX pode conter outros pacotes VSIX como referências. Cada um desses outros pacotes deve incluir seu próprio manifesto do VSIX.  
  
 Se um usuário tenta instalar uma extensão que tenha dependências, o instalador verifica se os assemblies necessários estão instalados no sistema de usuário. Se os assemblies necessários não foram encontrados **extensões e atualizações** exibe uma lista de assemblies ausentes.  
  
 Se o manifesto de extensão inclui um ou mais [referência](http://msdn.microsoft.com/en-us/32c52934-e81e-4b53-8cb6-4df45ef7bfa8) elementos **extensões e atualizações** compara o manifesto de cada referência para as extensões que estão instalados no sistema e instala o extensão referenciada se ele não ainda estiver instalado. Se uma versão anterior de uma extensão referenciada estiver instalada, a versão mais recente substitui-lo.  
  
 Se um projeto em uma solução multiprojeto inclui uma referência a outro projeto na mesma solução, o pacote VSIX inclui as dependências do projeto. Você pode substituir esse comportamento clicando-se a referência para o projeto interno e, em seguida, no **propriedades** janela, definindo o **saída grupos incluídos no VSIX** propriedade `BuiltProjectOutputGroup`.  
  
 Para incluir as DLLs satélite de assemblies referenciados no pacote VSIX, adicione `SatelliteDllsProjectOutputGroup` para o **saída grupos incluídos no VSIX** propriedade.  
  
## <a name="installation-location"></a>Local de instalação  
 Durante a instalação, **extensões e atualizações** procura o conteúdo do pacote VSIX em uma pasta sob % LocalAppData%\Microsoft\VisualStudio\14.0\Extensions.  
  
 Por padrão, a instalação se aplica somente ao usuário atual, como % LocalAppData % é um diretório específico do usuário. No entanto, se você definir a [AllUsers](http://msdn.microsoft.com/en-us/ac817f50-3276-4ddb-b467-8bbb1432455b) elemento do manifesto para `True`, a extensão será instalada em... \\ *VisualStudioInstallationFolder*\Common7\IDE\Extensions e estará disponível para todos os usuários do computador.  
  
## <a name="contenttypesxml"></a>[Content_Types]. XML  
 Arquivo [Content_Types]. XML identifica os tipos de arquivo no arquivo. VSIX expandido. Visual Studio usa esse arquivo durante a instalação do pacote, mas não instala o arquivo propriamente dito. Para obter mais informações sobre esse arquivo, consulte [a estrutura do Content_types\]. XML o arquivo](../extensibility/the-structure-of-the-content-types-dot-xml-file.md).  
  
 Um arquivo de [Content_Types]. XML é necessária, o Open Packaging Conventions (OPC) padrão. Para obter mais informações sobre OPC, consulte [OPC: um novo padrão para empacotamento seus dados](http://go.microsoft.com/fwlink/?LinkID=148207) no site do MSDN.

