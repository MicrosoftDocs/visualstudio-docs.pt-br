---
title: 'Como: configurar um computador para desenvolver soluções do Office'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- prerequisites [Office development in Visual Studio]
- Office development in Visual Studio, installing tools
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6a07545fb9a7ddb2fc70ba5053ad131d2e214636
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671307"
---
# <a name="how-to-configure-a-computer-to-develop-office-solutions"></a>Como: configurar um computador para desenvolver soluções do Office
  Para configurar um computador de desenvolvimento para que você pode usar o Microsoft Office developer tools no Visual Studio, siga as instruções neste tópico. Você deve ter privilégios administrativos no computador de desenvolvimento para executar essas etapas.  
  
### <a name="to-configure-the-development-computer"></a>Para configurar o computador de desenvolvimento  
  
1.  Instale uma versão do Visual Studio que inclui o Office developer tools. As ferramentas de desenvolvedor do Office são instaladas por padrão. Se você personalizar a instalação do Visual Studio, selecionando quais recursos serão instalados, verifique se **Microsoft Office Developer Tools** é selecionada durante a instalação. Para obter mais informações sobre as versões do Visual Studio que incluem o Office developer tools, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).  
  
2.  Instale uma versão do Office que é compatível com o Office developer tools no Visual Studio. Para obter mais informações, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).  
  
     Certifique-se de que você também pode instalar os PIAs para a versão do Office que você instalar. Por padrão, os PIAs são instalados com o Office. Se você modificar a instalação do Office, verifique se o **suporte à programação do .NET** está selecionado para os aplicativos de destino.  
  
3.  Se você tiver uma versão em inglês do Visual Studio, mas usa configurações diferentes do inglês para Windows, você pode instalar o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pacote de idiomas para ver [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] mensagens no mesmo idioma do Windows. Essas versões do Visual Studio instalam automaticamente o pacote de idiomas. O pacote de idiomas está disponível na [Centro de download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=140386).  
  
## <a name="see-also"></a>Consulte também  
 [O que há de novo no desenvolvimento do Office](https://msdn.microsoft.com/bf054af2-c896-4723-aa15-6381145b14bb)   
 [Introdução ao &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)   
 [Como: instalar o Visual Studio Tools for Office runtime redistribuível](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)   
 [Como: assemblies de interoperabilidade primários do Office de instalação](../vsto/how-to-install-office-primary-interop-assemblies.md)  
  
  