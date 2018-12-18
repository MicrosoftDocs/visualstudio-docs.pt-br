---
title: Preparar extensões para a implantação do Windows Installer | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: cc742fecbbe03ff3d3aa0fb3f8d61a9c5f09254b
ms.sourcegitcommit: 9765b3fcf89375ca499afd9fc42cf4645b66a8a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46495265"
---
# <a name="prepare-extensions-for-windows-installer-deployment"></a>Preparar extensões para a implantação do Windows Installer
Você não pode usar um pacote do Windows Installer (MSI) para implantar um pacote VSIX. No entanto, você pode extrair o conteúdo de um pacote VSIX para implantação de MSI. Este documento mostra como preparar um projeto cuja saída padrão é um pacote VSIX para inclusão em um projeto de instalação.  
  
## <a name="prepare-an-extension-project-for-windows-installer-deployment"></a>Preparar um projeto de extensão para a implantação do Windows Installer  
 Execute estas etapas em novos projetos de extensão antes de adicionar a um projeto de instalação.  
  
### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>Para preparar um projeto de extensão para a implantação do Windows Installer  
  
1.  Crie um VSPackage, componente MEF, Editor adorno ou outro tipo de projeto de extensibilidade que inclui um manifesto do VSIX.  
  
2.  Abra o manifesto do VSIX no editor de códigos.  
  
3.  Defina as `InstalledByMsi` elemento do manifesto do VSIX para `true`. Para obter mais informações sobre o manifesto do VSIX, consulte [referência de esquema 2.0 de extensão do VSIX](../extensibility/vsix-extension-schema-2-0-reference.md).  
  
     Isso impede que o instalador do VSIX tentar instalar o componente.  
  
4.  Clique com botão direito no projeto no **Gerenciador de soluções** e clique em **propriedades**.  
  
5.  Selecione o **VSIX** guia.  
  
6.  Marque a caixa denominada **conteúdo VSIX de cópia no seguinte local** e digite o caminho para onde o projeto de instalação irá pegar os arquivos.  
  
## <a name="extract-files-from-an-existing-vsix-package"></a>Extraia os arquivos de um pacote existente de VSIX  
 Execute estas etapas para adicionar o conteúdo de um pacote VSIX existente para um projeto de instalação quando você não tiver os arquivos de origem.  
  
### <a name="to-extract-files-from-an-existing-vsix-package"></a>Para extrair os arquivos de um pacote existente de VSIX  
  
1.  Renomeie o *. VSIX* arquivo que contém a extensão de *filename.vsix* à *filename.zip*.  
  
2.  Copie o conteúdo do *. zip* arquivo em um diretório.  
  
3.  Excluir o *[Content_types]. XML* arquivo do diretório.  
  
4.  Edite o manifesto do VSIX, conforme mostrado no procedimento anterior.  
  
5.  Adicione os arquivos restantes ao seu projeto de instalação.  
  
## <a name="see-also"></a>Consulte também  
 [Implantação do instalador do Visual Studio](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)   
 [Passo a passo: Criar uma ação personalizada](/previous-versions/visualstudio/visual-studio-2010/d9k65z2d(v=vs.100))