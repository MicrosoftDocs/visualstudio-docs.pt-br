---
title: Estender testes de IU codificados e gravações da ação
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: cbf4d89fc0a32501a2ea275c5168969dd2a0fd19
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894112"
---
# <a name="extend-coded-ui-tests-and-action-recordings"></a>Estender testes de IU codificados e gravações da ação

A estrutura de teste para testes de IU codificados e gravações da ação não dá suporte a todas as interfaces do usuário possíveis. Ele pode não dar suporte à interface do usuário específica que você deseja testar. Por exemplo, não é possível criar imediatamente um teste de IU codificado ou uma gravação da ação para uma planilha do Microsoft Excel. No entanto, é possível criar sua própria extensão para a estrutura de teste de IU codificado compatível com a interface do usuário específica, aproveitando a extensibilidade da estrutura do teste de IU codificado.

![Arquitetura de teste de IU](../test/media/ui_testarch.png)

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="sample-extension-to-test-microsoft-excel"></a>Extensão de exemplo para testar o Microsoft Excel

Essa [postagem no blog](https://blogs.msdn.microsoft.com/gautamg/2010/01/05/3-introducing-sample-excel-extension/) contém um link para uma [extensão de exemplo](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Components.PostAttachments/00/09/94/38/24/ExcelPluginSample.zip) para a estrutura do teste de IU codificado. Também é possível exibir toda a [série de postagens no blog para extensibilidade do teste de IU codificado](https://blogs.msdn.microsoft.com/gautamg/2010/01/05/series-on-coded-ui-test-extensibility/).

> [!NOTE]
> A amostra é destinada para uso com o Microsoft Excel 2010. Ela pode funcionar ou não com outras versões do Excel.

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>
- [Usar a automação de interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md)
- [Práticas recomendadas para testes de IU codificados](../test/best-practices-for-coded-ui-tests.md)
- [Configurações e plataformas compatíveis para testes de IU codificados e gravações de ação](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)