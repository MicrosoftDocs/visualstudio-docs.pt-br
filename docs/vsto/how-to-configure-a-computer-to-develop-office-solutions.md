---
title: Como configurar um computador para desenvolver soluções do Office
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- prerequisites [Office development in Visual Studio]
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3b13aa65e4dd5868a36e0dd833351b1d1751d8b0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546166"
---
# <a name="how-to-configure-a-computer-to-develop-office-solutions"></a>Como configurar um computador para desenvolver soluções do Office
  Para configurar um computador de desenvolvimento para que você possa usar as ferramentas de desenvolvedor do Microsoft Office no Visual Studio, siga as instruções neste tópico. Você deve ter privilégios administrativos no computador de desenvolvimento para executar essas etapas.

### <a name="to-configure-the-development-computer"></a>Para configurar o computador de desenvolvimento

1. Instale uma versão do Visual Studio que inclua as ferramentas de desenvolvedor do Office. As ferramentas de desenvolvedor do Office são instaladas por padrão. Se você personalizar a instalação do Visual Studio selecionando os recursos a serem instalados, verifique se **Microsoft Office ferramentas para desenvolvedores** está selecionada durante a instalação. Para obter mais informações sobre as versões do Visual Studio que incluem as ferramentas de desenvolvedor do Office, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).

2. Instale uma versão do Office com suporte nas ferramentas de desenvolvedor do Office no Visual Studio. Para obter mais informações, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).

     Certifique-se de também instalar os PIAs para a versão do Office que você instalar. Os PIAs são instalados com o Office por padrão. Se você modificar a instalação do Office, verifique se o recurso de **suporte de programação .net** está selecionado para os aplicativos que você deseja direcionar.

3. Se você tiver uma versão em inglês do Visual Studio, mas usar configurações que não sejam do inglês para o Windows, poderá instalar o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pacote de idiomas para ver [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] as mensagens no mesmo idioma que o Windows. Versões diferentes do inglês do Visual Studio instalam automaticamente o pacote de idiomas. O pacote de idiomas está disponível no [centro de download da Microsoft](https://www.microsoft.com/download/details.aspx?id=54246).

## <a name="see-also"></a>Consulte também

- [Introdução &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Como instalar o Ferramentas do Visual Studio para o Office Runtime Redistributable](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [Como instalar assemblies de interoperabilidade primária do Office](../vsto/how-to-install-office-primary-interop-assemblies.md)
