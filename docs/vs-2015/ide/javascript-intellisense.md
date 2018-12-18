---
title: JavaScript IntelliSense | Microsoft Docs
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
- IntelliSense [JavaScript]
- <reference> JavaScript XML tag
- JavaScript Code Editor
- XML code comments, JavaScript IntelliSense
- reference JavaScript XML tag
- JavaScript, IntelliSense
- code comments, JavaScript IntelliSense
- JavaScript, reference groups
- JavaScript Editor
- reference directives [JavaScript]
- JavaScript, XML documentation comments
- reference groups [JavaScript]
- JavaScript, reference directives
- IntelliSense [JavaScript], about
- IntelliSense extensibility [JavaScript]
- XML documentation comments [JavaScript]
ms.assetid: af1a3171-c9d8-45a3-9c96-a763e3b163ef
caps.latest.revision: 67
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 215bebb071ce707e2997e934fd58901ec2d56b8b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816333"
---
# <a name="javascript-intellisense"></a>JavaScript IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O IntelliSense ajuda a escrever código mais rapidamente e com menos erros fornecendo informações enquanto você codifica. À medida que você trabalha com o script de cliente no editor do JavaScript, o IntelliSense lista os objetos, as funções, as propriedades e os parâmetros que estão disponíveis com base no contexto atual. É possível selecionar uma opção de codificação na lista pop-up fornecida pelo IntelliSense para concluir o código.  
  
 O IntelliSense torna mais fácil concluir as seguintes tarefas:  
  
- Localizar informações do membro.  
  
- Inserir elementos de linguagem diretamente no seu código.  
  
- Manter o contexto sem precisar sair do editor de código.  
  
- Oferecer suporte ao IntelliSense personalizado com comentários da documentação XML e extensibilidade JavaScript IntelliSense.  
  
  Esse tópico contém as seguintes seções:  
  
- [Determinando o contexto do IntelliSense](#DeterminingIntelliSenseContext)  
  
- [Processando informações do IntelliSense](#ProcessingIntelliSenseInformation)  
  
- [Recursos do IntelliSense do JavaScript](#Features)  
  
- [Extensibilidade do IntelliSense do JavaScript](#Extensibility)  
  
- [Validação de JavaScript](#Validation)  
  
  Para obter mais informações sobre a funcionalidade IntelliSense do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)], consulte [usando o IntelliSense](../ide/using-intellisense.md).  
  
##  <a name="DeterminingIntelliSenseContext"></a> Determinando o contexto do IntelliSense  
 O JavaScript IntelliSense fornece opções de codificação com base em todos os scripts que são relevantes para o contexto de script atual. Isso inclui elementos de script no arquivo atual. Também inclui qualquer código que seja referenciado direta ou indiretamente de seu script, como referências de arquivo de script, referências de script de assembly, referências de serviço e referências associadas por página.  
  
 O contexto de script atual é criado com base nos seguintes itens:  
  
-   Funções que são definidas em todos os blocos de script no documento ativo. Blocos de script embutidos têm suporte em arquivos que tenham as extensões de nome de arquivo: .aspx, . ascx, .master, .html e .htm.  
  
-   Elementos de`script` com atributos `src` que apontam para outro arquivo de script. O arquivo de script de destino deve ter a extensão de nome de arquivo .js.  
  
-   Arquivos JavaScript que fazem referência a outros arquivos JavaScript usando uma diretiva `reference`.  
  
-   Grupos de referência para objetos globais, extensões do IntelliSense ou arquivos de script carregados com atraso.  
  
-   Referências a serviços Web XML.  
  
-   Os controles <xref:System.Web.UI.ScriptManager> e <xref:System.Web.UI.ScriptManagerProxy>, se o aplicativo Web for um aplicativos ASP.NET habilitado para AJAX.  
  
-   O [!INCLUDE[atlaslib_current_ext](../includes/atlaslib-current-ext-md.md)], se você estiver trabalhando em um aplicativo Web ASP.NET habilitado para AJAX.  
  
    > [!NOTE]
    >  O IntelliSense não tem suporte para script que esteja nos atributos de manipulador de eventos em elementos HTML ou que esteja definido nos atributos `href`.  
  
##  <a name="ProcessingIntelliSenseInformation"></a> Processando informações do IntelliSense  
 Para fornecer o IntelliSense do JavaScript, o serviço de linguagem executa as seguintes operações:  
  
-   Cria uma lista de arquivos JavaScript dependentes que se baseiam em referências no documento ativo, bem como no exame recursivo de referências de script nos arquivos referenciados.  
  
-   Percorre a lista e coleta informações de tipo, além de outros dados relevantes de cada arquivo.  
  
-   Agrega os dados e os transmite ao serviço de linguagem JavaScript, que disponibiliza os dados e informações de tipo para o IntelliSense.  
  
-   Monitora os arquivos em busca de alterações que podem afetar a lista do IntelliSense e atualiza a lista conforme a necessidade. Os scripts nos repositórios remotos (como os referenciados usando HTTP) não são monitorados.  
  
##  <a name="Features"></a> Recursos do IntelliSense do JavaScript  
 O JavaScript IntelliSense oferece suporte aos seguintes objetos:  
  
- [Elementos de modelo de objeto (DOM) de documento](#HTMLDom)  
  
- [Objetos intrínsecos](#IntrinsicObjects)  
  
- [As variáveis definidas pelo usuário, funções e objetos](#UserDefined)  
  
- Objetos definidos em arquivos externos usando referências como [referências de script](#Script), [diretivas de referência](#ReferenceDirectives), e [grupos de referência](#ReferenceGroups).  
  
- Objetos definidos nos arquivos remotos que são baixados pelo Visual Studio.  
  
- Objetos especificados em [comentários da documentação XML](#XMLDocComments), como parâmetros e campos.  
  
- Objetos descritos usando marcas de comentário JavaScript padrão (//). Para obter mais informações, consulte [Estendendo JavaScript IntelliSense](../ide/extending-javascript-intellisense.md).  
  
- Objetos com suporte usando o [extensibilidade do JavaScript IntelliSense](#Extensibility) mecanismo. Para obter mais informações, consulte [Estendendo JavaScript IntelliSense](../ide/extending-javascript-intellisense.md).  
  
- [Objetos AJAX ASP.NET](#ASPNet)  
  
  Quando o IntelliSense não pode determinar o tipo de um objeto, ele fornece opções para o preenchimento de declaração usando identificadores no documento ativo. Para obter mais informações, consulte [preenchimento de declaração para identificadores](../ide/statement-completion-for-identifiers.md).  
  
###  <a name="HTMLDom"></a> Elementos de DOM do HTML  
 O JavaScript IntelliSense fornece referências de programação para elementos DHTML (HTML dinâmico) DOM, como `body`, `form` e `div`. Somente os elementos que são incluídos no documento atual e na página mestra são exibidos pelo IntelliSense. O JavaScript IntelliSense também oferece suporte aos objetos `window` e `document` e a seus membros.  
  
###  <a name="IntrinsicObjects"></a> Objetos intrínsecos  
 O JavaScript IntelliSense fornece referências de programação para objetos intrínsecos como `Array`, `String`, `Math`, `Date` e `Number`. Para obter mais informações sobre objetos intrínsecos, consulte [objetos intrínsecos](~/E:/Repos/visualstudio-docs-pr/scripting-docs/javascript/intrinsic-objects-javascript.md).  
  
###  <a name="UserDefined"></a> As variáveis definidas pelo usuário, funções e objetos  
 Quando você altera um arquivo JavaScript, o [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] examina documentos abertos e referenciados para determinar todos os recursos de código disponíveis. Isso inclui as variáveis, funções e objetos que você criou. Esses recursos são então disponibilizados para o JavaScript IntelliSense.  
  
 Para obter mais informações sobre as variáveis definidas pelo usuário, funções e objetos, consulte [criando seus próprios objetos](http://go.microsoft.com/fwlink/?LinkId=108671) no site do MSDN.  
  
###  <a name="External"></a> Referências de arquivo externo  
 Você pode incluir vários tipos de referências de arquivo externo para obter o suporte do IntelliSense em seu código. As referências de arquivo externo podem ser referências de script, diretivas de referência ou podem ser especificadas usando grupos de referência.  
  
####  <a name="Script"></a> Referências de script  
 Em vez de escrever todo o script de cliente em uma página, você pode fazer referência a arquivos externos que incluam código de script. Isso facilita a reutilização de código entre páginas, além de permitir que o script de cliente seja armazenado em cache pelo navegador.  
  
 Se não estiver trabalhando com uma página da Web habilitada para AJAX ASP.NET, você poderá fazer referência a um arquivo de script externo usando o atributo `src` na marca de abertura de um elemento `script`. O atributo `src` especifica a URL para um arquivo externo que contém o código-fonte ou os dados.  
  
 O exemplo a seguir mostra a marcação que usa o `src` de atributo em um <`script`> marca para fazer referência a um arquivo de script.  
  
```html  
<script type="text/javascript" src="~/Scripts/JavaScript.js">  
  
</script>  
```  
  
 Se estiver trabalhando com uma página da Web habilitada para AJAX ASP.NET, você poderá fazer referência a arquivos de script usando o objeto <xref:System.Web.UI.ScriptReference> do controle <xref:System.Web.UI.ScriptManager>.  
  
 O exemplo a seguir mostra a marcação que usa um objeto <xref:System.Web.UI.ScriptReference> em um controle <xref:System.Web.UI.ScriptManager> para referência a um arquivo de script.  
  
```html  
<asp:ScriptManager ID="ScriptManager1" runat="server">  
  <Scripts>  
    <asp:ScriptReference Path="~/Scripts/JavaScript.js" />  
  </Scripts>  
</asp:ScriptManager>  
```  
  
 O IntelliSense também oferece suporte a arquivos de script que são inseridos como recursos em um assembly nos aplicativos Web AJAX ASP.NET. Para obter mais informações sobre recursos de script inseridos, consulte [instruções passo a passo: inserindo um arquivo JavaScript como um recurso em um Assembly](http://msdn.microsoft.com/library/d8cb78cd-95a9-4dc6-92df-391866817e89).  
  
####  <a name="ReferenceDirectives"></a> Diretivas de referência  
 Uma diretiva `reference` permite que o [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] estabeleça uma relação entre o script que você está editando no momento e outros scripts. A diretiva `reference` permite incluir um arquivo de script no contexto de script do arquivo de script atual. Isso permite que o IntelliSense faça referência a funções, tipos e campos definidos externamente enquanto você codifica.  
  
 Você cria uma diretiva `reference` na forma de um comentário XML. A diretiva deve ser declarada no arquivo antes de qualquer outro script. Uma diretiva `reference` pode incluir uma referência de script baseada em disco, uma referência de script baseada em assembly, uma referência de script baseada em serviço ou uma referência de script baseada em página.  
  
 O exemplo a seguir mostra como usar diretivas de referência baseadas em disco. No primeiro exemplo, o serviço de linguagem procura o arquivo na mesma pasta que contém o arquivo de projeto (por exemplo, .jsproj).  
  
 `/// <reference path="ScriptFile1.js" />`  
  
 `/// <reference path="Scripts/ScriptFile2.js" />`  
  
 `/// <reference path="../ScriptFile3.js" />`  
  
 `/// <reference path="~/Scripts/ScriptFile4.js" />`  
  
 O exemplo a seguir mostra como criar uma referência a um script baseado em assembly.  
  
 `/// <reference name "Ajax.js" assembly="System.Web.Extensions, ..." />`  
  
 O exemplo a seguir mostra como fazer referência de script baseado em serviço:  
  
 `/// <reference path="MyService.asmx" />`  
  
 `/// <reference path="Services/MyService.asmx" />`  
  
 `/// <reference path="../MyService.asmx" />`  
  
 `/// <reference path="~/Services/MyService.asmx" />`  
  
> [!NOTE]
>  O JavaScript IntelliSense não tem suporte no script que está contido em arquivos de serviço Web (.asmx) em Projetos de Aplicativo Web (WAP).  
  
 O exemplo a seguir mostra como fazer referência de script baseado em página:  
  
 `/// <reference path="Default.aspx" />`  
  
 `/// <reference path="Admin/Default.aspx" />`  
  
 `/// <reference path="../Default.aspx" />`  
  
 `/// <reference path="~/Admin/Default.aspx" />`  
  
 As regras a seguir se aplicam a uma diretiva `reference`.  
  
-   O comentário XML `reference` deve ser declarado antes de qualquer script.  
  
-   Você deve usar a sintaxe de comentários XML com três barras. As referências feitas usando a sintaxe de comentários padrão (duas barras) são ignoradas.  
  
-   Apenas um arquivo ou recurso pode ser especificado por diretiva.  
  
-   Não são permitidas várias referências aos scripts baseados em página.  
  
-   Se uma referência de página for especificada, nenhum outro tipo de diretiva de referência será permitido.  
  
-   Os nomes de arquivo usam caminhos relativos. Você pode usar o operador til (`~`) para fazer caminhos relativos de raiz por aplicativo.  
  
-   Os caminhos absolutos são ignorados.  
  
-   As diretivas de referência nas páginas referenciadas não serão processadas, isto é, as diretivas de referência não são resolvidas recursivamente para páginas. Somente o script que é referenciado diretamente pela página é incluído.  
  
####  <a name="ReferenceGroups"></a> Grupos de referência  
 Você pode usar grupos de referência predefinidos para especificar se determinados arquivos .js do IntelliSense estão no escopo para diferentes projetos JavaScript. Os seguintes tipos de grupo de referência estão disponíveis:  
  
- Implícitos (Windows), para aplicativos da [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] usando JavaScript. Os arquivos incluídos nesse grupo estão no escopo de cada arquivo .js aberto no Editor de Códigos para o projeto do tipo especificado.  
  
- Implícito (Web), para projetos HTML5. Os arquivos incluídos nesse grupo estão no escopo de cada arquivo .js aberto no Editor de Códigos para esses tipos de projeto.  
  
- Grupos de referência de atividade dedicada, para web workers HTML5. Os arquivos especificados nesse grupo estão no escopo de arquivos .js que têm uma referência explícita a um grupo de referência de atividade dedicada.  
  
- Genérico, para outros tipos de projeto JavaScript.  
  
  Na maioria dos cenários, não é preciso modificar grupos de referência. No entanto, se desejar fazer alterações, você poderá usar opções de configuração do Editor de Códigos do JavaScript para especificar os arquivos incluídos nos grupos de referência. Para obter instruções sobre como usar esse recurso, consulte [opções, Editor de texto, JavaScript, IntelliSense](../ide/reference/options-text-editor-javascript-intellisense.md).  
  
> [!TIP]
>  As referências do IntelliSense são normalmente usadas para oferecer suporte a objetos globais e para o IntelliSense [extensões](#Extensibility). Também é possível usar esse recurso para scripts que devem ser carregados no tempo de execução usando o carregador de scripts.  
  
### <a name="remote-file-references"></a>Referências de arquivo remoto  
 Você pode orientar o Visual Studio a baixar arquivos JavaScript remotos que são referenciados em um arquivo JavaScript para fornecer suporte ao arquivo remoto ou à biblioteca do IntelliSense. Quando você usa esse recurso, os arquivos são baixados quando são incluídos como uma referência no seu arquivo JavaScript.  
  
> [!NOTE]
>  Com exceção dos projetos Web, esse recurso funciona apenas para arquivos JavaScript que são abertos fora do contexto de um projeto. Em projetos Web, os arquivos remotos referenciados no seu projeto são baixados por padrão.  
  
 Para obter instruções sobre como usar esse recurso, consulte [opções, Editor de texto, JavaScript, IntelliSense](../ide/reference/options-text-editor-javascript-intellisense.md).  
  
> [!WARNING]
>  Se você habilitar esse recurso e perceber diminuição de desempenho no Editor de Códigos, é recomendável desabilitá-lo.  
  
###  <a name="XMLDocComments"></a> Comentários da documentação XML  
 Os comentários da documentação XML são descrições de texto de elementos de código que você adiciona ao script. Essas descrições de texto são exibidas no IntelliSense quando você faz referência ao script comentado. Por exemplo, é possível fornecer informações sobre parâmetros e valor de retorno de uma função. Os comentários da documentação XML estão disponíveis somente em assemblies, serviços e arquivos referenciados. Para obter mais informações, consulte [comentários da documentação XML](../ide/xml-documentation-comments-javascript.md) e [criar comentários da documentação XML](../ide/create-xml-documentation-comments-for-javascript-intellisense.md).  
  
 O IntelliSense pode exibir comentários da documentação XML nos seguintes cenários:  
  
- Um arquivo .js que faz referência a outro arquivo .js.  
  
- Um arquivo .js que faz referência a um arquivo .aspx.  
  
- Um arquivo .aspx que faz referência a um arquivo .js.  
  
  O IntelliSense não está disponível quando um arquivo .aspx faz referência a outro arquivo .aspx.  
  
###  <a name="ASPNet"></a> Objetos AJAX ASP.NET  
 O AJAX ASP.NET também oferece suporte ao JavaScript IntelliSense. O AJAX ASP.NET inclui uma estrutura de cliente que estende os tipos padrão que estão disponíveis no ECMAScript (JavaScript). Para permitir que o JavaScript IntelliSense forneça detalhes sobre objetos AJAX ASP.NET, os comentários da documentação XML foram adicionados em todo o [!INCLUDE[atlaslib_current_ext](../includes/atlaslib-current-ext-md.md)]. Esses comentários da documentação XML são exibidos quando você usa tipos e membros que estão contidos na biblioteca AJAX ASP.NET.  
  
> [!NOTE]
>  Os membros privados não são exibidos pelo JavaScript IntelliSense. Os membros privados são denotados no AJAX ASP.NET como membros que começam com um sublinhado (_).  
  
##  <a name="Extensibility"></a> Extensibilidade do IntelliSense do JavaScript  
 O serviço de linguagem JavaScript fornece objetos e funções que permitem modificar a experiência do IntelliSense para desenvolvedores que usam bibliotecas de terceiros. Esses recursos são especialmente úteis quando o serviço de linguagem padrão não pode fornecer todas as informações que você deseja fornecer aos clientes. Para obter mais informações, consulte [Estendendo JavaScript IntelliSense](../ide/extending-javascript-intellisense.md).  
  
##  <a name="Validation"></a> Validação de JavaScript  
 A validação de script JavaScript ocorre constantemente em segundo plano. Quando o [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] detecta erros de sintaxe no código JavaScript, os comentários são fornecidos das seguintes maneiras:  
  
-   Elementos sublinhados no editor. Sublinhados ondulados vermelhos indicam erros. Se você pousar o ponteiro do mouse sobre o erro, a dica de ferramenta exibirá a descrição do erro.  
  
-   **Lista de erros** janela. O **Error List** janela exibe a descrição do erro, o arquivo onde o erro ocorreu, o número de linha e coluna e o projeto. Para exibir o **lista de erros** janela, no **exibição** menu, clique em **lista de erros**.  
  
-   A janela Saída mostra referências que não foram carregadas.  
  
## <a name="see-also"></a>Consulte também  
 [Usando o IntelliSense](../ide/using-intellisense.md)   
 [Criar comentários de documentação XML](../ide/create-xml-documentation-comments-for-javascript-intellisense.md)   
 [Estendendo o JavaScript IntelliSense](../ide/extending-javascript-intellisense.md)   
 [Preenchimento de declaração para identificadores](../ide/statement-completion-for-identifiers.md)   
 [Comentários da documentação XML](../ide/xml-documentation-comments-javascript.md)   
 [Sobre o modelo de objeto DHTML](http://go.microsoft.com/fwlink/?LinkID=92344)   
 [Listar membros](http://msdn.microsoft.com/en-us/1b9cc469-9cd4-4d42-9999-1f9479635ff8)   
 [Atributo SRC &#124; propriedade src](http://go.microsoft.com/fwlink/?LinkId=92345)



