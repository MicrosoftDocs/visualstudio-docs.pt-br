---
title: Configurar um computador para desenvolver soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, installing tools
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 19c7e012775ff1a761b5c267f05b8f7ff250d5c6
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672220"
---
# <a name="configure-a-computer-to-develop-office-solutions"></a>Configurar um computador para desenvolver soluções do Office

Para criar suplementos do VSTO e personalizações para o Microsoft Office, instale uma versão compatível do Visual Studio, o .NET Framework e o Microsoft Office.

|Software|Versões com suporte|
|--------------|------------------------|
|Visual Studio 2017| Qualquer edição com o **desenvolvimento do Office/SharePoint** carga de trabalho.|
|.NET Framework|– O .NET Framework 4 ou posterior.|
|Microsoft Office|<ul><li>Qualquer edição do pacote do Office, incluindo o Office Professional Plus do Office 365.</li><li>Qualquer uma das aplicações autônomas seguintes:<br /><br /> <ul><li>Excel</li><li>InfoPath (Office 2013 e Office 2010 apenas)</li><li>Outlook</li><li>PowerPoint</li><li>Projeto</li><li>Visio</li><li>Palavra</li></ul></li></ul><br /> O Visual Basic for Applications (VBA) deve ser instalado como parte do Office. **Importante:** Click-to-Run versões de aplicativos do Office 2010 não são suportadas.|

Para obter etapas detalhadas de instalação, consulte [como: configurar um computador para desenvolver soluções do Office](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md).

## <a name="if-project-templates-dont-appear-or-they-dont-work-in-visual-studio"></a>Se os modelos de projeto não são exibidos ou não funcionam no Visual Studio

Se você instalar uma versão compatível do Visual Studio, o .NET Framework e o Microsoft Office, mas os modelos de projeto do Office não são exibidos no Visual Studio **novo projeto** caixa de diálogo, ou você recebe um erro ao tentar usar um, Verifique o seguinte:

- Certifique-se de que o Microsoft Office Developer Tools esteja instalado no computador.

     Ferramentas de desenvolvedor do Office são um componente opcional do Visual Studio, mas eles são instalados automaticamente juntamente com o Visual Studio. Se você personalizar a instalação do Visual Studio especificando quais recursos instalar, certifique-se de que você escolhe **Microsoft Office Developer Tools** durante a instalação para instalar as ferramentas.

     Para certificar-se de que essas ferramentas são instaladas, inicie o programa de instalação do Visual Studio e escolha o **modificar** botão. Selecione o **Microsoft Office Developer Tools** caixa de seleção e, em seguida, escolha o **atualização** botão.

- Certifique-se de que você não estiver executando uma versão do Office que foi entregue por clique para executar. Ver [como: verificar se o Outlook é um aplicativo de clique para executar em um computador](/previous-versions/office/developer/office-2010/ff864733(v=office.14)).

- Certifique-se de que está executando apenas uma versão do Microsoft Office.

Se você continuar a ter problemas, consulte [suporte adicional para erros em soluções do Office](../vsto/additional-support-for-errors-in-office-solutions.md).

## <a name="see-also"></a>Consulte também

[Introdução ao &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)  
[Como: configurar um computador para desenvolver soluções do Office](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)  
[Como: instalar o Visual Studio Tools for Office runtime redistribuível](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)  
[Como: assemblies de interoperabilidade primários do Office de instalação](../vsto/how-to-install-office-primary-interop-assemblies.md)  
[Recursos disponíveis por tipo de projeto e aplicativo do Office](../vsto/features-available-by-office-application-and-project-type.md)
