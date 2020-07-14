---
title: SDK do Microsoft Help Viewer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
caps.latest.revision: 34
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3f7cbe9606b73741e1e59eb14f40cb277052944a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545074"
---
# <a name="microsoft-help-viewer-sdk"></a>SDK do Microsoft Help Viewer
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Este artigo contém as seguintes tarefas para integradores do Visualizador da ajuda do Visual Studio:

- Criando um tópico (suporte F1)

- Criando um pacote de identidade visual de conteúdo do Visualizador da ajuda

- Implantando um conjunto de artigos

- Adicionando ajuda ao shell do Visual Studio (integrado ou isolado)

- Recursos adicionais

### <a name="creating-a-topic-f1-support"></a>Criando um tópico (suporte F1)
 Esta seção fornece uma visão geral dos componentes de um tópico apresentado, requisitos de tópico, uma breve descrição de como criar um tópico (incluindo os requisitos de suporte F1) e, por fim, um tópico de exemplo com seu resultado renderizado.

 **Visão geral do tópico do Help Viewer**

 Quando um tópico é chamado para renderização, o Visualizador da ajuda obtém os elementos do pacote de identidade visual associados ao tópico no momento da instalação ou da última atualização, juntamente com o tópico XHTML, e combina os dois para resultar no modo de exibição de conteúdo apresentado (dados de identidade visual + dados de tópico).  O pacote de identidade visual contém logotipos, suporte para comportamentos de conteúdo e texto de identidade visual (direitos autorais etc.).  Consulte "criando pacote de identidade visual" abaixo para obter mais informações sobre os elementos do pacote de identidade visual.  Caso não haja nenhum pacote de identidade visual associado ao tópico, o Visualizador da ajuda usará o pacote de identidade visual de fallback localizado na raiz do aplicativo Help Viewer (Branding_en-US. mshc).

 **Requisitos do tópico do Help Viewer**

 Para ser renderizado corretamente no Visualizador da ajuda, o conteúdo bruto do tópico deve ser o XHTML básico do W3C 1,1.

 Um tópico normalmente contém duas seções:

- Metadados (consulte referência de metadados de conteúdo): dados sobre o tópico, por exemplo, a ID exclusiva do tópico, o valor da palavra-chave, a ID de Sumário do tópico, a ID do nó pai, etc.

- Conteúdo do corpo: compatível com o XHTML básico 1,1 do W3C, que inclui comportamentos de conteúdo com suporte (área recolhível, trecho de código, etc.) Uma lista completa é mostrada abaixo).

  Controles com suporte do pacote de marca do Visual Studio:

- Links

- CodeSnippet

- CollapsibleArea

- Membro herdado

- LanguageSpecificText

  Cadeias de idiomas com suporte (não diferencia maiúsculas de minúsculas):

- javascript

- Csharp ou c #

- CPlusPlus ou Visual c++ + + ou c++

- jscript

- VisualBasic ou VB

- f # ou FSharp ou FS

- outro – uma cadeia de caracteres que representa um nome de idioma

  **Criando um tópico do Help Viewer**

  Crie um novo documento XHTML chamado ContosoTopic4.htm e inclua a marca de título (abaixo).

```html
<html>
<head>
<title>Contoso Topic 4</title>
</head>

<body>

</body>
</html>

```

 Em seguida, adicione dados para definir como o tópico deve ser apresentado (automarcado ou não), como fazer referência a este tópico para F1, em que este tópico existe dentro do Sumário, sua ID (para referência de link por outros tópicos), etc.  Consulte a tabela "metadados de conteúdo" abaixo para obter uma lista completa dos metadados com suporte.

- Nesse caso, usaremos nosso próprio pacote de marca, uma variante do pacote de identidade visual do Help Viewer.

- Adicione o meta e o valor F1 ("Microsoft. help. F1" content = "ContosoTopic4") que corresponderão ao valor F1 fornecido no recipiente de propriedades do IDE.  (Consulte a seção suporte F1 para obter mais informações.)   Esse é o valor que é correspondido à chamada F1 de dentro do IDE para exibir este tópico quando F1 é escolhido no IDE.

- Adicione a ID do tópico. Esta é a cadeia de caracteres usada por outros tópicos para vincular a este tópico.  É a ID do Visualizador da ajuda deste tópico.

- Para o Sumário, adicione o nó pai deste tópico para definir onde este nó de Sumário do tópico será exibido.

- Para o Sumário, adicione a ordem de nó deste tópico. Quando o nó pai tem n número de nós filhos, defina na ordem dos nós filho o local deste tópico. Por exemplo, este tópico é o número 4 de 4 tópicos filho.)

  Exemplo de seção de metadados:

```html
<html>
<head>
<title>Contoso Topic 4</title>

<meta name="SelfBranded" content="false" />
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="Microsoft.Help.Id" content="ContosoTopic4" />
<meta name="Microsoft.Help.F1" content=" ContosoTopic4" />
    <meta name="Language" content="en-us" />
<meta name="Microsoft.Help.TocParent" content="ContosoTopic0" />
<meta name="Microsoft.Help.TocOrder" content="4" />

</head>

<body>

</body>
</html>

```

 **O corpo do tópico**

 O corpo (sem incluir o cabeçalho e o rodapé) do tópico conterá links de página, uma seção de observação, uma área recolhível, um trecho de código e uma seção de texto específico de idioma.  Consulte a seção identidade visual para obter informações sobre essas áreas do tópico apresentado.

1. Adicione uma marca de título de tópico:`<div class="title">Contoso Topic 4</div>`

2. Adicionar uma seção de observação:`<div class="alert"> add your table tag and text </div>`

3. Adicione uma área recolhível:`<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4. Adicione um trecho de código:`<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5. Adicionar texto específico à linguagem de código: `<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />` Observe que devLangnu = permite que você insira outros idiomas. Por exemplo, devLangnu = "Fortran" exibirá o Fortran quando o trecho de código DisplayLanguage = Fortran

6. Adicionar links de página:`<a href="ms-xhelp://?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
> Observação: para uma nova colorização de código "idioma de vídeo" (exemplo, F #, COBOL, Fortran) sem suporte no trecho de código será monocromático.

 **Tópico do Help Viewer de exemplo** O código ilustra como definir metadados, um trecho de código, uma área recolhível e um texto específico de idioma.

```
<?xml version="1.0" encoding="utf-8"?>
<html>
<head>
<title>Contoso Topic 4</title>

    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="Microsoft.Help.Id" content="ContosoTopic4" />
<meta name="Microsoft.Help.F1" content=" ContosoTopic4" />
    <meta name="Language" content="en-us" />
<meta name="Microsoft.Help.TocParent" content="ContosoTopic0" />
<meta name="Microsoft.Help.TocOrder" content="4" />
<meta name="SelfBranded" content="false" />
</head>

<body>
<div class="title">Contoso Topic 4</div>

  <div id="header">
<table id="bottomTable" cellpadding="0" cellspacing="0"  width="100%">
        <tr id="headerTableRow2"><td align="left">
            <span id="nsrTitle">Contoso Topic 1</span>
          </td>
<td align="right">
</td></tr>
<tr id="headerTableRow1"><td align="left">
            <span id="runningHeaderText">Contoso Widgets & Sprockets</span>
          </td></tr>
      </table>
</div>

<h2>Table of Contents</h2>

<ul class="toc">
<li class="tocline1"><a href="#introduction" target="_self">1.0 Introduction</a></li>
<li class="tocline1"><a href="#seealso" target="_self">2.1 See Also</a></li>
</ul>

<div class="topic">

<div id="mainSection">
<div id="mainBody">

<a name="introduction"></a>
<h2>1.0 Introduction</h2>
<p>[This documentation is for sample purposes only.]</p>

<p>Contoso Topic 1 contains examples of:
<ul>
<li>Collapsible Area</li>
<li>Bookmark ("See also")</li>
<li>Code Snippets from Branding Package</li>
</ul>
 </p>
<div class="alert"><table><tr><th>
<strong>Note </strong></th></tr>
<tr><td>
<p>This is an example of a <span class="label">Note </span>section.
Call out important items for your reader in this <span class="label">Note </span>box.
</p></td></tr>
</table>
</div>
</div>

<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading">

            <a id="sectionToggle0"><!----></a>

<div>
Example of Collapsible Area
<br/>
Lorem ipsum dolor sit amet...
</div>
</CollapsibleArea>

<div id="snippetGroup" >
<CodeSnippet EnableCopyCode="true" Language="VisualBasic" ContainsMarkup="false" DisplayLanguage="Visual Basic" >
Private Sub ToolStripRenderer1_RenderGrip(sender as Object, e as ToolStripGripRenderEventArgs) _ Handles ToolStripRenderer1.RenderGrip
Dim messageBoxVB as New System.Text.StringBuilder()
    messageBoxVB.AppendFormat("{0} = {1}", "GripBounds", e.GripBounds)
    messageBoxVB.AppendLine()
 ...
    MessageBox.Show(messageBoxVB.ToString(),"RenderGrip Event")
End Sub
</CodeSnippet>

<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" >
private void ToolStripRenderer1_RenderGrip(Object sender, ToolStripGripRenderEventArgs e)
{
System.Text.StringBuilder messageBoxCS = new System.Text.StringBuilder();
messageBoxCS.AppendFormat("{0} = {1}", "GripBounds", e.GripBounds );
messageBoxCS.AppendLine();
...
MessageBox.Show(messageBoxCS.ToString(), "RenderGrip Event" );
}
</CodeSnippet>

<CodeSnippet EnableCopyCode="true" Language="fsharp" ContainsMarkup="false" DisplayLanguage="F#" >
some F# code
</CodeSnippet>
</div>

<h4 class="subHeading">Example of code specific text</h4>Language = <LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />

<a name="seealso"></a>
<h1 class="heading">See Also</h1>

    <div id="seeAlsoSection" class="section">
    <div class="seeAlsoStyle">
        <a href="ms-xhelp://?Id=ContosoTopic1">Main Topic</a>
    </div>
 </div>
</div>
</div>
</body>
</html>

```

 **Suporte a F1**

 No Visual Studio, a seleção de F1 gera valores fornecidos a partir do posicionamento do cursor dentro do IDE e popula um "recipiente de propriedades" com os valores fornecidos (com base no local do cursor. Quando o cursor está sobre o recurso x, o recurso x está ativo/em foco e popula o recipiente de propriedades com valores.  Quando F1 é selecionado, o recipiente de propriedades é preenchido e o código F1 do Visual Studio procura ver se a fonte de ajuda padrão dos clientes é local ou online (online é o padrão), em seguida, cria a cadeia de caracteres apropriada com base na configuração de usuários (online é o padrão) – execução do Shell (consulte o guia do administrador da ajuda para parâmetros de inicialização exe) com parâmetros para o Help Viewer local + palavra-chave do recipiente de propriedades se a ajuda local for o padrão , ou a URL do MSDN com a palavra-chave na lista de parâmetros.

 Se três cadeias de caracteres forem retornadas para F1, mencionadas como uma cadeia de valores múltiplos, pegar o primeiro termo, procurar um problema e, se for encontrado, terminaremos; caso contrário, mova para a próxima cadeia de caracteres.  O pedido é importante. A apresentação das palavras-chave de vários valores deve ser a cadeia de caracteres mais longa para a cadeia de caracteres mais curta.  Para verificar isso no caso de palavras-chave de vários valores, examine a cadeia de caracteres de URL F1 online, que incluirá a palavra-chave escolhida.

 No Visual Studio 2012, fizemos intencionalmente uma divisão mais forte entre online e offline, de modo que, se a configuração do usuário estivesse para online, simplesmente passamos a solicitação F1 diretamente para nosso serviço de consulta online no MSDN em vez de rotear por meio do agente da biblioteca de ajuda que tínhamos no Visual Studio 2010. Em seguida, usamos um estado de "conteúdo do fornecedor instalado = verdadeiro" para determinar se é preciso fazer algo diferente nesse contexto. Se for true, executamos essa lógica de análise e de roteamento dependendo do que você deseja dar suporte aos seus clientes. Se for false, basta ir para o MSDN. Se a configuração do usuário for local, todas as chamadas vão para o mecanismo de ajuda local.

 Diagrama de fluxo de F1:

 ![Fluxo de F1](../../extensibility/internals/media/f1flow.png "F1flow")

 Quando a fonte de conteúdo da ajuda padrão do Visualizador da ajuda está definida como online (iniciar no navegador):

- Os recursos do Visual Studio Partner (VSP) emitem um valor para o recipiente de propriedades F1 (prefixo do recipiente de propriedades. a palavra-chave e a URL online para o prefixo encontrado no registro): F1 envia uma URL do VSP + parâmetros para o navegador.

- Recursos do Visual Studio (editor de linguagem, itens de menu específicos do Visual Studio, etc.): F1 envia uma URL do Visual Studio para o navegador.

  Quando a fonte de conteúdo da ajuda padrão do Visualizador da ajuda é definida como ajuda local (iniciar no Visualizador da ajuda):

- Os recursos do VSP em que a palavra-chave corresponde entre o recipiente de propriedades F1 e o índice de repositório local (ou seja, o prefixo do recipiente de propriedades. keyword = o valor encontrado no índice de repositório local): F1 renderiza o tópico no Help Viewer.

- Recursos do Visual Studio (nenhuma opção para o VSP substituir o recipiente de propriedades emitido por recursos do Visual Studio): F1 renderiza um tópico do Visual Studio no Visualizador da ajuda.

  Defina os valores de registro a seguir para habilitar o fallback F1 para o conteúdo de ajuda do fornecedor. O fallback de F1 significa que o Visualizador da ajuda está definido para procurar F1 conteúdo de ajuda online e o conteúdo do fornecedor é instalado localmente no disco rígido dos usuários. O Visualizador da ajuda deve examinar a ajuda local do conteúdo, mesmo que a configuração padrão seja para a ajuda online.

1. Defina o valor **VendorContent** na chave do registro Help 2,1:

   - Para sistemas operacionais de 32 bits:

        HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Help\v2.1\Catalogs\VisualStudio12

        "VendorContent" = DWORD: 00000001

   - Para sistemas operacionais de 64 bits:

        HKEY_LOCAL_MACHINE \SOFTWARE\Wow6432Node\Microsoft\Help\v2.1\Catalogs\VisualStudio12

        "VendorContent" = DWORD: 00000001

2. Registre o namespace do parceiro na chave do registro Help 2,1:

   - Para sistemas operacionais de 32 bits:

      <em> \\ Namespace \> </em> do HKEY_LOCAL_MACHINE \software\microsoft\help\v2.1\partner<

      "local" = "offline"

   - Para sistemas operacionais de 64 bits:

      <em> \\ Namespace \> </em> do HKEY_LOCAL_MACHINE \software\wow6432node\microsoft\help\v2.1\partner<

      "local" = "offline"

   **Análise de namespace nativo base**

   Para ativar a análise de namespace nativo base, no registro, adicione um novo DWORD com o nome de: BaseNativeNamespaces e defina seu valor como 1 (na chave de catálogo para a qual deseja oferecer suporte).  Por exemplo, se você quiser usar o catálogo do Visual Studio, poderá adicionar a chave ao caminho:

   HKEY_LOCAL_MACHINE \SOFTWARE\Wow6432Node\Microsoft\Help\v2.1\Catalogs\VisualStudio12

   Quando for encontrada uma palavra-chave F1 no formato de cabeçalho/método, o caractere '/' será analisado, resultando na seguinte construção:

- HEADER: será o namespace que pode ser usado para se registrar no registro

- MÉTODO: isso se tornará a palavra-chave que é passada.

  Por exemplo, dada uma biblioteca personalizada chamada CustomLibrary e um método chamado MyTestMethod, quando uma solicitação F1 chega, ela será formatada como `CustomLibrary/MyTestMethod` .

  Um usuário pode então registrar CustomLibrary como o namespace no hive Partners e fornecer qualquer chave de local que desejarem, e a palavra-chave passada para a consulta será MyTestMethod.

  **Habilitar a ferramenta de depuração de ajuda no IDE**

  Adicione a seguinte chave do registro e valor:

  HKEY_CURRENT_USER chave de ajuda do \Software\Microsoft\VisualStudio\12.0\Dynamic: exibir a saída de depuração no valor de varejo: Sim

  No IDE, no item de menu ajuda, selecione "contexto de ajuda de depuração"

  **Metadados de conteúdo**

  Na tabela a seguir, qualquer cadeia de caracteres que apareça entre colchetes é um espaço reservado que deve ser substituído por um valor reconhecido. Por exemplo, em \<meta name="Microsoft.Help.Locale" content="[language code]" /> , "[código de idioma]" deve ser substituído por um valor como "en-US".

|Propriedade (representação HTML)|Descrição|
|--------------------------------------|-----------------|
|\< meta name="Microsoft.Help.Locale" content="[language-code]" />|Define uma localidade para este tópico. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez e deverá ser inserida acima de qualquer outra marca de ajuda da Microsoft. Se essa marca não for usada, o texto do corpo do tópico será indexado usando o separador de palavras associado à localidade do produto, se for especificado; caso contrário, o separador de palavras en-US será usado. Essa marca está de acordo com o ISOC RFC 4646. Para garantir que a ajuda da Microsoft funcione corretamente, use essa propriedade em vez do atributo idioma geral.|
|\< meta name="Microsoft.Help.TopicLocale" content="[language-code]" />|Define uma localidade para este tópico quando outras localidades também são usadas. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez. Use essa marca quando o catálogo contiver conteúdo em mais de um idioma. Vários tópicos em um catálogo podem ter a mesma ID, mas cada um deles deve especificar um TopicLocale exclusivo. O tópico que especifica um TopicLocale que corresponde à localidade do catálogo é o tópico que é exibido no sumário. No entanto, todas as versões de idioma do tópico são exibidas nos resultados da pesquisa.|
|\< title>Título\</title>|Especifica o título deste tópico. Essa marca é necessária e deve ser usada apenas uma vez em um tópico. Se o corpo do tópico não contiver uma seção de título \<div> , esse título será exibido no tópico e no sumário.|
|\< meta name=" Microsoft.Help.Keywords" content="[aKeywordPhrase]"/>|Especifica o texto de um link que é exibido no painel índice do Help Viewer. Quando o link é clicado, o tópico é exibido. Você pode especificar várias palavras-chave de índice para um tópico ou pode omitir essa marca se não quiser que os links para este tópico apareçam no índice. Palavras-chave "K" de versões anteriores da ajuda podem ser convertidas para essa propriedade.|
|\< meta name="Microsoft.Help.Id" content="[TopicID]"/>|Define o identificador deste tópico. Essa marca é necessária e deve ser usada apenas uma vez em um tópico. A ID deve ser exclusiva entre os tópicos no catálogo que têm a mesma configuração de localidade. Em outro tópico, você pode criar um link para este tópico usando essa ID.|
|\< meta name="Microsoft.Help.F1" content="[System.Windows.Controls.Primitives.IRecyclingItemContainerGenerator]"/>|Especifica a palavra-chave F1 para este tópico. Você pode especificar várias palavras-chave F1 para um tópico ou pode omitir essa marca se não quiser que este tópico seja exibido quando um usuário do aplicativo pressionar F1. Normalmente, apenas uma palavra-chave F1 é especificada para um tópico. Palavras-chave "F" de versões anteriores da ajuda podem ser convertidas para essa propriedade.|
|\< meta name="Description" content="[topic description]" />|Fornece um breve resumo do conteúdo deste tópico. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez. Essa propriedade é acessada diretamente pela biblioteca de consulta; Ele não é armazenado no arquivo de índice.|
 meta name = "Microsoft. help. TocParent" content = "[parent_Id]"/>|Especifica o tópico pai deste tópico no sumário. Essa marca é necessária e deve ser usada apenas uma vez em um tópico. O valor é o Microsoft.Help.Id do pai. Um tópico pode ter apenas um local no sumário. "-1" é considerado a ID do tópico para a raiz do Sumário. No [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)] , essa página é o Help Viewer Home Page. Esse é o mesmo motivo pelo qual adicionamos especificamente TocParent =-1 a alguns tópicos para garantir que eles apareçam no nível superior. O Visualizador da ajuda home page é uma página do sistema e, portanto, não substituível. Se um VSP tentar adicionar uma página com uma ID de-1, ela poderá ser adicionada ao conjunto de conteúdo, mas o Help Viewer sempre usará a página do sistema – início do Help Viewer|
|\< meta name="Microsoft.Help.TocOrder" content="[positive integer]"/>|Especifica o local no sumário que este tópico aparece em relação aos seus tópicos de pares. Essa marca é necessária e deve ser usada apenas uma vez em um tópico. O valor é um inteiro. Um tópico que especifica um inteiro de valor inferior aparece acima de um tópico que especifica um inteiro de valor mais alto.|
|\< meta name="Microsoft.Help.Product" content="[product code]"/>|Especifica o produto que este tópico descreve. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez. Essas informações também podem ser fornecidas como um parâmetro que é passado para o indexador da ajuda.|
|\< meta name="Microsoft.Help.ProductVersion" content="[version number]"/>|Especifica a versão do produto que este tópico descreve. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez. Essas informações também podem ser fornecidas como um parâmetro que é passado para o indexador da ajuda.|
|\< meta name="Microsoft.Help.Category" content="[string]"/>|Usado por produtos para identificar subseções de conteúdo. Você pode identificar várias subseções para um tópico ou pode omitir essa marca se não quiser que os links identifiquem nenhuma subseção. Essa marca é usada para armazenar os atributos para TargetOS e TargetFrameworkMoniker quando um tópico é convertido de uma versão anterior da ajuda. O formato do conteúdo é AttributeName: AttributeValue.|
|\< meta name="Microsoft.Help.TopicVersion content="[topic version number]"/>|Especifica esta versão do tópico quando há várias versões em um catálogo. Como não há garantia de que Microsoft.Help.Id seja exclusivo, essa marca é necessária quando há mais de uma versão de um tópico em um catálogo, por exemplo, quando um catálogo contém um tópico para o .NET Framework 3,5 e um tópico para o .NET Framework 4 e ambos têm o mesmo Microsoft.Help.Id.|
|\< meta name="SelfBranded" content="[TRUE or FALSE]"/>|Especifica se este tópico usa o pacote de identidade visual de inicialização do Gerenciador de biblioteca de ajuda ou um pacote de identidade visual que é específico para o tópico. Essa marca deve ser TRUE ou FALSE. Se for TRUE, o pacote de identidade visual do tópico associado substituirá o pacote de identidade visual definido quando o Gerenciador de biblioteca de ajuda for iniciado para que o tópico seja renderizado como pretendido mesmo que seja diferente do processamento de outro conteúdo. Se for FALSE, o tópico atual será renderizado de acordo com o pacote de identidade visual que é definido quando o Gerenciador de biblioteca de ajuda é iniciado. Por padrão, o Gerenciador de biblioteca de ajuda assume que a própria identidade visual seja falsa, a menos que a variável SelfBranded seja declarada como verdadeira; Portanto, você não precisa declarar \<meta name="SelfBranded" content="FALSE"/> .|

### <a name="creating-a-branding-package"></a>Criando um pacote de identidade visual
 A versão do Visual Studio abrange vários produtos diferentes do Visual Studio, incluindo os shells isolados e integrados para parceiros do Visual Studio.  Cada um desses produtos requer algum grau de suporte de identidade visual de conteúdo de ajuda baseado em tópico, exclusivo para o produto.  Por exemplo, os tópicos do Visual Studio precisam ter uma apresentação de marca consistente, enquanto o SQL Studio, que encapsula o Shell ISO, requer sua própria identidade visual exclusiva de conteúdo da ajuda para cada tópico.  Um parceiro de shell integrado pode querer que seus tópicos de ajuda estejam dentro do conteúdo da ajuda do produto do Visual Studio pai, mantendo sua própria identidade visual de tópico.

 Os pacotes de identidade visual são instalados pelo produto que contém o Visualizador da ajuda.  Para produtos do Visual Studio:

- Um pacote de identidade visual de fallback (Branding_ \<locale> . mshc) é instalado na raiz do aplicativo Help viewer 2,1 (exemplo: c:\Arquivos de programas (x86) \Microsoft Help Viewer\v2.1) pelo pacote de idiomas do Help Viewer.  Isso é usado para casos em que o pacote de identidade visual do produto não está instalado (nenhum conteúdo foi instalado) ou onde o pacote de identidade visual instalado está corrompido.  Os elementos do Visual Studio (logotipo e comentários) são ignorados quando o pacote de identidade visual de fallback de raiz do aplicativo é usado.

- Quando o conteúdo do Visual Studio é instalado a partir do serviço de pacote de conteúdo, um pacote de marca também é instalado (para o cenário de instalação de conteúdo pela primeira vez).  Se houver uma atualização para o pacote de identidade visual, a atualização será instalada quando a próxima atualização de conteúdo ou ação de instalação de pacote adicional ocorrer.

  O Microsoft Help Viewer dá suporte à identidade visual de tópicos com base nos metadados do tópico.

- Onde os metadados do tópico definem Self-Brand = true, renderizar o tópico como está, não faça nada (no que diz respeito à identidade visual).

- Quando os metadados do tópico definem a automarca = false, use o pacote de identidade visual associado ao valor de metadados TopicVendor.

- Em que os metadados de tópico definem Name = "Microsoft. help. TopicVendor" Content = \< branding package name in vendor MSHA> , use o pacote de identidade visual definido no valor de conteúdo.

- No catálogo do Visual Studio, há um aplicativo de prioridade de pacotes de marca.  A primeira marca padrão do Visual Studio é aplicada e, em seguida, se definido nos metadados do tópico e com suporte com o pacote de identidade visual associado (conforme definido no MSHA de instalação), a identidade visual definida pelo fornecedor será aplicada como uma substituição.

  Os elementos de identidade visual normalmente se enquadram em três categorias principais:

- Elementos de cabeçalho (exemplos incluem link de comentários, texto de aviso de isenção de responsabilidade condicional, logotipo)

- Comportamentos de conteúdo (exemplos incluem elementos de texto de controle expandir/recolher e elementos de trecho de código)

- Elementos de rodapé (exemplo de direitos autorais)

  Os itens considerados como elementos de marca incluem (detalhados nesta especificação):

- Logotipo do catálogo/produto (exemplo, Visual Studio)

- Elementos de link e email de comentários

- Texto de isenção

- Texto de direitos autorais

  Os arquivos de suporte no pacote de identidade Visual Studio Help Viewer incluem:

- Gráficos (logotipos, ícones, etc.)

- Branding.js – arquivos de script com suporte a comportamentos de conteúdo

- Branding.xml – cadeias de caracteres usadas consistentemente no conteúdo do catálogo.  Observação: para elementos de texto de localização do Visual Studio na branding.xml, inclua _locID = " \<unique value> "

- Identidade visual. css – definições de estilo para consistência de apresentação

- Imprimindo. css – definições de estilo para apresentação impressa consistente

  Conforme observado acima, os pacotes de identidade visual são associados ao tópico:

- Quando SelfBranded = false é definido nos metadados, o tópico herda o pacote de identidade visual do catálogo

- Ou quando SelfBranded = false e houver um pacote de identidade visual exclusivo definido no MSHA e disponível quando o conteúdo for instalado

  Para VSPs implementar pacotes personalizados de identidade visual (VSP, SelfBranded = true), uma maneira de prosseguir é começar com o pacote de identidade visual de fallback (instalado com o Visualizador da ajuda) e alterar o nome do arquivo conforme apropriado.  O \<locale> arquivo Branding_. mshc é um arquivo zip com a extensão de arquivo alterada para. mshc, portanto, basta alterar a extensão de. mshc para. zip e extrair o conteúdo.  Veja abaixo os elementos de pacote de identidade visual e modifique conforme apropriado (por exemplo, altere o logotipo para o logotipo VSP e a referência ao logotipo no arquivo Branding.xml, atualize Branding.xml específico de VSP etc.).

  Quando todas as modificações forem concluídas, crie um arquivo ZIP contendo os elementos de identidade visual desejados e altere a extensão para. mshc.

  Para associar o pacote de identidade visual personalizado, crie o MSHA, que contém a referência ao arquivo de identidade visual mshc junto com o conteúdo mshc (que contém os tópicos).  Consulte abaixo "MSHA" para saber como criar um MSHA básico.

  O arquivo de Branding.xml contém um elemento de lista usado para renderizar consistentemente itens específicos em um tópico quando o tópico contém \<meta name="Microsoft.Help.SelfBranded" content="false"/> .  A lista de elementos do Visual Studio no arquivo de Branding.xml está listada abaixo.  Essa lista destina-se a ser usada como um modelo para os usuários do Shell ISO, onde eles modificam esses elementos (por exemplo, logotipo, comentários e direitos autorais) para atender às suas necessidades de identidade visual do produto.

  Observação: as variáveis indicadas por "{n}" têm dependências de código – remover ou alterar esses valores causará erros e possivelmente falha do aplicativo. Os identificadores de localização (por exemplo _locID = "CodeSnippet. n") estão incluídos no pacote de identidade Visual Studio.

  **Branding.xml**

Recurso: **CollapsibleArea** use: expande recolhe o texto de controle de conteúdo

|**Elemento**|**Valor**|
|-|-|
|ExpandText|Expanda|
|CollapseText|Recolher|

Recurso:**CodeSnippet** use: texto de controle de trecho de código.  Observação: o conteúdo do trecho de código com espaço "não separável" será alterado para espaço.

|**Elemento**|**Valor**|
|-|-|
|CopyToClipboard|Copiar para a Área de Transferência|
|ViewColorizedText|Exibir colorido|
|CombinedVBTabDisplayLanguage|Visual Basic (exemplo)|
|VBDeclaration|Declaração|
|VBUsage|Uso|

Recurso: **comentários, rodapé e** uso do logotipo: forneça um controle de comentários para que o cliente forneça comentários sobre o tópico atual por email.  Texto de direitos autorais do conteúdo.  Definição do logotipo.

|**Elemento**|**Valor (essas cadeias de caracteres podem ser modificadas para atender à necessidade de conteúdo.)**|
|-|-|
|Internacionais|© 2013 Microsoft Corporation. Todos os direitos reservados.|
|SendFeedback|\<a href="{0}" {1}>Envie comentários \</a> sobre este tópico para a Microsoft.|
|FeedbackLink||
|LogoTitle|[!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)]|
|LogoFileName|vs_logo_bk.gif|
|LogoFileNameHC|vs_logo_wh.gif|

Recurso: uso de **isenção** : um conjunto de isenções de responsabilidade específicas para conteúdo traduzido do computador.

|**Elemento**|**Valor**|
|-|-|
|MT_Editable|Este artigo foi traduzido por máquina. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo.|
|MT_NonEditable|Este artigo foi traduzido por máquina. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo.|
|MT_QualityEditable|Este artigo foi traduzido manualmente. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo.|
|MT_QualityNonEditable|Este artigo foi traduzido manualmente. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo.|
|MT_BetaContents|Este artigo foi traduzido por máquina para uma versão preliminar. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo.|
|MT_BetaRecycledContents|Este artigo foi traduzido manualmente para uma versão preliminar. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo.|

Recurso: use **linktable** : suporte para links de tópico online

|**Elemento**|**Valor**|
|-|-|
|LinkTableTitle|Vincular tabela|
|TopicEnuLinkText|Exiba a versão em inglês \</a> deste tópico que está disponível no seu computador.|
|TopicOnlineLinkText|Exibir este tópico \<a href="{0}" {1}> online\</a>|
|OnlineText|Online|

Recurso: uso de **controle de áudio de vídeo** : exibir elementos e texto para conteúdo de vídeo

|**Elemento**|**Valor**|
|-|-|
|MultiMediaNotSupported|O Internet Explorer 9 ou superior deve estar instalado para dar suporte ao {0} conteúdo.|
|VideoText|exibindo vídeo|
|AudioText|áudio de streaming|
|OnlineVideoLinkText|\<p>Para exibir o vídeo associado a este tópico, clique {0} \<a href="{1}"> {2} aqui \</a> .\</p>|
|OnlineAudioLinkText|\<p>Para ouvir o áudio associado a este tópico, clique {0} \<a href="{1}"> {2} aqui \</a> .\</p>|

Recurso: **conteúdo não instalado controle** uso: elementos de texto (cadeias de caracteres) usados para a renderização de contentnotinstalled.htm

|**Elemento**|**Valor**|
|-|-|
|ContentNotInstalledTitle|Nenhum conteúdo foi encontrado no seu computador.|
|ContentNotInstalledDownloadContentText|\<p>Para baixar o conteúdo para o seu computador, \<a href="{0}" {1}> clique na guia Gerenciar \</a> .\</p>|
|ContentNotInstalledText|\<p>Nenhum conteúdo está instalado em seu computador. Consulte o administrador para a instalação do conteúdo da ajuda local.\</p>|

Recurso: **tópico não encontrado** uso de controle: elementos de texto (cadeias de caracteres) usados para a renderização de topicnotfound.htm

|**Elemento**|**Valor**|
|-|-|
|TopicNotFoundTitle|Não é possível localizar o tópico solicitado no seu computador.|
|TopicNotFoundViewOnlineText|\<p>O tópico solicitado não foi encontrado no seu computador, mas você pode \<a href="{0}" {1}> Exibir o tópico online \</a> .\</p>|
|TopicNotFoundDownloadContentText|\<p>Consulte o painel de navegação para obter links para tópicos semelhantes ou \<a href="{0}" {1}> clique na guia Gerenciar \</a> para baixar conteúdo para o seu computador.\</p>|
|TopicNotFoundText|\<p>O tópico solicitado não foi encontrado no seu computador.\</p>|

Recurso: **tópico uso de controle corrompido** : elementos de texto (cadeias de caracteres) usados para a renderização de topiccorrupted.htm

|**Elemento**|**Valor**|
|-|-|
|TopicCorruptedTitle|Não é possível exibir o tópico solicitado.|
|TopicCorruptedViewOnlineText|\<p>O Visualizador da ajuda não pode exibir o tópico solicitado. Pode haver um erro no conteúdo do tópico ou em uma dependência de sistema subjacente.\</p>|

Recurso: uso de **controle de página inicial** : texto que dá suporte à exibição do conteúdo do nó de nível superior do Help Viewer.

|**Elemento**|**Valor**|
|-|-|
|HomePageTitle|Página inicial do Help Viewer|
|HomePageIntroduction|\<p>Bem-vindo ao Microsoft Help Viewer, uma fonte essencial de informações para todos que usam ferramentas, produtos, tecnologias e serviços da Microsoft. O Help Viewer fornece acesso a informações de instruções e referência, código de exemplo, artigos técnicos e muito mais. Para localizar o conteúdo de que você precisa, procure o Sumário, use a pesquisa de texto completo ou navegue pelo conteúdo usando o índice de palavra-chave.\</p>|
|HomePageContentInstallText|\<p>\<br />Use a \<a href="{0}" {1}> guia gerenciar conteúdo \</a> para fazer o seguinte: \<ul> \<li> adicionar conteúdo ao seu computador. \</li> \<li> Verifique se há atualizações para seu conteúdo local. \</li> \<li> Remova o conteúdo do seu computador.\</li>\</ul>\</p>|
|HomePageInstalledBooks|Livros instalados|
|HomePageNoBooksInstalled|Nenhum conteúdo foi encontrado no seu computador.|
|HomePageHelpSettings|Configurações de conteúdo da ajuda|
|HomePageHelpSettingsText|\<p>Sua configuração atual é ajuda local. O Visualizador da ajuda exibe o conteúdo que você instalou em seu computador. \<br /> Para alterar a origem do conteúdo da ajuda, na barra de menus do Visual Studio, escolha \<span style="{0}"> ajuda, definir preferência de ajuda \</span> .\<br />\</p>|
|MB|MB|

 **branding.js**

 O arquivo de branding.js contém o JavaScript usado pelos elementos de identidade Visual Studio Help Viewer.  Abaixo está uma lista dos elementos de identidade visual e a função JavaScript de suporte.  Todas as cadeias de caracteres a serem localizadas para esse arquivo são definidas na seção "cadeias de caracteres localizáveis" na parte superior deste arquivo.  O arquivo ICL foi criado para as cadeias de caracteres Loc dentro do arquivo de branding.js.

|**Recurso de identidade visual**|**Função JavaScript**|**Descrição**|
|-|-|-|
|Var...||Definir variáveis|
|Obter o idioma do código do usuário|setUserPreferenceLang|mapeia um índice # para linguagem de código|
|Definir e obter valores de cookie|GetCookie, SetCookie||
|Membro herdado|changeMembersLabel|Expandir/recolher membro herdado|
|Quando SelfBranded = false|Carregamento|Leia a cadeia de caracteres de consulta para verificar se é uma solicitação de impressão.  Defina todos os trechos para focalizar a guia preferencial do usuário.  Se for uma solicitação de impressão, defina isPrinterFriendly como true. Verifique o modo de alto contraste.|
|Trecho de código|addSpecificTextLanguageTagSet||
||getIndexFromDevLang||
||ChangeTab||
||setCodesnippetLang||
||setCurrentLang||
||CopyToClipboard||
|CollapsibleArea|addToCollapsibleControlSet|Escreva todo o objeto de controle recolhível na lista.|
||CA_Click|com base no estado da área recolhível, define a imagem e o texto a serem apresentados|
|Suporte de contraste para logotipo|isBlackBackground()|Chamado para determinar se o plano de fundo é preto.  Somente preciso no modo de alto contraste.|
||isHighContrast()|usar um intervalo colorido para detectar o modo de alto contraste|
||onHighContrast (preto)|Chamado quando é detectado alto contraste|
|Funcionalidade LST|||
||addToLanSpecTextIdSet (ID)||
||updateLST(currentLang)||
||getDevLangFromCodeSnippet (Lang)||
|Funcionalidade de multimídia|legenda (início, fim, texto, estilo)||
||findAllMediaControls(normalizedId)||
||getActivePlayer(normalizedId)||
||captionsOnOff (ID)||
||totais (t)||
||getAllComments (nó)||
||styleRectify (estilo, stylevalue)||
||showCC (ID)||
||subtítulo (ID)||

 **ARQUIVOS HTM**

 O pacote de identidade visual contém um conjunto de arquivos HTM que dão suporte a cenários para a comunicação de informações de chave para ajudar os usuários de conteúdo, por exemplo, uma home page que contém uma seção que descreve quais conjuntos de conteúdo são instalados e as páginas que dizem ao usuário quando os tópicos não podem ser encontrados no conjunto de tópicos local. Esses arquivos HTM podem ser modificados por produto.  Os fornecedores de shell ISO são capazes de usar o pacote de identidade visual padrão e alterar o comportamento e o conteúdo dessas páginas para atender às suas necessidades.  Esses arquivos fazem referência ao respectivo pacote de identidade visual para que as marcas de identidade visual obtenham o conteúdo correspondente do arquivo de branding.xml.

|**Arquivo**|**Utilizá**|**Fonte de conteúdo exibida**|
|-|-|-|
|homepage.htm|Esta é uma página que exibe o conteúdo atualmente instalado e qualquer outra mensagem apropriada para apresentar ao usuário sobre seu conteúdo.  Esse arquivo tem o atributo de metadados adicional "Microsoft.Help.Id" content = "-1", que coloca esse conteúdo na parte superior do Sumário de conteúdo local.||
||<META_HOME_PAGE_TITLE_ADD/>|Branding.xml, marca\<HomePageTitle>|
||<HOME_PAGE_INTRODUCTION_SECTION_ADD/>|Branding.xml, marca\<HomePageIntroduction>|
||<HOME_PAGE_CONTENT_INSTALL_SECTION_ADD/>|Branding.xml, marca\<HomePageContentInstallText>|
||<HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD/>|A seção de título Branding.xml marca \<HomePageInstalledBooks> , os dados gerados do aplicativo, \<HomePageNoBooksInstalled> quando nenhum livro é instalado.|
||<HOME_PAGE_SETTINGS_SECTION_ADD/>|Seção de título Branding.xml marca \<HomePageHelpSettings> , texto da seção \<HomePageHelpSettingsText> .|
|topiccorrupted.htm|Quando um tópico existe no conjunto local, mas por algum motivo não pode ser exibido (conteúdo corrompido).||
||<META_TOPIC_CORRUPTED_TITLE_ADD/>|Branding.xml, marca\<TopicCorruptedTitle>|
||<TOPIC_CORRUPTED_SECTION_ADD/>|Branding.xml, marca\<TopicCorruptedViewOnlineText>|
|topicnotfound.htm|Quando um tópico não é encontrado no conjunto de conteúdo local, nem está disponível online||
||<META_TOPIC_NOT_FOUND_TITLE_ADD/>|Branding.xml, marca\<TopicNotFoundTitle>|
||<META_TOPIC_NOT_FOUND_ID_ADD/>|Branding.xml, marca\<TopicNotFoundViewOnlineText> + \<TopicNotFoundDownloadContentText>|
||<TOPIC_NOT_FOUND_SECTION_ADD/>|Branding.xml, marca\<TopicNotFoundText>|
|contentnotinstalled.htm|Quando não há nenhum conteúdo local instalado para o produto.||
||<META_CONTENT_NOT_INSTALLED_TITLE_ADD/>|Branding.xml, marca\<ContentNotInstalledTitle>|
||<META_CONTENT_NOT_INSTALLED_ID_ADD/>|Branding.xml, marca\<ContentNotInstalledDownloadContentText>|
||<CONTENT_NOT_INSTALLED_SECTION_ADD/>|Branding.xml, marca\<ContentNotInstalledText>|

 **Arquivos CSS**

 O pacote de identidade visual do Visualizador da ajuda do Visual Studio contém dois arquivos CSS para dar suporte à apresentação de conteúdo da ajuda do Visual Studio consistente:

- Branding. css – contém elementos CSS para renderização em que SelfBranded = false

- Printer. css – contém elementos CSS para renderização em que SelfBranded = false

  Os arquivos. CSS de identidade visual incluem definições para a apresentação de tópico (a limitação é que a identidade visual. css contida no Branding_ \<locale> . mshc do serviço de pacote pode ser alterada).

  **Arquivos gráficos**

  O conteúdo do Visual Studio exibe um logotipo do Visual Studio, bem como outros gráficos.  A lista completa de arquivos gráficos no pacote de identidade visual do Visualizador da ajuda é mostrada abaixo.

|**Arquivo**|**Utilizá**|**Exemplos**|
|-|-|-|
|clear.gif|Usado para renderizar a área recolhível||
|footer_slice.gif|Apresentação de rodapé||
|info_icon.gif|Usado ao exibir informações|Isenção de responsabilidade|
|online_icon.gif|Este ícone deve ser associado a links online||
|tabLeftBD.gif|Usado para renderizar o contêiner de trecho de código||
|tabRightBD.gif|Usado para renderizar o contêiner de trecho de código||
|vs_logo_bk.gif|Usado para referências de logotipo de contraste normal, conforme definido na marca Branding.xml \<LogoFileName> .  Para produtos do Visual Studio, o nome do logotipo é vs_logo_bk.gif.||
|vs_logo_wh.gif|Usado para referências de logotipo alto normal, conforme definido na marca Branding.xml \<LogoFileNameHC> .  Para produtos do Visual Studio, o nome do logotipo é vs_logo_wh.gif.||
|ccOff.png|Gráfico de legendas||
|ccOn.png|Gráfico de legendas||
|ImageSprite.png|Usado para renderizar a área recolhível|gráfico expandido ou recolher|

### <a name="deploying-a-set-of-topics"></a>Implantando um conjunto de tópicos
 Este é um tutorial simples e rápido para a criação de um conjunto de implantação de conteúdo do Help Viewer composto por um arquivo MSHA e o conjunto de cabs ou MSHCs que contém os tópicos. O MSHA é um arquivo XML que descreve um conjunto de arquivos cabs ou MSHC. O Help Viewer pode ler o MSHA para obter uma lista de conteúdo (o. CAB ou. Arquivos MSHC) disponíveis para instalação local.

 Isso é apenas um primo que descreve o esquema XML muito básico para o Help Viewer MSHA.  Há um exemplo de implementação abaixo desta breve visão geral e exemplo de arquivo HelpContentSetup. msha.

 O nome do MSHA, para os fins deste primor, é arquivo HelpContentSetup. msha (o nome do arquivo pode ser qualquer coisa, com a extensão. MSHA). Arquivo HelpContentSetup. msha (exemplo abaixo) deve conter uma lista de cabs ou MSHCs disponíveis.  O tipo de arquivo deve ser consistente dentro do MSHA (não dá suporte a uma combinação de tipos de arquivo MSHA e CAB). Para cada CAB ou MSHC, deve haver um \<div class="package"> ...\</div> (Veja o exemplo abaixo).

 Observação: no exemplo de implementação abaixo, incluímos o pacote de identidade visual. Isso é essencial para incluir a fim de obter os elementos de renderização de conteúdo do Visual Studio e os comportamentos de conteúdo necessários.

 Arquivo arquivo HelpContentSetup. msha de exemplo: (substitua "nome do conjunto de conteúdo 1" e "nome do conjunto de conteúdo 2", etc. com os nomes de arquivo.)

```html
<html>
<head />
<body class="vendor-book">
<div class="details">
<span class="vendor">Your Company</span>
<span class="locale">en-us</span>
<span class="product">Your Company Help Content</span>
<span class="name">Your Company Help Content</span>
</div>
<div class="package-list">
<div class="package">
<span class="name">Your_Company _Content_Set_1</span>
<span class="deployed">True</span>
<a class="current-link" href="Your_Company _Content_Set_1.mshc">Your_Company _Content_Set_1.mshc </a>
</div>
<div class="package">
<span class="name">Your_Company _Content_Set_2</span>
<span class="deployed">True</span>
<a class="current-link"href=" Your_Company _Content_Set_2.mshc "> Your_Company _Content_Set_2.mshc </a>
</div>.

```

1. Criar pasta local, algo como "C:\SampleContent"

2. Para este exemplo, usaremos os arquivos MSHC para conter os tópicos.  Um MSHC é um zip com a extensão de arquivo alterada de. zip para. MSHC.

3. Crie o arquivo HelpContentSetup. msha abaixo como um arquivo de texto (o bloco de notas foi usado para criar o arquivo) e salve-o na pasta indicada acima (consulte a etapa 1).

   A classe "branding" existe e é exclusiva. A mshc de identidade visual está incluída neste primor para que o conteúdo instalado tenha identidade visual, e os comportamentos de conteúdo contidos no MSHCs terão os elementos de suporte apropriados contidos no pacote de identidade visual. Sem isso, os erros ocorrerão quando o sistema procurar por itens de suporte que não fazem parte do conteúdo copiado (instalado).

   Para obter o pacote de marcas do Visual Studio, copie o arquivo Branding_en-US. mshc em C:\Arquivos de programas (x86) \Microsoft Help Viewer\v2.1\ para sua pasta de trabalho.

```html
<html>
<head />
<body class="vendor-book">
<div class="details">
<span class="vendor">Your Company</span>
<span class="locale">en-us</span>
<span class="product">Your Company Help Content</span>
<span class="name">Your Company Help Content</span>
</div>
<div class="package-list">
<div class="package">
<span class="name">Your_Company _Content_Set_1</span>
<span class="deployed">True</span>
<a class="current-link" href="Your_Company _Content_Set_1.mshc">Your_Company _Content_Set_1.mshc </a>
</div>
<div class="package">
<span class="name">Your_Company _Content_Set_2</span>
<span class="deployed">True</span>
<a class="current-link"href=" Your_Company _Content_Set_2.mshc "> Your_Company _Content_Set_2.mshc </a>
</div>
<div class="package">
<span class="packageType">branding</span>
<span class="name">Branding_en-US</span>
<span class="deployed">True</span>
<a class="current-link" href="Branding_en-US.mshc">Branding_en-US.mshc</a>
</div>
</div>
</body>
</html>

```

 **Resumo**

 Usar e estender as etapas acima permitirá que o VSPs implante seus conjuntos de conteúdo para o Visualizador da ajuda do Visual Studio.

### <a name="adding-help-to-the-visual-studio-shell-integrated-and-isolated"></a>Adicionando ajuda ao shell do Visual Studio (integrado e isolado)
 **Introdução**

 Este tutorial demonstra como incorporar o conteúdo da ajuda em um aplicativo de shell do Visual Studio e, em seguida, implantá-lo.

 **Requisitos**

1. [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)]

2. [Redistribuição de shell isolado Visual Studio 2013](https://aka.ms/VS2013/IsoShell-LP/all)

   **Visão geral**

   O [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)] shell é uma versão do [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)] IDE na qual você pode basear um aplicativo. Esses aplicativos contêm o Shell isolado junto com as extensões que você cria. Use modelos de projeto de shell isolados, que são incluídos no [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)] SDK, para criar extensões.

   As etapas básicas para criar um aplicativo baseado em shell isolado e sua ajuda:

3. Obtenha os pacotes [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)] redistribuíveis do Shell ISO (um download da Microsoft).

4. No Visual Studio, crie uma extensão de ajuda com base no Shell isolado, por exemplo, a extensão de ajuda da Contoso que é descrita mais adiante neste guia.

5. Empacote a extensão e o Shell ISO redistribuível em um MSI de implantação (uma instalação de aplicativo). Este passo a passos não inclui uma etapa de configuração.

   Crie um repositório de conteúdo do Visual Studio. Para o cenário de shell integrado, altere o Visual Studio12 para o nome do catálogo de produtos da seguinte maneira:

- Criar pasta C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio12.

- Crie um arquivo chamado CatalogType.xml e adicione-o à pasta. O arquivo deve conter as seguintes linhas de código:

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <catalogType>UserManaged</catalogType>
  ```

  Defina o repositório de conteúdo no registro. Para o Shell integrado, altere VisualStudio12 para o nome do catálogo de produtos:

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.1\Catalogs\VisualStudio12

   Chave: LocationPath valor da cadeia de caracteres: C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio12\

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.1\Catalogs\VisualStudio12\en-US

   Chave: CatalogName valor da cadeia de caracteres: [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)] documentação

  **Criar o projeto**

  Para criar uma extensão de shell isolada:

1. No Visual Studio, em **arquivo**, escolha **novo projeto**, em **outros tipos de projeto** , escolha **extensibilidade**e, em seguida, escolha **shell do Visual Studio isolado**. Nomeie o projeto `ContosoHelpShell` para criar um projeto de extensibilidade com base no modelo de shell isolado do Visual Studio.

2. No Gerenciador de Soluções, no projeto ContosoHelpShellUI, na pasta arquivos de recursos, abra ApplicationCommands. vsct. Verifique se essa linha foi comentada (pesquise por "No_Help"):`<!-- <define name=“No_HelpMenuCommands”/> -->`

3. Escolha a tecla F5 para compilar e executar a **depuração**. Na instância experimental do IDE do Shell isolado, escolha o menu **ajuda** . Verifique se a **exibição ajuda**, **adicione e remova o conteúdo da ajuda**e **defina** os comandos de preferência da ajuda.

4. No Gerenciador de Soluções, no projeto ContosHelpShell, na pasta personalização do Shell, abra ContosoHelpShell. pkgdef. Para definir o catálogo de ajuda da Contoso, adicione as seguintes linhas:

   ```
    [$RootKey$\Help]
   "Product"="Contoso"
   "Catalog"="Contoso"
   “Version"="100"
   "BrandingPackage"="ContosoBrandingPackage.mshc"
   ```

5. No Gerenciador de Soluções, no projeto ContosHelpShell, na pasta de personalização do Shell, abra ContosoHelpShell. Application. pkgdef. Para habilitar a ajuda F1, adicione as seguintes linhas:

   ```
   // F1 Help Provider

   [$RootKey$\HelpProviders\{C99BDC23-FF29-46bf-9658-ADD634CCAED8}]
   "Name"="13407"
   "Package"="{DA9FB551-C724-11d0-AE1F-00A0C90FFFC3}"
   @="Help3 Provider"
   [$RootKey$\HelpProviders]
   @="{C99BDC23-FF29-46bf-9658-ADD634CCAED8}"
   [$RootKey$\Services\{C99BDC23-FF29-46bf-9658-ADD634CCAED8}]
   "Name"="Help3 Provider"
   @="{4A791146-19E4-11D3-B86B-00C04F79F802}"
   ```

6. No Gerenciador de Soluções, no menu de contexto da solução ContosoHelpShell, escolha o item de menu **Propriedades** . Em **Propriedades de configuração**, selecione **Configuration Manager**. Na coluna **configuração** , altere cada valor de "debug" para "Release".

7. Compile a solução. Isso cria um conjunto de arquivos em uma pasta de liberação, que será usada na próxima seção.

   Para testar isso como se fosse implantado:

8. No computador em que você está implantando o contoso, instale o Shell ISO baixado (do acima).

9. Crie uma pasta em \\ \Program Files (x86) \\ e nomeie-a `Contoso` .

10. Copie o conteúdo da pasta ContosoHelpShell Release para \\ \Program Files (x86) \Contoso\ Folder.

11. Inicie o editor do registro escolhendo **executar** no menu **Iniciar** e inserindo `Regedit` . No editor do registro, escolha **arquivo**e **importar**. Navegue até a pasta do projeto ContosoHelpShell. Na subpasta ContosoHelpShell, escolha ContosoHelpShell. reg.

12. Criar um repositório de conteúdo:

     Para o Shell ISO-criar um C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\ContosoDev12 de armazenamento de conteúdo contoso

     Para o [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)] shell integrado, crie a pasta C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio12

13. Crie CatalogType.xml e adicione ao repositório de conteúdo (etapa anterior) que contém:

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

14. Adicione as seguintes chaves do registro:

     HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.1\Catalogs\VisualStudio12Key: valor da cadeia de LocationPath:

     Para o Shell ISO:

     C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio12

     [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)]Shell integrado:

     C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio12en-US

     Chave: CatalogName valor da cadeia de caracteres: [!INCLUDE[vs_dev12](../../includes/vs-dev12-md.md)] documentação. Para o Shell ISO, esse é o nome do seu catálogo.

15. Copie seu conteúdo (CABS ou MSHC e MSHA) para uma pasta local.

16. Exemplo de linha de comando de shell integrada para testar o repositório de conteúdo. Para o Shell ISO, altere os valores de catálogo e launchingApp, conforme apropriado, para corresponder ao produto.

      "C:\Arquivos de programas (x86) \Microsoft Help Viewer\v2.1\HlpViewer.exe"/catalogName VisualStudio12/helpQuery Method = "Page&ID = ContosoTopic0"/launchingApp Microsoft, VisualStudio, 12.0

17. Inicie o aplicativo contoso (da raiz do aplicativo contoso). No Shell ISO, escolha o item de menu **ajuda** e altere a **preferência de ajuda definir** para **usar a ajuda local**.

18. No Shell, escolha o item de menu **ajuda** e, em seguida, **exiba a ajuda**. O Visualizador da ajuda local deve ser iniciado. Escolha a guia **gerenciar conteúdo** . Em **origem da instalação**, escolha o botão de opção **disco** . Escolha o botão **...** e navegue até a pasta local que contém o conteúdo da Contoso (copiado para a pasta local na etapa acima). Escolha o arquivo HelpContentSetup. msha. Agora, a Contoso deve aparecer como um livro nas seleções do livro. Escolha **Adicionar**e, em seguida, escolha o botão **Atualizar** (canto inferior direito).

19. No IDE contoso, escolha a tecla F1 para testar a funcionalidade F1.

### <a name="additional-resources"></a>Recursos adicionais

Para a API de tempo de execução, consulte [API de ajuda do Windows](https://msdn.microsoft.com/library/windows/desktop/hh447318\(v=vs.85\).aspx).

Para obter mais informações sobre como aproveitar a API de ajuda, consulte [exemplos de código do Help Viewer](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples).

Para obter atualizações sobre problemas de interrupção, consulte o [Leiame do Help Viewer](https://go.microsoft.com/fwlink/?LinkId=255960).
