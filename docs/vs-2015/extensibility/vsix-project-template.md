---
title: Modelo de projeto do VSIX | Microsoft Docs
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
- deploy packages
- publish extension
ms.assetid: b6c82167-e2a5-4cff-8c8b-2d72e2a9092c
caps.latest.revision: 22
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c2b06582e1de7939e34f8fa49aa1cc9435010789
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51733854"
---
# <a name="vsix-project-template"></a>Modelo de projeto do VSIX
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o modelo de projeto de VSIX para encapsular uma ou mais extensões do Visual Studio em um projeto VSIX e, em seguida, publicar o pacote na [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847) site da Web.  
  
 Dá suporte à implantação do VSIX VSPackages, assemblies, componentes MEF, modelos de projeto, modelos de item, controles de caixa de ferramentas e os tipos de extensão personalizada.  
  
> [!NOTE]
>  Para usar os projetos VSIX, você deve instalar o SDK do Visual Studio. Para obter mais informações sobre o SDK do Visual Studio, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
## <a name="where-to-find-the-vsix-project-template"></a>Onde encontrar o modelo de projeto do VSIX  
 O modelo de projeto do VSIX está disponível na **novo projeto** caixa de diálogo. Expanda o **Visual Basic** nó ou o **Visual c#** nó e, em seguida, escolha **extensibilidade**.  
  
> [!TIP]
>  Assegure-se de que o .NET Framework 4.5 ou superior é especificado na lista suspensa na parte superior do **novo projeto** caixa de diálogo.  
  
## <a name="uses-of-the-vsix-project-template"></a>Usos do modelo de projeto do VSIX  
 O modelo de projeto do VSIX tem dois usos principais:  
  
- Para implantar modelos de projeto, modelos de item e outras extensões que não têm suporte do VSIX.  
  
- Para encapsular as saídas de várias extensões em pacote de uma implantação.  
  
  Não é necessário usar o modelo de projeto de VSIX para implantar os VSPackages ou outros tipos de extensões que já têm VSIX suporte.  
  
## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>Empacotando uma extensão em um projeto do VSIX vazio  
 Você pode empacotar uma extensão existente ou uma extensão que ainda não tenha VSIX dar suporte, encapsulando-os em um projeto vazio do VSIX. A extensão a ser encapsulado deve ser de um tipo que é compatível com o [esquema VSIX](../extensibility/vsix-extension-schema-2-0-reference.md).  
  
#### <a name="to-package-an-extension-by-using-a-vsix-project"></a>Para empacotar uma extensão usando um projeto do VSIX  
  
1.  Compile os projetos que compõem sua extensão.  
  
2.  Criar um projeto VSIX usando o **VSIX Project** modelo.  
  
     Vsixmanifest é aberto no **Designer de manifesto**.  
  
3.  Sobre o **ativos** guia, escolha o **New** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
4.  No **tipo** lista, escolha o tipo de extensão a ser adicionada.  
  
5.  Para adicionar um elemento de extensão ou conteúdo que está incluído na solução atual (por exemplo, um modelo de item ou um assembly compilado), execute as seguintes etapas:  
  
    1.  No **fonte** , escolha **um projeto na solução atual**.  
  
    2.  No **projeto** , escolha o nome da extensão.  
  
    3.  No **Embed nesta pasta** , digite o nome de uma pasta na qual é possível incorporar o ativo e, em seguida, escolha o **Okey** botão.  
  
6.  Para adicionar uma extensão ou um elemento de conteúdo que não está incluído na solução atual, execute as seguintes etapas:  
  
    1.  No **fonte** caixa de listagem, escolha **arquivo no sistema de arquivos**.  
  
    2.  No **caminho** campo, insira o caminho completo para o arquivo de extensão compilada ou compactada ou usar o **procurar** botão para navegar até o arquivo.  
  
    3.  No **Embed nesta pasta** , digite o nome de uma pasta na qual é possível incorporar o ativo e, em seguida, escolha o **Okey** botão.  
  
7.  Se você quiser que seu pacote para incluir extensões adicionais, você deve adicioná-los da mesma maneira.  
  
8.  Compile a solução.  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria um arquivo. VSIX que contém um arquivo de manifesto do VSIX, um arquivo de [Content_Types]. XML e todos os ativos de extensão que você adicionou ao projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema 2.0 de extensão do VSIX](../extensibility/vsix-extension-schema-2-0-reference.md)   
 [Localizando e usando extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md)

