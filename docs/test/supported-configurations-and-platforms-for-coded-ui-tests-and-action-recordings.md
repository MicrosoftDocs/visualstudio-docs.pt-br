---
title: Configurações e plataformas para testes de interface do usuário codificados
description: Este artigo contém as configurações e plataformas com suporte para testes de interface do usuário codificados para Visual Studio Enterprise.
ms.custom: SEO-VS-2020
ms.date: 10/04/2015
ms.topic: reference
helpviewer_keywords:
- coded UI tests
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: ddad690c98b3516586b769e57721da8760b28b75
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894537"
---
# <a name="supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings"></a>Configurações e plataformas compatíveis com testes de IU codificados e gravações de ação

As configurações e as plataformas de testes de IU codificados com suporte no Visual Studio Enterprise são listadas na tabela a seguir. Essas configurações também se aplicam às gravações de ação criadas usando o [!INCLUDE[MTRlong](../test/includes/mtrlong_md.md)].

> [!NOTE]
> O processo de teste de IU codificado deve ter os mesmos privilégios que o aplicativo testado.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**Requirements**

- Visual Studio Enterprise

## <a name="supported-configurations"></a>Configurações com suporte

| Configuração | Suportado |
|-| - |
| Sistemas operacionais | [!INCLUDE[win7](../debugger/includes/win7_md.md)]<br /><br /> [!INCLUDE[winsvr08_r2](../debugger/includes/winsvr08_r2_md.md)]<br /><br /> [!INCLUDE[win8](../debugger/includes/win8_md.md)]<br /><br /> Windows 10 |
| Suporte para 32 bits/64 bits | O Windows de 32 bits que está executando o [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] de 32 bits pode testar aplicativos de 32 bits.<br /><br /> O Windows de 64 bits que está executando o [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] de 32 bits pode testar os aplicativos WOW de 32 bits que têm Sincronização de IU.<br /><br /> O Windows de 64 bits que está executando o [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] de 32 bits pode testar aplicativos do Windows Forms e do WPF que não têm Sincronização de IU. |
| Arquitetura | x86 e x64 **Observação:** não há suporte para o Internet Explorer no modo de 64 bits, exceto quando executado no [!INCLUDE[win8](../debugger/includes/win8_md.md)] ou em versões posteriores. |
| .NET | .NET 2.0, 3.0, 3.5, 4 e 4.5. **Observação: o**  [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] e o Visual Studio exigirão o .NET 4 para funcionar. No entanto, há suporte para os aplicativos desenvolvidos usando as versões listadas do .NET. |

> [!NOTE]
> *Sincronização de interface do usuário* é um recurso em que a reprodução é verificada na fila de mensagens de cada controle. Se um controle não respondeu ao evento enviado para ele, o evento será enviado novamente.

## <a name="platform-support"></a>Suporte a plataforma

| Plataforma | Nível de suporte |
|-| - |
| Aplicativos do Windows Phone | Somente aplicativos do Phone com base em WinRT-XAML são compatíveis. |
| Aplicativos UWP | Somente aplicativos UWP baseados em XAML são compatíveis. |
| Aplicativos universais do Windows | Há suporte para Aplicativos Universais do Windows baseados em XAML somente no Windows Phone e Desktop. |
| Edge | Não há suporte para a gravação de etapas da ação ou uso do construtor para exibir as propriedades do objeto. Os testes podem ser reproduzidos no navegador Edge, usando a atualização 2 do Visual Studio 2015 e versões posteriores usando a [extensão de teste entre navegadores de interface do usuário codificada](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting). |
| Internet Explorer 8<br /><br /> Internet Explorer 9<br /><br /> Internet Explorer 10 **Importante:** há suporte para o Internet Explorer 10 somente na área de trabalho. <br /><br /> Internet Explorer 11 **Importante:** há suporte para o Internet Explorer 11 somente na área de trabalho. | Suporte total.<br /><br /> -   **Suporte para HTML5 no Internet Explorer 9 e Internet Explorer 10:** registro de suporte de testes de IU codificados, reprodução e validação dos controles HTML5: Audio, Video, ProgressBar e Slider. Para obter mais informações, consulte [usando controles HTML5 em testes de interface do usuário codificados](../test/using-html5-controls-in-coded-ui-tests.md). **Aviso:**      se você criar testes de IU codificados no Internet Explorer 10, eles poderão não ser executados no Internet Explorer 9 ou no Internet Explorer 8. Isso ocorre porque o Internet Explorer 10 inclui controles HTML5, como Audio, Video, ProgressBar e Slider. Esses controles HTML5 não são reconhecidos pelo Internet Explorer 9 ou pelo Internet Explorer 8. Da mesma forma, seu teste de IU codificado usando o Internet Explorer 9 pode incluir alguns controles do HTML5 que também não serão reconhecidos pelo Internet Explorer 8.<br />-   **Suporte para verificação ortográfica do Internet Explorer 10:** o Internet Explorer 10 inclui funcionalidades de verificação ortográfica para todas as caixas de texto. Isso permite que você escolha entre uma lista de correções sugeridas. O Teste de IU Codificado ignorará essas ações do usuário, como a seleção de uma sugestão de ortografia alternativa. Será gravado apenas o texto digitado final na caixa de texto.<br />     As seguintes ações são registradas para o teste de IU codificado que usa o controle de verificação ortográfica: Adicionar ao Dicionário, Copiar, Selecionar Tudo, Adicionar ao Dicionário e Ignorar.<br />-   **Suporte para Internet Explorer de 64 bits executado no Windows 8:** anteriormente, não havia suporte para versões de 64 bits do Internet Explorer para gravação e reprodução. Com o [!INCLUDE[win8](../debugger/includes/win8_md.md)] e o [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)], os testes de IU codificados foram habilitados para versões de 64 bits do Internet Explorer. **Aviso:** o suporte de 64 bits para o Internet Explorer se aplica somente quando você executa o [!INCLUDE[win8](../debugger/includes/win8_md.md)] ou posterior.<br />-   **Suporte para sites fixos no Internet Explorer 9:** no Internet Explorer 9, foram introduzidos sites fixos. Com os sites fixos, você pode acessar seus sites favoritos diretamente da barra de tarefas do Windows, sem ter de abrir o Internet Explorer primeiro. Os testes de IU codificados agora podem gerar ações intencionais em sites fixos. Para obter mais informações sobre sites fixos, consulte [sites fixos](https://support.microsoft.com/hub/4230784/internet-explorer-help).<br />-   **Suporte para marcas semânticas do Internet Explorer 9:** o Internet Explorer 9 introduziu as seguintes marcas semânticas: section, nav, article, aside, hgroup, header, footer, figure, figcaption e mark. Os testes de IU codificados ignoram todas essas marcas semânticas durante a gravação. Você pode adicionar asserções nessas marcas usando o Construtor de Teste de IU Codificado. Você pode usar o seletor de navegação no Construtor de Teste de IU Codificado para navegar para qualquer um desses elementos e exibir suas propriedades.<br />-   **Tratamento direto de caracteres de espaço em branco entre versões do Internet Explorer:** há diferenças no tratamento de caracteres de espaço em branco entre o Internet Explorer 8, o Internet Explorer 9 e o Internet Explorer 10. O Teste de IU Codificado trata dessas diferenças perfeitamente. Portanto, um teste de IU codificado criado no Internet Explorer 8, por exemplo, executará com êxito no Internet Explorer 9 e no Internet Explorer 10.<br />-   **A área de notificação do Internet Explorer agora está gravada com o conjunto de atributos "continuar se houver erro":** Todas as ações na área de notificação do Internet Explorer agora estão gravadas com o conjunto de atributos "continuar no erro". Se a barra de notificação não aparecer durante a reprodução, as ações nela serão ignoradas e o teste de IU codificado continuará com a próxima ação. |
| Controles de terceiros no Windows Forms e no WPF | Suporte total.<br /><br /> Para habilitar os controles de terceiros em aplicativos do Windows Forms e do WPF, você deve adicionar referências e código. Para obter mais informações, consulte [habilitar teste de interface do usuário codificado de seus controles](../test/enable-coded-ui-testing-of-your-controls.md). |
| Internet Explorer 6<br /><br /> Internet Explorer 7 | Não há suporte. |
| Chrome<br /><br /> Firefox | Não há suporte para a gravação de etapas de ação. Os testes de IU codificados podem ser executados novamente nos navegadores Chrome e Firefox com a Atualização 4 do Visual Studio 2012 ou posterior. Acesse [aqui](using-different-web-browsers-with-coded-ui-tests.md) para obter mais detalhes. |
| Opera<br /><br /> Safari | Não há suporte. |
| Silverlight | Não há suporte.<br /><br /> No entanto, para o Visual pino 2013, você pode baixar o [plug-in de teste de interface do usuário codificado do Microsoft Visual Studio 2013 para o Silverlight](https://marketplace.visualstudio.com/items?itemName=PrachiBoraMSFT.MicrosoftVisualStudio2013CodedUITestPluginforSilve) na galeria do Visual Studio. |
| Flash/Java | Não há suporte. |
| Windows Forms 2.0 e posterior | Suporte total. **Observação:** os controles NetFx têm suporte completo, mas nem todos os controles de terceiros têm suporte. |
| WPF 3.5 e posterior | Suporte total.<br /><br /> **Observação** Os controles NetFx têm suporte total, mas nem todos os controles de terceiros têm suporte. |
| Windows Win32 | Pode funcionar com alguns problemas conhecidos, mas sem suporte oficial. |
| MFC | Suporte parcial. Consulte a [estrutura de UITest](/archive/blogs/vstsqualitytools/uitest-framework-mfc-support-in-vs-2010) para obter detalhes sobre quais recursos têm suporte. |
| SharePoint | Suporte total. |
| Aplicativos clientes do Office | Não há suporte. |
| Cliente Web do Dynamics CRM | Suporte total. |
| Cliente do Dynamics (Ax) 2012 | A gravação e reprodução de ações têm suporte parcial. Consulte [suporte a gravações de IU/ações codificadas do Visual Studio 10 para o Microsoft Dynamics](/archive/blogs/dave_froslie/visual-studio-10-coded-ui-action-recordings-support-for-microsoft-dynamics-ax-2012) para obter detalhes. |
| SAP | Não há suporte. |
| Citrix/Serviços de Terminal | Não recomendamos ações de gravação em um servidor Host da Sessão da Área de Trabalho Remota. O gravador não dá suporte à execução de várias instâncias ao mesmo tempo. |
| PowerBuilder | Suporte parcial.<br /><br /> O suporte é habilitado na acessibilidade de extensões para controles PowerBuilder. |

Para obter informações sobre como criar extensões para dar suporte a outras plataformas, confira [Habilitar testes de IU codificados dos controles](../test/enable-coded-ui-testing-of-your-controls.md) e [Estender testes de IU codificados e gravações de ação](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md).

## <a name="see-also"></a>Confira também

- [Usar a automação da interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)