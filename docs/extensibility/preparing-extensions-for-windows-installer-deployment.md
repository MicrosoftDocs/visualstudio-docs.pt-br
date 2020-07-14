---
title: Preparando extensões para implantação de Windows Installer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 74cfdcaf5b9f9babe9eefed59f1ea62478434e66
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85906157"
---
# <a name="prepare-extensions-for-windows-installer-deployment"></a>Preparar extensões para implantação de Windows Installer
Você não pode usar um pacote de Windows Installer (MSI) para implantar um pacote VSIX. No entanto, você pode extrair o conteúdo de um pacote VSIX para a implantação do MSI. Este documento mostra como preparar um projeto cuja saída padrão é um pacote VSIX para inclusão em um projeto de instalação.

## <a name="prepare-an-extension-project-for-windows-installer-deployment"></a>Preparar um projeto de extensão para implantação Windows Installer
 Execute estas etapas em novos projetos de extensão antes de adicionar a um projeto de instalação.

### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>Para preparar um projeto de extensão para implantação Windows Installer

1. Crie um VSPackage, um componente do MEF, um editor Adornment ou outro tipo de projeto de extensibilidade que inclua um manifesto do VSIX.

2. Abra o manifesto do VSIX no editor de código.

3. Defina o `InstalledByMsi` elemento do manifesto do VSIX como `true` . Para obter mais informações sobre o manifesto do VSIX, consulte [referência do esquema de extensão do vsix 2,0](../extensibility/vsix-extension-schema-2-0-reference.md).

     Isso impede que o instalador do VSIX tente instalar o componente.

4. Clique com o botão direito do mouse no projeto em **Gerenciador de soluções** e clique em **Propriedades**.

5. Selecione a guia **VSIX** .

6. Marque a caixa rotulada **copiar conteúdo do VSIX no seguinte local** e digite o caminho para onde o projeto de instalação irá pegar os arquivos.

## <a name="extract-files-from-an-existing-vsix-package"></a>Extrair arquivos de um pacote VSIX existente
 Execute estas etapas para adicionar o conteúdo de um pacote VSIX existente a um projeto de instalação quando você não tiver os arquivos de origem.

### <a name="to-extract-files-from-an-existing-vsix-package"></a>Para extrair arquivos de um pacote VSIX existente

1. Renomeie o *. Arquivo VSIX* que contém a extensão de *filename. vsix* para *filename.zip*.

2. Copie o conteúdo do arquivo *. zip* em um diretório.

3. Exclua o arquivo *[Content_types]. xml* do diretório.

4. Edite o manifesto do VSIX, conforme mostrado no procedimento anterior.

5. Adicione os arquivos restantes ao seu projeto de instalação.

## <a name="see-also"></a>Confira também
- [Implantação do instalador do Visual Studio](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)
- [Walkthrough: criar uma ação personalizada](/previous-versions/visualstudio/visual-studio-2010/d9k65z2d(v=vs.100))
