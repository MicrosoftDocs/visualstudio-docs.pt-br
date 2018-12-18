---
title: Anatomia de um pacote VSIX | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- visual studio extension
- vsix
- packages
ms.assetid: 8b86d62f-c274-4e91-82e0-38cdb9a423d5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1dea0fce75d83678161013baef109364842fcc46
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49937727"
---
# <a name="anatomy-of-a-vsix-package"></a>Anatomia de um pacote VSIX
Um pacote VSIX é um *VSIX* arquivo que contém um ou mais extensões do Visual Studio, junto com os metadados do Visual Studio usa para classificar e instalar as extensões. Se os metadados está contido no manifesto do VSIX e o *[Content_Types]. XML* arquivo. Um pacote VSIX também pode conter um ou mais *Extension.vsixlangpack* arquivos para fornecer localizado texto da instalação e pode conter outros pacotes VSIX para instalar dependências.  
  
 O formato de pacote VSIX segue o padrão Open Packaging Conventions (OPC). O pacote contém binários e arquivos de suporte, juntamente com uma *[Content_Types]. XML* arquivo e um *VSIX* arquivo de manifesto. Um pacote VSIX pode conter a saída de vários projetos, ou até mesmo vários pacotes que têm seus próprios manifestos.  
  
> [!NOTE]
>  Os nomes dos arquivos incluídos em pacotes VSIX não devem incluir espaços nem caracteres reservados em identificadores de URI (Uniform Resource), como definido em [ \[RFC2396\]](http://go.microsoft.com/fwlink/?LinkId=90339).  
  
## <a name="the-vsix-manifest"></a>O manifesto do VSIX  
 O manifesto do VSIX contém informações sobre a extensão a ser instalado e segue o esquema de VSX. Para obter mais informações, consulte [referência de esquema 1.0 de extensão do VSIX](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b). Para um manifesto do VSIX de exemplo, consulte [PackageManifest elemento (elemento raiz, o esquema VSX)](https://msdn.microsoft.com/library/f8ae42ba-775a-4d2b-976a-f556e147f187).  
  
 O manifesto do VSIX deve ser nomeado `extension.vsixmanifest` quando ele é incluído em um ^. VSIX * arquivo.  
  
## <a name="the-content"></a>O conteúdo  
 Um pacote VSIX pode conter itens de caixa de ferramentas, modelos, VSPackages ou qualquer outro tipo de extensão com suporte pelo Visual Studio.  
  
## <a name="language-packs"></a>Pacotes de idiomas  
 Um pacote VSIX pode conter uma vez ou mais *Extension.vsixlangpack* arquivos para fornecer o texto localizado durante a instalação. Para obter mais informações, consulte [pacotes VSIX Localizando](../extensibility/localizing-vsix-packages.md).  
  
## <a name="dependencies-and-references"></a>Dependências e referências  
 Um pacote VSIX pode conter outros pacotes VSIX como referências. Cada um desses outros pacotes deve incluir seu próprio manifesto do VSIX.  
  
 Se um usuário tenta instalar uma extensão que tenha dependências, o instalador verifica se os assemblies necessários estão instalados no sistema de usuário. Se os assemblies necessários não foram encontrados **extensões e atualizações** exibe uma lista de assemblies ausentes.  
  
 Se o manifesto de extensão inclui um ou mais [referência](/previous-versions/visualstudio/visual-studio-2010/dd393687(v=vs.100)) elementos **extensões e atualizações** compara o manifesto de cada referência para as extensões que estão instalados no sistema e instala o extensão referenciada se ele não ainda estiver instalado. Se uma versão anterior de uma extensão referenciada estiver instalada, a versão mais recente substitui-lo.  
  
 Se um projeto em uma solução multiprojeto inclui uma referência a outro projeto na mesma solução, o pacote VSIX inclui as dependências do projeto. Você pode substituir esse comportamento clicando-se a referência para o projeto interno e, em seguida, no **propriedades** janela, definindo o **saída grupos incluídos no VSIX** propriedade `BuiltProjectOutputGroup`.  
  
 Para incluir as DLLs satélite de assemblies referenciados no pacote VSIX, adicione `SatelliteDllsProjectOutputGroup` para o **saída grupos incluídos no VSIX** propriedade.  
  
## <a name="installation-location"></a>Local de instalação  
 Durante a instalação, **extensões e atualizações** procura o conteúdo do pacote VSIX em uma pasta sob *%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions*.  
  
 Por padrão, a instalação se aplica somente ao usuário atual, pois *% LocalAppData %* é um diretório específico do usuário. No entanto, se você definir a [AllUsers](https://msdn.microsoft.com/library/ac817f50-3276-4ddb-b467-8bbb1432455b) elemento do manifesto para `True`, a extensão será instalada em <em>... \\</em> VisualStudioInstallationFolder<em>\Common7\IDE\Extensions</em> e estará disponível para todos os usuários do computador.  
  
## <a name="contenttypesxml"></a>[Content_Types]. XML  
 O *[Content_Types]. XML* arquivo identifica os tipos de arquivo expandido *VSIX* arquivo. Visual Studio usa esse arquivo durante a instalação do pacote, mas não instala o arquivo propriamente dito. Para obter mais informações sobre esse arquivo, consulte [a estrutura do arquivo [Content_types]. XML](the-structure-of-the-content-types-dot-xml-file.md).  
  
 Um *[Content_Types]. XML* arquivo é exigido pelo padrão Open Packaging Conventions (OPC). Para obter mais informações sobre OPC, consulte [OPC: um novo padrão para empacotar dados](https://blogs.msdn.microsoft.com/msdnmagazine/2007/08/08/opc-a-new-standard-for-packaging-your-data/) no site do MSDN.