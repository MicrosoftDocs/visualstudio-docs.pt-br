---
title: Criando aplicativos em linguagens bidirecionais | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Hebrew character display, creating applications
- bi-directional language support, about bi-directional language support
- Arabic language, creating applications
ms.assetid: b56f9795-ed8d-4452-9d49-8ca0b0145d86
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 32acd2a58c2482de6fdd7ed10c99a023d41a8cb4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49248489"
---
# <a name="creating-applications-in-bi-directional-languages"></a>Criando aplicativos em idiomas bidirecionais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível usar o Visual Studio para criar aplicativos que exibem o texto corretamente em idiomas escritos da direita para a esquerda, incluindo árabe e hebraico. Para alguns recursos, é possível apenas definir as propriedades. Em outros casos, é necessário implementar recursos no código.  
  
> [!NOTE]
>  Para inserir e exibir idiomas bidirecionais, é necessário estar trabalhando com uma versão do Windows que está configurada com o idioma apropriado. Essa pode ser uma versão em inglês do Windows com o pacote de idioma apropriado instalado, ou a versão localizada do Windows.  
  
## <a name="types-of-application-that-support-bi-directional-languages"></a>Tipos de aplicativo que dão suporte a idiomas bidirecionais  
  
1.  Aplicativos do Windows. É possível criar aplicativos totalmente bidirecionais que incluem suporte para texto bidirecional, sentido de leitura da direita para a esquerda e espelhamento (reversão do layout de janelas, menus, caixas de diálogo e assim por diante). Com exceção do espelhamento, esses recursos estão disponíveis por padrão ou como configurações de propriedades. Há suporte inerente para o espelhamento em alguns recursos, como caixas de mensagem. No entanto, em outros casos, é necessário implementar o espelhamento no código. Para obter mais informações, consulte [Suporte bidirecional para aplicativos do Windows Forms](http://msdn.microsoft.com/library/7b622fa4-f390-4e4d-b624-83a1917cccf2).  
  
2.  Aplicativos Web. Os serviços Web dão suporte ao recebimento e envio de textos UTF-8 e Unicode, tornando-os adequados para aplicativos que envolvem idiomas bidirecionais. Os aplicativos cliente Web dependem de navegadores para sua interface do usuário e, portanto, o grau de suporte bidirecional em um aplicativo Web depende do nível de suporte do navegador do usuário a esses recursos bidirecionais. No Visual Studio, é possível criar aplicativos com suporte para texto em árabe ou hebraico, sentido de leitura da direita para a esquerda, codificação de arquivos e configurações da cultura local. Para obter mais informações, consulte [Suporte bidirecional para aplicativos Web ASP.NET](http://msdn.microsoft.com/library/5576f9b1-9b86-41ef-8354-092d366bcd03).  
  
3.  Aplicativos de console. Aplicativos de console não incluem o suporte de texto para idiomas bidirecionais. Esta é uma consequência de como o Windows funciona com aplicativos de console.  
  
## <a name="visual-studio-features-that-are-fully-supported"></a>Recursos do Visual Studio com suporte completo  
 Em tempo de design no Visual Studio, é possível usar idiomas bidirecionais das seguintes maneiras:  
  
-   **Entrada de texto** O Visual Studio dá suporte ao Unicode; portanto, se o sistema estiver definido com a localidade e o idioma de entrada apropriados, será possível inserir texto em árabe ou hebraico. (O suporte para árabe inclui Kashida e Sinais Diacríticos.)  
  
-   **Nomes de objeto** É possível usar idiomas bidirecionais para atribuir nomes a soluções, projetos, arquivos, pastas e assim por diante. No código, é possível usar idiomas bidirecionais para os nomes de variáveis, classes, objetos, atributos, metadados e outros elementos.  
  
-   **Codificação do arquivo** é possível salvar e abrir arquivos com uma codificação Unicode ou específica a um idioma. Para obter mais informações, consulte [Como salvar e abrir arquivos com codificação](../ide/how-to-save-and-open-files-with-encoding.md).  
  
## <a name="features-with-limited-or-no-support"></a>Recursos com suporte limitado ou sem suporte  
 Outros recursos comuns a aplicativos de idiomas bidirecionais não tem suporte completo no Visual Studio, ou em alguns casos, não tem nenhum suporte. Elas incluem:  
  
-   **Ordem de leitura da direita para a esquerda** Por padrão, os controles de entrada de texto usados no Visual Studio usam o sentido de leitura da esquerda para a direita. Na maioria dos casos, é possível usar gestos do Windows padrão para mudar o sentido de leitura. Por exemplo, é possível pressionar Ctrl+Shift Direita para mudar para a janela Propriedades para dar suporte ao sentido de leitura da direita para a esquerda em valores da propriedade.  
  
     No entanto, não há suporte ao sentido de leitura da direita para a esquerda em nenhum lugar do Visual Studio. As exceções incluem:  
  
    -   Caixas de seleção, listas suspensas e outros controles em caixas de diálogo do Visual Studio sempre usam o sentido de leitura da esquerda para a direita.  
  
    -   O editor de código (e o editor de texto) não dão suporte ao sentido de leitura da direita para a esquerda. É possível inserir texto em um idioma bidirecional, mas o sentido de leitura sempre será da esquerda para a direita.  
  
## <a name="naming-things-using-arabic-or-hebrew-text"></a>Nomeando itens usando um texto em árabe ou hebraico  
 É possível usar um texto em árabe ou hebraico para atribuir nomes a pastas, variáveis ou outros objetos. Ao trabalhar com o árabe, é possível usar qualquer caractere árabe, incluindo Kashida e Sinais Diacríticos.  
  
 Os seguintes elementos podem ser nomeados usando o árabe ou o hebraico e serão manipulados corretamente no Visual Studio:  
  
-   Nomes de solução, projeto e arquivo, incluindo as pastas incluídas no caminho do projeto. O Gerenciador de Soluções exibirá os nomes de elemento e de solução corretamente.  
  
-   Conteúdo do arquivo. É possível abrir ou salvar arquivos com a codificação Unicode ou com uma página de código selecionada.  
  
    > [!NOTE]
    >  O editor de código é um caso especial. Para obter detalhes, consulte abaixo.  
  
-   Elementos de dados. O **Gerenciador de Servidores** exibirá esses elementos corretamente e permitirá sua edição.  
  
-   Elementos copiados para a Área de Transferência do Windows.  
  
-   Atributos e metadados.  
  
-   Valores da propriedade. É possível usar um texto em árabe ou hebraico na janela Propriedades. A janela permite mudar entre o sentido de leitura da direita para a esquerda e da esquerda para a direita usando pressionamentos de tecla padrão do Windows (CTRL+Shift Direita para direita para a esquerda e CTRL+Shift Esquerda para esquerda para a direita).  
  
-   Código e texto literal. No editor de código (que também é o editor de texto), é possível usar o árabe ou o hebraico para nomear classes, funções, variáveis, propriedades, literais de cadeia de caracteres, atributos e assim por diante. No entanto, o editor não dá suporte ao sentido de leitura da direita para a esquerda; o texto sempre começa na margem esquerda.  
  
    > [!TIP]
    >  É recomendável colocar literais de cadeia de caracteres em arquivos de recurso, em vez de codificá-los nos programas. Para obter mais informações, consulte [Passo a passo: Localizando o Windows Forms](http://msdn.microsoft.com/en-us/9a96220d-a19b-4de0-9f48-01e5d82679e5).  
  
    > [!NOTE]
    >  Você deve ser consistente na forma como se refere aos objetos nomeados nesses idiomas. Por exemplo, se você usar Kashida ao nomear uma variável em árabe, deverá sempre usar Kashida ao se referir a essa variável; caso contrário, ocorrerão erros.  
  
-   Comentários sobre o código. É possível criar comentários em árabe ou hebraico. Você também pode usar esses idiomas na ferramenta de construtor de comentários.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte bidirecional para aplicativos do Windows Forms](http://msdn.microsoft.com/library/7b622fa4-f390-4e4d-b624-83a1917cccf2)   
 [Suporte bidirecional para aplicativos Web ASP.NET](http://msdn.microsoft.com/library/5576f9b1-9b86-41ef-8354-092d366bcd03)   
 [Globalizando aplicativos](../ide/globalizing-applications.md)   
 [Localizando aplicativos](../ide/localizing-applications.md)

