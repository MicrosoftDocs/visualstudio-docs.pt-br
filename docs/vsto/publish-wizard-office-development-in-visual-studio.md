---
title: Assistente de publicação (desenvolvimento do Office no Visual Studio)
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VST.ProjectProperties.PublishWizard
- VST.PublishWizard.Publish.2007System
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], Publish Wizard
- deploying applications [Office development in Visual Studio], Publish Wizard
- Office applications [Office development in Visual Studio], Publish Wizard
- Publish Wizard, Office solutions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0d1b72745b3bd8a24dc69a5bc4e1508c8b2f7571
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672740"
---
# <a name="publish-wizard-office-development-in-visual-studio"></a>Assistente de publicação (desenvolvimento do Office no Visual Studio)
  Use o **Assistente de publicação** para copiar arquivos de solução para um local especificado, criar os arquivos de manifesto e criar um programa de instalação.  
  
 Para acessar esse assistente, no **construir** menu, escolha **Publish** *SolutionName*. Você também pode acessar o **Assistente de publicação** partir **Gerenciador de soluções**. Abra o menu de atalho do nó do projeto e, em seguida, escolha **publicar**.  
  
 As seções a seguir descreve uma página do assistente.  
  
## <a name="where-do-you-want-to-publish-the-application"></a>Onde você deseja publicar o aplicativo?  
 **Especifique o local para publicar este aplicativo**  
 Necessário. O local de publicação é o diretório onde o **Assistente de publicação** copia os arquivos de solução, como os manifestos, assemblies, certificado temporário e outros arquivos do build. Você deve ter acesso de gravação a esse diretório.  
  
 Digite o local como um caminho de disco, compartilhamento de arquivos, site FTP ou URL do site da web ou clique a **procurar** botão para procurar o local. O caminho pode ser nos seguintes formatos:  
  
- Um caminho relativo ou absoluto no padrão Windows Formatar, como *C:\Deploy\MyApplication* ou *\MyApplication*.  
  
- Um caminho de convenção de nomenclatura Universal (UNC), como  *\\\ServerName\MyApplication\\*.  
  
- Uma URL de uma web site, como http://www.microsoft.com/MyApplication.  
  
  Por padrão, é o local de publicação *http://localhost/projectname/* se tiver instalado o IIS ou o diretório de Publish se você fizer não tiver o IIS instalado.  
  
> [!NOTE]  
>  Existem considerações mais se o computador de destino está executando o Windows Vista. Você deve ser um administrador no computador Windows Vista para usar a opção de publicação local. Além disso, o local padrão é sempre o *publique\\*  diretório, independentemente de você ter instalado o IIS.  
  
## <a name="what-is-the-default-installation-path-on-end-user-computers"></a>O que é o caminho de instalação padrão em computadores de usuários finais?  
 O caminho de instalação é opcional. Se você preferir, você pode definir o caminho de instalação mais tarde. Para obter detalhes, consulte [como: alterar o caminho de instalação de uma solução do Office](https://msdn.microsoft.com/d0eaa07b-2d72-4902-899f-2f9fb165b8fd).  
  
 O caminho de instalação é o diretório do qual o usuário final instalará a personalização. Também é o caminho que a solução usará para verificar se há atualizações. O **Assistente de publicação** não implanta a solução para esse local, a menos que o caminho é o mesmo que você digitou na **especifique o local para publicar este aplicativo** caixa da página anterior.  
  
 **De um site da Web**  
 Especifique a URL que os usuários finais seguirá para instalar a solução.  
  
 **De um compartilhamento de arquivo ou caminho UNC**  
 Especifique o caminho UNC que os usuários finais seguirá para instalar a solução.  
  
 **De um CD-ROM ou DVD-ROM**  
 Essa opção não exige um caminho de instalação.  
  
 Visual Studio não gravar o CD ou DVD. Você deve copiar a saída para um CD ou DVD manualmente.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)   
 [Página de publicação, Designer de projeto &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/publish-page-project-designer-office-development-in-visual-studio.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)  
  
  