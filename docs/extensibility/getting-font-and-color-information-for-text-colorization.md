---
title: Obtendo informações de cores para colorização de texto e fonte | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- text, coloring
- font and color control [Visual Studio SDK], coloring
ms.assetid: d1f985bd-743e-40b7-9458-d9af53647c91
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1b9d5aa4c3f649f7be44db2e18f67884acd23201
ms.sourcegitcommit: 3dd15e019cba7d35dbabc1aa3bf55842a59f5278
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46370660"
---
# <a name="get-font-and-color-information-for-text-colorization"></a>Obter informações de fonte e cor para a colorização do texto
O processo que processa ou exibe texto coloridos serão em elementos de (UI) interface do usuário depende do tipo de projeto, sua tecnologia e desenvolvedor preferências. O **fontes e cores** página de propriedades armazena as configurações.

 A maioria das implementações que exibem texto coloridos serão precisa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> e associados a interfaces para as configurações de exibição de apresentação, recuperar e armazenar texto.

> [!NOTE]
>  Ao personalizar o editor principal (que oferece suporte a **EditorCategory texto**), é recomendável que você use a tecnologia de cores no serviço de linguagem. Para obter mais informações, consulte [visão geral de fontes e cores](../extensibility/font-and-color-overview.md).

## <a name="get-default-font-and-color-information"></a>Obter informações de fonte e cor padrão
 Todos os as **fontes e cores** configurações de qualquer janela de exibição de texto devem ser especificadas na **itens de exibição** de um **categoria**. Para obter mais informações, consulte [fontes e cores, ambiente, caixa de diálogo Opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md).

Para colorir, um VSPackage deverá obter o atual **fontes e cores** configurações. Um VSPackage pode obter as configurações atuais das seguintes maneiras, dependendo das suas necessidades:

-   Use o mecanismo de persistência de fontes e cores para recuperar o estado atual ou armazenado. Para obter mais informações, consulte [acesso armazenados configurações de fonte e cor](../extensibility/accessing-stored-font-and-color-settings.md).

-   Use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> interface de um serviço que fornece dados de fontes e cores para obter uma instância de <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>, se o VSPackage não é também o provedor de fonte e cor.

-   Implementar a interface <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>.

Para garantir que os resultados obtidos por meio de sondagem são atualizadas, talvez seja útil usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> interface para determinar se uma atualização é necessária antes de chamar os métodos de recuperação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface.

Depois que você obteve informações de fonte e cor, analisar o texto a ser exibido para identificar elementos que exigem a colorização. Exiba o texto na janela usando as cores e fontes apropriadas.

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>
- [Use fontes e texto](/dotnet/framework/winforms/advanced/using-fonts-and-text)
- [Trabalhar com cores](/cpp/windows/working-with-color-image-editor-for-icons)
- [GDI (interface gráfica de dispositivo)](https://msdn.microsoft.com/library/7e1d4540-bb2e-4257-8eee-eee376acba83)