---
title: Preparar extensões para a implantação do Windows Installer | Microsoft Docs
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
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 90dc7fb0ca361e6c1994cfd7108b171cda2ad1f9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755098"
---
# <a name="preparing-extensions-for-windows-installer-deployment"></a>Preparando extensões para a implantação do Windows Installer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você não pode usar um pacote do Windows Installer (MSI) para implantar um pacote VSIX. No entanto, você pode extrair o conteúdo de um pacote VSIX para implantação de MSI. Este documento mostra como preparar um projeto cuja saída padrão é um pacote VSIX para inclusão em um projeto de instalação.  
  
## <a name="preparing-an-extension-project-for-windows-installer-deployment"></a>Preparando um projeto de extensão para a implantação do Windows Installer  
 Execute estas etapas em novos projetos de extensão antes de adicionar a um projeto de instalação.  
  
#### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>Para preparar um projeto de extensão para a implantação do Windows Installer  
  
1.  Crie um VSPackage, componente MEF, Editor adorno ou outro tipo de projeto de extensibilidade que inclui um manifesto do VSIX.  
  
2.  Abra o manifesto do VSIX no editor de códigos.  
  
3.  Defina o elemento InstalledByMsi do manifesto do VSIX para `true`. Para obter mais informações sobre o manifesto do VSIX, consulte [2.0 referência do esquema de extensão do VSIX](../extensibility/vsix-extension-schema-2-0-reference.md).  
  
     Isso impede que o instalador do VSIX tentar instalar o componente.  
  
4.  Clique com botão direito no projeto no **Gerenciador de soluções** e clique em **propriedades**.  
  
5.  Selecione o **VSIX** guia.  
  
6.  Marque a caixa denominada **conteúdo VSIX de cópia no seguinte local** e digite o caminho para onde o projeto de instalação irá pegar os arquivos.  
  
## <a name="extracting-files-from-an-existing-vsix-package"></a>Extrair os arquivos de um pacote existente de VSIX  
 Execute estas etapas para adicionar o conteúdo de um pacote VSIX existente para um projeto de instalação quando você não tiver os arquivos de origem.  
  
#### <a name="to-extract-files-from-an-existing-vsix-package"></a>Para extrair os arquivos de um pacote existente de VSIX  
  
1.  Renomeie o. Arquivo VSIX que contém a extensão de *filename*. VSIX para *filename*. zip.  
  
2.  Copie o conteúdo do arquivo. zip em um diretório.  
  
3.  Exclua arquivo [Content_types]. XML do diretório.  
  
4.  Edite o manifesto do VSIX, conforme mostrado no procedimento anterior.  
  
5.  Adicione os arquivos restantes ao seu projeto de instalação.  
  
## <a name="see-also"></a>Consulte também  
 [Implantação de instalador do Visual Studio](http://msdn.microsoft.com/en-us/121be21b-b916-43e2-8f10-8b080516d2a0)   
 [Passo a passo: Criando uma ação personalizada](http://msdn.microsoft.com/en-us/4bd4b63a-2b91-431e-839c-5752443f0eaf)

