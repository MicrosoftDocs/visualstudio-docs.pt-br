---
title: 'Como: empacotar manualmente uma extensão (implantação do VSIX) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d25990e0-e782-4a79-9d9a-1caf3c56c6a2
caps.latest.revision: 10
manager: douge
ms.openlocfilehash: 0d10d0e49389b43a288826adf2043c603aeff36a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49925832"
---
# <a name="how-to-manually-package-an-extension-vsix-deployment"></a>Como: empacotar manualmente uma extensão (implantação do VSIX)
Você pode criar um pacote VSIX para encapsular um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão para a implantação. Há três maneiras de criar o pacote:  
  
- Criar um projeto de pacote VSIX usando um dos modelos de extensibilidade que estão incluídos no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] SDK. Essa é a opção mais fácil na maioria dos cenários.  
  
- Encapsular a saída do seu projeto de extensão em um vazio [VSIX Project](../extensibility/vsix-project-template.md). Recomendamos essa opção para modelos, não há suporte para assemblies e tipos personalizados.  
  
- Crie manualmente um pacote VSIX. Recomendamos essa opção somente quando as duas opções não estão disponíveis.  
  
  Este documento descreve a terceira opção.  
  
## <a name="creating-a-vsix-package"></a>Criando um pacote VSIX  
 Para empacotar manualmente uma extensão, adicione um arquivo extension.manifest e um [Content_Types]. XML ao projeto de extensão, colocá-los em um arquivo compactado junto com sua saída de compilação e renomear o arquivo compactado para que ele tenha uma extensão de nome de arquivo. VSIX. A extensão para ser empacotado deve ser de um tipo que é compatível com o [esquema VSIX](http://msdn.microsoft.com/en-us/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).  
  
> [!NOTE]
>  Os nomes dos arquivos em pacotes VSIX não devem incluir espaços nem caracteres reservados em identificadores de URI (Uniform Resource), como definido em [ \[RFC2396\]](http://go.microsoft.com/fwlink/?LinkId=90339).  
  
#### <a name="to-manually-create-a-vsix-package"></a>Para criar manualmente um pacote VSIX  
  
1.  Crie uma extensão do Visual Studio de um tipo que é compatível com o esquema VSIX.  
  
2.  Crie um arquivo XML e nomeie- `extension.vsixmanifest`.  
  
3.  Preencha o arquivo Extension vsixmanifest de acordo com o esquema VSIX. Para um manifesto de exemplo, consulte [PackageManifest elemento (elemento raiz, o esquema de VSX)](http://msdn.microsoft.com/en-us/f8ae42ba-775a-4d2b-976a-f556e147f187).  
  
4.  Crie um segundo arquivo XML e nomeie- `[Content_Types].xml`.  
  
5.  Preencha o arquivo [Content_Types]. XML conforme especificado na [a estrutura do Content_types\]. XML o arquivo](../extensibility/the-structure-of-the-content-types-dot-xml-file.md).  
  
6.  Colocar ambos os arquivos XML em um diretório junto com a extensão a ser implantado.  
  
     No caso de um modelo de projeto ou o modelo de item, coloque o arquivo. zip que contém o modelo na mesma pasta dos arquivos XML. Não coloque os arquivos XML no arquivo. zip.  
  
     Em todos os outros casos, coloque os arquivos XML no mesmo diretório que a saída da compilação.  
  
7.  No Windows Explorer, clique com botão direito na pasta que contém a extensão de conteúdo e os dois arquivos XML, clique em **enviar para**e, em seguida, clique em **pasta compactada (zipada)**.  
  
8.  Renomeie o arquivo. zip resultante *Filename*. VSIX, onde *Filename* é o nome do arquivo redistribuível que instala o pacote.  
  
## <a name="see-also"></a>Consulte também  
 [Envio de extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)   
 [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)   
 [Elemento PackageManifest (elemento raiz, o esquema VSX)](http://msdn.microsoft.com/en-us/f8ae42ba-775a-4d2b-976a-f556e147f187)