---
title: Usando navegadores diferentes com testes de interface do usuário codificada
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: f7301ef674e3ad3b940204be30bfffa878f88e45
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895100"
---
# <a name="use-different-web-browsers-with-coded-ui-tests"></a>Usar navegadores da Web diferentes com testes de IU codificados

Os testes de IU codificados podem automatizar testes para aplicativos Web gravando os testes usando o Internet Explorer. Você pode personalizar o teste e executá-lo usando o Internet Explorer ou outros tipos de navegador para esses aplicativos Web.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

Primeiro, instale os [Componentes do Selenium para testes de IU codificados entre navegadores](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting).

## <a name="whats-supported-across-all-web-browsers"></a>O que tem suporte em todos os navegadores da Web?

-   [Adicionar código personalizado para recursos de controle, ](https://blogs.msdn.microsoft.com/devops/2012/12/09/coded-ui-test-configuring-search-properties-while-recording-on-internet-explorer/)como propriedades, pesquisa e waiters de reprodução.

-   Pop-ups e caixas de diálogo

-   [Executar JavaScript básico sem tipo de retorno](https://blogs.msdn.microsoft.com/devops/2013/01/18/introducing-javascript-execution-on-internetexplorer-and-crossbrowser-in-coded-ui-test/)

-   Resiliência de pesquisa (usando smart match) e [melhorias de desempenho](https://blogs.msdn.microsoft.com/devops/2012/01/31/guidelines-on-improving-performance-of-coded-ui-test-playback/)

## <a name="why-should-i-use-coded-ui-tests-across-multiple-web-browser-types"></a>Por que eu deveria usar testes de IU codificados em vários tipos de navegadores da Web?

Testando seu aplicativo Web com uma variedade de tipos de navegadores da Web, você emula melhor a experiência de IU de seus usuários que podem usar navegadores diferentes. Por exemplo, o aplicativo pode incluir um controle ou um código no Internet Explorer que não seja compatível com outros navegadores da Web. Executando os testes de IU codificados em outros navegadores, você pode identificar e corrigir qualquer problema antes que isso afete seus clientes.

## <a name="how-do-i-record-and-play-back-coded-ui-tests-on-web-applications-using-the-supported-web-browsers"></a>Como faço para gravar e reproduzir testes de IU codificados em aplicativos Web usando os navegadores da Web com suporte?

**Gravação**: você deve usar o Construtor de teste de IU codificado para registrar o teste do aplicativo Web usando o Internet Explorer. Opcionalmente, você pode adicionar validação e código personalizado para os controles testados usando um conjunto predefinido de propriedades como você faria normalmente para testes de IU codificados. Para obter mais informações, confira [Usar a automação da interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md).

> [!NOTE]
> Você não pode gravar testes de IU codificados usando os navegadores Google Chrome ou Mozilla Firefox.

 **Reprodução com o Internet Explorer**: quando nenhum navegador é especificado, os testes são executados no Internet Explorer por padrão. Você pode declarar explicitamente o navegador a ser usado ao definir a propriedade **BrowserWindow.CurrentBrowser** no seu código de teste. Para o Internet Explorer, essa propriedade deve ser definida como **IE** ou **Internet Explorer**.

 **Reprodução com navegadores da Web diferentes do Internet Explorer**: para reproduzir em navegadores da Web diferentes do Internet Explorer, altere a propriedade BrowserWindow.CurrentBrowser no código de teste para **Firefox** ou **Chrome**.

 Para executar testes em navegadores da web que não sejam o IE, você deve instalar os **componentes Selenium para testes de IU codificados entre navegadores**.

### <a name="install-selenium-components"></a>Instalar componentes do Selenium

1.  No menu **Ferramentas**, escolha **Extensões e Atualizações**.

2.  Na caixa de diálogo **Extensões e Atualizações**, pesquise `Selenium components for Cross Browser Testing`.

3.  Realce a extensão e escolha **Baixar**.

    > [!TIP]
    > Você também pode baixar os componentes Selenium para testes de IU codificados entre navegadores [aqui](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting).

Para obter mais informações sobre como criar e usar testes de IU codificados, confira [Criar testes de IU codificados](../test/use-ui-automation-to-test-your-code.md).

### <a name="enable-debugging"></a>Habilitar a depuração

Para habilitar a depuração em seu aplicativo Web, conclua as seguintes opções de configuração:

1.  Habilitar Apenas Meu Código:

    1.  No menu **Ferramentas**, escolha **Opções** e, então, **Depuração**.

    2.  Selecione **Habilitar Apenas Meu Código**.

2.  Desabilitar exceções CLR:

    1.  No menu **Depurar**, escolha **Exceções**.

    2.  Para **exceções de Common Language Runtime**, desmarque **Sem tratamento do usuário**.

Se não vir a opção para alterar `BrowserWindow.CurrentBrowser` no teste de IU codificado, talvez você esteja usando uma versão do Visual Studio sem suporte para testes de IU codificados usando vários navegadores da Web. Para usar tais testes de IU codificados, é necessário usar a edição Visual Studio Enterprise.

Estas são algumas outras coisas que você precisa saber:

- O navegador da Web Apple Safari não tem suporte.

- A ação de iniciar o navegador da Web deve fazer parte de teste de IU codificado.

   Se você tiver um navegador da Web já aberto e quiser executar etapas nele, a reprodução falhará a menos que você esteja usando o Internet Explorer. Consequentemente, é uma prática recomendada incluir a inicialização do navegador da Web como parte dos testes de IU codificados.

- Não há suporte para automatizar ações de IU baseadas em navegadores específicos, como maximizar, minimizar e restaurar.

## <a name="tips"></a>Dicas

Você pode configurar a saída para incluir capturas de tela nos logs de IU codificados. Para fazer isso, você precisa definir algumas configurações no arquivo *QTAgent32.exe.config*. Por padrão, esse arquivo é instalado no seguinte local:

*%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE*

Defina os seguintes valores:

- `EqtTraceLevel` na seção `system.diagnostics`.

- `<add name="EqtTraceLevel" value="4" />`

   Definindo o valor como 3 ou mais, são feitas capturas de tela para cada ação. Quando o valor é definido para 1 ou 2, as capturas de tela são feitas apenas para ações de erro.

Para obter mais informações, confira [Analisar testes de IU codificados usando logs de teste de IU codificado](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md).

## <a name="video-resources"></a>Recursos em vídeo

 [Gravar no IE e reproduzir em qualquer lugar](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!183&authkey=!ANqaLtCZbtJrImU)

 [Criar testes entre navegadores com construtor de teste de IU codificado](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!184&authkey=!AKG8CSow_qmeTq8)

 [Criar testes entre navegadores de autor usando codificação manual básica sem mapa da IU](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!186&authkey=!AJaEvxJnsefyAT4)

 [Executar testes entre navegadores sequencialmente em vários navegadores](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!187&authkey=!ADI8eCQkxHnpOR8)

 [Solucionar problemas de falhas de teste entre navegadores](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!182&authkey=!AEpS48i295B49FI)

## <a name="see-also"></a>Consulte também

- [Usar a automação de interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md)
- [Configurações e plataformas compatíveis para testes de IU codificados e gravações de ação](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
- [Analisar testes de IU codificados usando logs de teste de IU codificado](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)
