---
title: 'Passo a passo: Criando um Editor personalizado | Microsoft Docs'
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
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0b7c8bd8643b6c670e614f4745650f42ccca35f5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809734"
---
# <a name="walkthrough-creating-a-custom-editor"></a>Passo a passo: criando um editor personalizado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O modelo de projeto de VSPackage pode criar um editor personalizado simple em C++.  O modelo de projeto de VSPackage não dá suporte a projetos em C# ou Visual Basic. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="the-visual-studio-package-project-template"></a>O modelo de projeto de pacote do Visual Studio  
 O modelo de projeto de pacote do Visual Studio pode ser encontrado na **novo projeto** caixa de diálogo na pasta de extensibilidade do C++  
  
### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>Para criar um VSPackage usando o modelo de pacote do Visual Studio  
  
1.  Crie um projeto com o modelo de pacote do Visual Studio.  
  
2.  Selecione o **Editor personalizado** opção e clique em **próxima**. O **opções do Editor** página é exibida.  
  
3.  Digite o nome do seu editor na **nome do Editor** caixa. Digite a extensão de arquivo que você deseja ser associado com seu editor na **extensão de arquivo** caixa. O editor está disponível para arquivos com essa extensão. A extensão de arquivo está registrada para o Visual Studio apenas, não para Windows. Digite o nome de arquivo padrão para novos documentos criados com o seu editor na **nome de arquivo padrão** caixa.  
  
4.  Clique em **concluir** para criar o VSPackage na pasta que você especificou.  
  
### <a name="to-test-your-custom-editor"></a>Para testar seu editor personalizado  
  
1.  Sobre o **arquivo** , aponte para **New** e, em seguida, clique em **arquivo**.  
  
2.  No **modelos instalados** painel da **novo arquivo** caixa de diálogo, selecione o modelo de arquivo e, em seguida, o arquivo de tipo que você acabou de registrar.  
  
3.  Clique em **abrir** para exibir e editar o documento.  
  
     O editor dá suporte a operações de recortar e colar, localizar e substituir e aberto e de carga.  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../extensibility/internals/vspackages.md)

