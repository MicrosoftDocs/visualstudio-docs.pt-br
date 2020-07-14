---
title: Caixa de diálogo Pré-requisitos
ms.date: 06/29/2018
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- Microsoft.VisualStudio.Publish.BaseProvider.Dialog.Bootstrapper
helpviewer_keywords:
- Prerequisites dialog box
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cf555a9a4b7c73e4e204bcc42e6b57d3ab96cd01
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419166"
---
# <a name="prerequisites-dialog-box"></a>Caixa de diálogo Pré-requisitos

A caixa de diálogo **Pré-requisitos** especifica quais componentes de pré-requisito são instalados, como eles são instalados e em qual ordem os pacotes são instalados.

![Caixa de diálogo Pré-requisitos no Visual Studio](media/prerequisites-dialog-box.png)

Para acessar a caixa de diálogo, selecione um nó do projeto no **Gerenciador de Soluções** e, em seguida, selecione **Projeto** > **Propriedades**. Quando o **Designer de Projeto** for exibido, selecione a guia **Publicar** e, em seguida, selecione **Pré-requisitos**. Para projetos de Instalação, no menu **Projeto**, clique em **Propriedades**. Quando a caixa de diálogo **Páginas de Propriedades** for exibida, clique em **Pré-requisitos**.

## <a name="uielement-list"></a>Lista de elementos de interface do usuário

|Elemento|Descrição|
|-------------|-----------------|
|**Criar programa de instalação para instalar os componentes de pré-requisitos**|Inclui os componentes de pré-requisito no programa de instalação do aplicativo (*Setup.exe*) para que eles sejam instalados antes do aplicativo, na ordem de dependência. Por padrão, essa opção é selecionada. Se ela não for selecionada, não será criado nenhum *Setup.exe*.|
|**Escolher quais pré-requisitos serão instalados**|Especifica se componentes, como bibliotecas de runtime do .NET Framework e do C++, devem ser instalados.<br /><br />Por exemplo, ao marcar a caixa de seleção ao lado de **SQL Server 2012 Express**, você especifica que o programa de instalação precisa verificar se esse componente está instalado no computador de destino e instalá-lo caso não esteja.<br /><br />Para obter informações detalhadas sobre cada pacote de pré-requisitos, confira [Informações de pré-requisitos](#prerequisites-information).|
|**Baixar os pré-requisitos no site do fornecedor do componente**|Especifica que os componentes de pré-requisitos são instalados por meio do site do fornecedor. Essa é a opção padrão.|
|**Baixar os pré-requisitos no mesmo local do meu aplicativo**|Especifica que os componentes de pré-requisitos são instalados por meio do mesmo local que o aplicativo. Isso copia todos os pacotes de pré-requisitos no local de publicação. Para que essa opção funcione, os pacotes do pré-requisito devem estar no computador de desenvolvimento.|
|**Baixar os pré-requisitos no seguinte local**|Especifica que os componentes de pré-requisitos são instalados pelo local inserido. É possível usar o botão **Procurar** para selecionar um local.|

> [!NOTE]
> Para obter informações sobre onde colocar os pré-requisitos, confira [Criar pacotes de bootstrapper](../../deployment/creating-bootstrapper-packages.md#create-custom-bootstrapper-packages).

## <a name="prerequisites-information"></a>Informações de pré-requisitos

Os componentes de pré-requisitos exibidos na caixa de diálogo **Pré-requisitos** podem ser diferentes daqueles da lista a seguir. Os pacotes de pré-requisitos listados na **Caixa de diálogo Pré-requisitos** são definidos automaticamente na primeira vez em que a caixa de diálogo é aberta. Se você alterar a estrutura de destino do projeto mais tarde, será necessário selecionar os pré-requisitos manualmente para corresponder à nova estrutura de destino.

|Elemento|Descrição|
|-------------|-----------------|
|**.NET Framework 3.5 SP1**|Esse pacote instala o seguinte:<br /><br /> -   .NET Framework versões 2.0, 3.0 e 3.5.<br />-   Suporte para todas as versões do .NET Framework em sistemas operacionais de 32 bits (x86) e 64 bits (x64).<br />-   Pacotes de idiomas para cada versão do .NET Framework que é instalada com o pacote.<br />-   Service packs para o .NET Framework 2.0 e 3.0.<br /><br /> O .NET Framework 3.0 está incluído no Windows Vista e o .NET Framework 3.5 está incluído no Visual Studio. O .NET Framework 3.5 é necessário para todos os projetos do Visual Basic e C# que são compilados para sistemas operacionais de 32 bits e para quais a estrutura de destino é definida como **.NET Framework 3.5**, bem como para projetos do Visual Basic e C# compilados para sistemas operacionais de 64 bits. (Não há suporte para IA64.) Observe que os projetos Visual Basic e C# são compilados para qualquer arquitetura de CPU por padrão. Para obter mais informações, confira [Visão geral do direcionamento de estrutura](../../ide/visual-studio-multi-targeting-overview.md) e [Pré-requisitos de implantação para aplicativos de 64 bits](../../deployment/deploying-prerequisites-for-64-bit-applications.md).|
|**Microsoft .NET Framework 4.x**|Esse pacote instala o .NET Framework 4.x para as plataformas x86 e x64.|
|**Microsoft System CLR Types para SQL Server 2014 (x64 e x86)**|Este pacote instala o Microsoft System CLR Types para SQL Server 2014 para x64 ou x86.|
|**SQL Server 2008 R2 Express**|Esse pacote instala o Microsoft SQL Server 2008 R2 Express, uma edição gratuita do Microsoft SQL Server 2008 R2, um banco de dados ideal para aplicativos Web, de servidor ou de área de trabalho pequenos. Pode ser usado gratuitamente para desenvolvimento e produção.|
|**SQL Server 2012 Express**|Este pacote instala o Microsoft SQL Server 2012 Express.|
|**SQL Server 2012 Express LocalDB**|Este pacote instala o Microsoft SQL Server 2012 Express LocalDB.|
|**Bibliotecas de Runtime do Visual C++ "14" (ARM)**|Esse pacote instala as bibliotecas em tempo de execução Visual C++ para a arquitetura Itanium, que fornecem rotinas de programação para o sistema operacional Microsoft Windows. Essas rotinas automatizam várias tarefas comuns de programação que não são fornecidas pelas linguagens C e C++.<br /><br /> Para obter mais informações, consulte [Referência da biblioteca em tempo de execução C](/cpp/c-runtime-library/c-run-time-library-reference).|
|**Bibliotecas de Runtime do Visual C++ "14" (x64)**|Esse pacote instala as bibliotecas em tempo de execução Visual C++ para os sistemas operacionais x64, que fornecem rotinas de programação para o sistema operacional Microsoft Windows. Essas rotinas automatizam várias tarefas comuns de programação que não são fornecidas pelas linguagens C e C++.<br /><br /> Para obter mais informações, consulte [Referência da biblioteca em tempo de execução C](/cpp/c-runtime-library/c-run-time-library-reference).|
|**Bibliotecas de Runtime do Visual C++ "14" (x86)**|Esse pacote instala as bibliotecas em tempo de execução Visual C++ para os sistemas operacionais x86, que fornecem rotinas de programação para o sistema operacional Microsoft Windows. Essas rotinas automatizam várias tarefas comuns de programação que não são fornecidas pelas linguagens C e C++.<br /><br /> Para obter mais informações, consulte [Referência da biblioteca em tempo de execução C](/cpp/c-runtime-library/c-run-time-library-reference).|

## <a name="see-also"></a>Veja também

- [Página de Publicação, Designer de Projeto](../../ide/reference/publish-page-project-designer.md)
- [Pré-requisitos de implantação de aplicativo](../../deployment/application-deployment-prerequisites.md)
- [Implantando pré-requisitos para aplicativos de 64 bits](../../deployment/deploying-prerequisites-for-64-bit-applications.md)
- [Visão geral do direcionamento de estrutura](../../ide/visual-studio-multi-targeting-overview.md)
