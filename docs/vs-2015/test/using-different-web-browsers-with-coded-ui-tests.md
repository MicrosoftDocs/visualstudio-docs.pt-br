---
title: Uso de navegadores da Web diferentes com testes de IU codificados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a859595f-6517-43f2-9d61-c706cb55a388
caps.latest.revision: 25
ms.author: gewarren
manager: douge
ms.openlocfilehash: e9e540e35bdfd68d8c371c2bad0ace3fc4b420e0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49893228"
---
# <a name="using-different-web-browsers-with-coded-ui-tests"></a>Usando navegadores diferentes com testes de interface do usuário codificada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os testes de IU codificados podem automatizar testes para aplicativos Web gravando os testes usando o Internet Explorer. Você pode personalizar o teste e executá-lo usando o Internet Explorer ou outros tipos de navegador para esses aplicativos Web.  
  
 **Requisitos**  
  
- Visual Studio Enterprise  
  
- Sistemas operacionais:  
  
  -   Microsoft Windows 7  
  
  -   Microsoft Windows 8  
  
  -   Microsoft Windows Server 2008 R2 SP1  
  
- Versões de navegadores da Web:  
  
  -   Windows Internet Explorer 9  
  
  -   Windows Internet Explorer 10  
  
  -   Para versões com suporte do Mozilla Firefox e do Google Chrome, acesse [aqui](http://visualstudiogallery.msdn.microsoft.com/11cfc881-f8c9-4f96-b303-a2780156628d/)  
  
- Instale os [componentes Selenium para testes de IU codificados entre navegadores](http://visualstudiogallery.msdn.microsoft.com/11cfc881-f8c9-4f96-b303-a2780156628d/).  
  
  **O que tem suporte por todos os navegadores da Web?**  
  
- [Adicionar código personalizado para recursos de controle, ](http://blogs.msdn.com/b/visualstudioalm/archive/2012/12/10/coded-ui-test-configuring-search-properties-while-recording-on-internet-explorer.aspx)como propriedades, pesquisa e waiters de reprodução.  
  
- Pop-ups e caixas de diálogo  
  
- [Executar JavaScript básico sem tipo de retorno](http://blogs.msdn.com/b/visualstudioalm/archive/2013/01/18/introducing-jscript-execution-on-internetexplorer-and-crossbrowser-in-coded-ui-test.aspx)  
  
- Resiliência de pesquisa (usando smart match) e [melhorias de desempenho](http://blogs.msdn.com/b/visualstudioalm/archive/2012/02/01/guidelines-on-improving-performance-of-coded-ui-test-playback.aspx)  
  
## <a name="why-should-i-use-coded-ui-tests-across-multiple-web-browser-types"></a>Por que eu deveria usar testes de IU codificados em vários tipos de navegadores da Web?  
 Testando seu aplicativo Web com uma variedade de tipos de navegadores da Web, você emula melhor a experiência de IU de seus usuários que podem usar navegadores diferentes. Por exemplo, o aplicativo pode incluir um controle ou um código no Internet Explorer que não seja compatível com outros navegadores da Web. Executando os testes de IU codificados em outros navegadores, você pode identificar e corrigir qualquer problema antes que isso afete seus clientes.  
  
## <a name="how-do-i-record-and-play-back-coded-ui-tests-on-web-applications-using-the-supported-web-browsers"></a>Como faço para gravar e reproduzir testes de IU codificados em aplicativos Web usando os navegadores da Web com suporte?  
 **Gravação**: você deve usar o Construtor de teste de IU codificado para registrar o teste do aplicativo Web usando o Internet Explorer. Opcionalmente, você pode adicionar validação e código personalizado para os controles testados usando um conjunto predefinido de propriedades como você faria normalmente para testes de IU codificados. Para obter mais informações, confira [Uso da automação da interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md).  
  
> [!NOTE]
>  Você não pode gravar testes de IU codificados usando os navegadores Google Chrome ou Mozilla Firefox.  
  
 **Reprodução com o Internet Explorer**: quando nenhum navegador é especificado, os testes são executados no Internet Explorer por padrão. Você pode declarar explicitamente o navegador a ser usado ao definir a propriedade **BrowserWindow.CurrentBrowser** no seu código de teste. Para o Internet Explorer, essa propriedade deve ser definida como **IE** ou **Internet Explorer**.  
  
 **Reprodução com navegadores da Web diferentes do Internet Explorer**: para reproduzir em navegadores da Web diferentes do Internet Explorer, altere a propriedade BrowserWindow.CurrentBrowser no código de teste para **Firefox** ou **Chrome**.  
  
 Para executar testes em navegadores da web que não sejam o IE, você deve instalar os **componentes Selenium para testes de IU codificados entre navegadores**.  
  
#### <a name="installing-selenium-components"></a>Instalando componentes Selenium  
  
1. No menu **Ferramentas**, escolha **Extensões e Atualizações**.  
  
2. Na caixa de diálogo Extensões e Atualizações, pesquise `Selenium components for Cross Browser Testing`.  
  
3. Realce a extensão e escolha **Baixar**.  
  
   > [!TIP]
   >  Você também pode baixar os componentes Selenium para testes de IU codificados entre navegadores [aqui](http://visualstudiogallery.msdn.microsoft.com/11cfc881-f8c9-4f96-b303-a2780156628d/).  
  
   Para obter mais informações sobre a criação e o uso de testes de IU codificados, confira [Criação de testes de IU codificados](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate).  
  
### <a name="enable-debugging"></a>Habilitar a depuração  
 Para habilitar a depuração em seu aplicativo Web, conclua as seguintes opções de configuração:  
  
1.  Habilitar Apenas Meu Código:  
  
    1.  No menu **Ferramentas**, escolha **Opções** e, então, **Depuração**.  
  
    2.  Selecione **Habilitar Apenas Meu Código**.  
  
2.  Desabilitar exceções CLR:  
  
    1.  No menu **Depurar**, escolha **Exceções**.  
  
    2.  Para **exceções de Common Language Runtime**, desmarque **Sem tratamento do usuário**.  
  
##  <a name="generate"></a> *Não vejo a opção para alterar BrowserWindow.CurrentBrowser no teste de IU codificado.*  
 Você pode usar uma versão do [!INCLUDE[vs2011_first](../includes/vs2011-first-md.md)] que não oferece suporte a testes de IU codificados usando vários navegadores da Web. Para usar tais testes de IU codificados, você precisa usar o Visual Studio Enterprise.  
  
 *O que mais eu deveria saber?*  
 **Observações**  
  
- ![Prerequsite](../test/media/prereq.png "Prereq") não há suporte para o navegador Safari da Apple.  
  
- ![Prerequsite](../test/media/prereq.png "Prereq") A ação de iniciar o navegador deve fazer parte do teste de IU codificado.  
  
   Se você tiver um navegador da Web já aberto e quiser executar etapas nele, a reprodução falhará a menos que você esteja usando o Internet Explorer. Consequentemente, é uma prática recomendada incluir a inicialização do navegador da Web como parte dos testes de IU codificados.  
  
- ![Prerequsite](../test/media/prereq.png "Prereq") Não há suporte para automatizar ações de IU baseadas em navegadores específicos, como maximizar, minimizar e restaurar.  
  
  **Dicas**  
  
- ![Tip](../test/media/tip.png "Tip") Você pode configurar a saída para incluir capturas de tela nos logs de IU codificados. Para fazer isso, você precisa definir algumas configurações no arquivo QTAgent32.exe.config. Por padrão, esse arquivo é instalado no seguinte local:  
  
   **C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE**  
  
   Defina os seguintes valores:  
  
  - `EqtTraceLevel` na seção `system.diagnostics`.  
  
  - `<add name="EqtTraceLevel" value="4" />`  
  
     Definindo o valor para 3 ou mais, as captura de tela são tiradas para cada ação. Quando o valor é definido para 1 ou 2, as capturas de tela são feitas apenas para ações de erro.  
  
    Para obter mais informações, consulte [Analisando Testes de IU Codificado usando o Logs de Teste de IU Codificado](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md).  
  
## <a name="external-resources"></a>Recursos externos  
  
### <a name="videos"></a>Vídeos  
 [Gravar no IE e reproduzir em qualquer lugar](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!183&authkey=!ANqaLtCZbtJrImU)  
  
 [Criar testes entre navegadores de autor com construtor de teste de IU codificado](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!184&authkey=!AKG8CSow_qmeTq8)  
  
 [Criar testes entre navegadores de autor usando codificação manual básica sem mapa da IU](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!186&authkey=!AJaEvxJnsefyAT4)  
  
 [Executar testes entre navegadores sequencialmente em vários navegadores](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!187&authkey=!ADI8eCQkxHnpOR8)  
  
 [Solucionar problemas de falhas de teste entre navegadores](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!182&authkey=!AEpS48i295B49FI)  
  
### <a name="guidance"></a>Diretrizes  
 [Testes de Entrega Contínua com o Visual Studio 2012 – Capítulo 2: Teste de Unidade: Testando o Interior](http://go.microsoft.com/fwlink/?LinkID=255188)  
  
 [Teste de Entrega Contínua com o Visual Studio 2012 – Capítulo 5: Automatizar Testes do Sistema](http://go.microsoft.com/fwlink/?LinkID=255196)  
  
### <a name="faq"></a>Perguntas Frequentes  
 [Perguntas frequentes sobre testes de IU codificados – 1](http://go.microsoft.com/fwlink/?LinkID=230576)  
  
 [Perguntas frequentes sobre testes de IU codificados – 2](http://go.microsoft.com/fwlink/?LinkID=230578)  
  
### <a name="forum"></a>Fórum  
 [Teste de automação da interface do usuário do Visual Studio (inclui IU codificada)](http://go.microsoft.com/fwlink/?LinkID=224497)  
  
## <a name="see-also"></a>Consulte também  
 [Usar a automação de interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)   
 [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)   
 [Analisando testes de IU codificados usando logs de teste de IU codificado](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)



