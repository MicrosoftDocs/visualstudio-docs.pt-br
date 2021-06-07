---
title: SDK do Microsoft Help Viewer | Microsoft Docs
description: Saiba mais sobre as tarefas do Visualizador de ajuda do Visual Studio, como a criação de um artigo, a criação de um pacote de identidade visual de conteúdo do Help Viewer e a implantação de um conjunto de artigos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8bc2ed473e25dc75d0155bc864aa02c157e3482f
ms.sourcegitcommit: f430d014f912aa7874e1db65026dc72688b973e4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111448318"
---
# <a name="microsoft-help-viewer-sdk"></a>SDK do Microsoft Help Viewer

Este artigo contém as seguintes tarefas para integradores do Visualizador da ajuda do Visual Studio:

- Criando um tópico (suporte F1)

- Criando um pacote de identidade visual de conteúdo do Visualizador da ajuda

- Implantando um conjunto de artigos

- Adicionando ajuda ao shell do Visual Studio (integrado ou isolado)

- Recursos adicionais

## <a name="create-a-topic-f1-support"></a>Criar um tópico (suporte F1)

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

- Other-uma cadeia de caracteres que representa um nome de idioma

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

Em seguida, adicione dados para definir como o tópico deve ser apresentado (automarcado ou não), como fazer referência a este tópico para F1, em que este tópico existe dentro do Sumário, sua ID (para referência de link por outros tópicos), etc. Consulte a tabela "metadados de conteúdo" abaixo para obter uma lista completa dos metadados com suporte.

- Nesse caso, usaremos nosso próprio pacote de marca, uma variante do pacote de identidade visual do Help Viewer.

- Adicione o meta e o valor F1 ("Microsoft. help. F1" content = "ContosoTopic4") que corresponderão ao valor F1 fornecido no recipiente de propriedades do IDE. (Consulte a seção suporte F1 para obter mais informações.) Esse é o valor que é correspondido à chamada F1 de dentro do IDE para exibir este tópico quando F1 é escolhido no IDE.

- Adicione a ID do tópico. Esta é a cadeia de caracteres usada por outros tópicos para vincular a este tópico. É a ID do Visualizador da ajuda deste tópico.

- Para o Sumário, adicione o nó pai deste tópico para definir onde este nó de Sumário do tópico será exibido.

- Para o Sumário, adicione a ordem de nó deste tópico. Quando o nó pai tem `n` o número de nós filhos, defina na ordem dos nós filho o local deste tópico. Por exemplo, este tópico é o número 4 de 4 tópicos filho.

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

O corpo (sem incluir o cabeçalho e o rodapé) do tópico conterá links de página, uma seção de observação, uma área recolhível, um trecho de código e uma seção de texto específico do idioma.  Consulte a seção identidade visual para obter informações sobre essas áreas do tópico apresentado.

1. Adicione uma marca de título de tópico:  `<div class="title">Contoso Topic 4</div>`

2. Adicionar uma seção de observação: `<div class="alert"> add your table tag and text </div>`

3. Adicione uma área recolhível:  `<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4. Adicione um trecho de código:  `<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5. Adicionar texto específico à linguagem de código:  `<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />` Observe que `devLangnu=` permite que você insira outros idiomas. Por exemplo, `devLangnu="Fortran"` exibe o Fortran quando o trecho de código DisplayLanguage = Fortran

6. Adicionar links de página: `<a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
> Observação: para uma nova colorização de código "idioma de vídeo" (exemplo, F #, COBOL, Fortran) sem suporte no trecho de código será monocromático.

**Tópico do Help Viewer de exemplo** O código ilustra como definir metadados, um trecho de código, uma área recolhível e um texto específico a um idioma.

```html
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
<li class="tocline1"><a href="#seealso" target="_self">See Also</a></li>
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
        <a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>
    </div>
 </div>
</div>
</div>
</body>
</html>
```

**Suporte a F1**

No Visual Studio, a seleção de F1 gera valores fornecidos a partir do posicionamento do cursor dentro do IDE e popula um "recipiente de propriedades" com os valores fornecidos (com base no local do cursor. Quando o cursor está sobre o recurso x, o recurso x está ativo/em foco e popula o recipiente de propriedades com valores.  Quando F1 é selecionado, o recipiente de propriedades é preenchido e o código F1 do Visual Studio procura ver se a fonte de ajuda padrão dos clientes é local ou online (online é o padrão), em seguida, cria a cadeia de caracteres apropriada com base na configuração de usuários (online é o padrão)-shell execute (consulte o guia do administrador da ajuda para parâmetros de inicialização exe) com parâmetros para a ajuda local do Help Viewer + palavra-chave do recipiente de propriedades se a ajuda local for o padrão , ou a URL do MSDN com a palavra-chave na lista de parâmetros.

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

1. Defina o valor **VendorContent** na chave do registro Help 2,3:

   - Para sistemas operacionais de 32 bits:

        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent" = DWORD: 00000001

   - Para sistemas operacionais de 64 bits:

        HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent" = DWORD: 00000001

2. Registre o namespace do parceiro na chave do registro Help 2,3:

   - Para sistemas operacionais de 32 bits:

      <em> \\ Namespace \> de<</em> de HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Partner

      "local" = "offline"

   - Para sistemas operacionais de 64 bits:

      <em> \\ Namespace \> de<</em> de HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Partner

      "local" = "offline"

**Análise de namespace nativo base**

Para ativar a análise de namespace nativo de base, no Registro, adicione uma nova DWORD pelo nome de: BaseNativeNamespaces e de definido seu valor como 1 (na chave do catálogo que deseja dar suporte).  Por exemplo, se você quiser usar o catálogo Visual Studio, poderá adicionar a chave ao caminho:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

Quando uma palavra-chave F1 no formato HEADER/METHOD for encontrada, o caractere '/' será analisado, resultando na seguinte construção:

- HEADER: será o namespace que pode ser usado para se registrar no Registro

- METHOD: isso se tornará a palavra-chave que é passada.

Por exemplo, dada uma biblioteca personalizada chamada CustomLibrary e um método chamado MyTestMethod, quando uma solicitação F1 chega, ela será formatada como `CustomLibrary/MyTestMethod` .

Em seguida, um usuário pode registrar CustomLibrary como o namespace no hive Parceiros e fornecer qualquer chave de local desejada, e a palavra-chave passada para a consulta será MyTestMethod.

**Habilitar a ferramenta de depuração de Ajuda no IDE**

Adicione a seguinte chave e valor do Registro:

::: moniker range="vs-2017"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Dynamic Help**

::: moniker-end

::: moniker range=">=vs-2019"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Dynamic Help**

::: moniker-end

Valor: Exibir saída de depuração em dados de varejo: SIM

No IDE, no item de menu Ajuda, selecione **Depurar Contexto da Ajuda**.

**Metadados de conteúdo**

Na tabela a seguir, qualquer cadeia de caracteres que aparece entre colchetes é um espaço reservado que deve ser substituído por um valor reconhecido. Por exemplo, em \<meta name="Microsoft.Help.Locale" content="[language code]" /> , "[código de linguagem]" deve ser substituído por um valor como "en-us".

| Propriedade (Representação HTML) | Descrição |
| - | - |
| \< meta name="Microsoft.Help.Locale" content="[language-code]" /> | Define uma localidade para este tópico. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez e deve ser inserida acima de qualquer outra marca de Ajuda da Microsoft. Se essa marca não for usada, o texto do corpo do tópico será indexado usando o disjuntor de palavras associado à localidade do produto, se for especificado; caso contrário, o disjuntor de palavras en-us será usado. Essa marca está em conformidade com o ISOC RFC 4646. Para garantir que a Ajuda da Microsoft funcione corretamente, use essa propriedade em vez do atributo language geral. |
| \< meta name="Microsoft.Help.TopicLocale" content="[language-code]" /> | Define uma localidade para este tópico quando outras localidades também são usadas. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez. Use essa marca quando o catálogo contiver conteúdo em mais de um idioma. Vários tópicos em um catálogo podem ter a mesma ID, mas cada um deve especificar um TopicLocale exclusivo. O tópico que especifica um TopicLocale que corresponde à localidade do catálogo é o tópico exibido no índice. No entanto, todas as versões de idioma do tópico são exibidas nos resultados da pesquisa. |
| \< title>[Título]\</title> | Especifica o título deste tópico. Essa marca é necessária e deve ser usada apenas uma vez em um tópico. Se o corpo do tópico não contém uma seção de título, este Título é exibido no tópico e no \<div> tabela de conteúdo. |
| \< meta name=" Microsoft.Help.Keywords" content="[aKeywordPhrase]"/> | Especifica o texto de um link exibido no painel de índice do Help Viewer. Quando o link é clicado, o tópico é exibido. Você pode especificar várias palavras-chave de índice para um tópico ou omitir essa marca se não quiser que os links para este tópico apareçam no índice. Palavras-chave "K" de versões anteriores da Ajuda podem ser convertidas nessa propriedade. |
| \< meta name="Microsoft.Help.Id" content="[TopicID]"/> | Define o identificador deste tópico. Essa marca é necessária e deve ser usada apenas uma vez em um tópico. A ID deve ser exclusiva entre os tópicos no catálogo que têm a mesma configuração de localidade. Em outro tópico, você pode criar um link para este tópico usando essa ID. |
| \< meta name="Microsoft.Help.F1" content="[System.Windows.Controls.Primitives.IRecyclingItemContainerGenerator]"/> | Especifica a palavra-chave F1 para este tópico. Você pode especificar várias palavras-chave F1 para um tópico ou pode omitir essa marca se não quiser que este tópico seja exibido quando um usuário do aplicativo pressionar F1. Normalmente, apenas uma palavra-chave F1 é especificada para um tópico. Palavras-chave "F" de versões anteriores da Ajuda podem ser convertidas nessa propriedade. |
| \< meta name="Description" content="[topic description]" /> | Fornece um breve resumo do conteúdo neste tópico. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez. Essa propriedade é acessada diretamente pela biblioteca de consultas; ele não é armazenado no arquivo de índice. |
| meta name="Microsoft.Help.TocParent" content="[parent_Id]"/> | Especifica o tópico pai deste tópico no tabela de conteúdo. Essa marca é necessária e deve ser usada apenas uma vez em um tópico. O valor é o Microsoft.Help.Id do pai. Um tópico pode ter apenas um local no tabela de conteúdo. "-1" é considerado a ID do tópico para a raiz do TOC. No [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] , essa página é Help Viewer home page. Esse é o mesmo motivo pelo qual adicionamos especificamente TocParent=-1 a alguns tópicos para garantir que eles aparecem no nível superior. A página do Help Viewer home page é uma página do sistema e, portanto, não substituível. Se um VSP tentar adicionar uma página com uma ID de -1, ela poderá ser adicionada ao conjunto de conteúdo, mas o Help Viewer sempre usará a página do sistema – Página Inicial do Help Viewer |
| \< meta name="Microsoft.Help.TocOrder" content="[positive integer]"/> | Especifica onde no tabela de conteúdo este tópico aparece em relação a seus tópicos pares. Essa marca é necessária e deve ser usada apenas uma vez em um tópico. O valor é um inteiro. Um tópico que especifica um inteiro de valor inferior é exibido acima de um tópico que especifica um inteiro de valor mais alto. |
| \< meta name="Microsoft.Help.Product" content="[product code]"/> | Especifica o produto que este tópico descreve. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez. Essas informações também podem ser fornecidas como um parâmetro que é passado para o Help Indexer. |
| \< meta name="Microsoft.Help.ProductVersion" content="[version number]"/> | Especifica a versão do produto que este tópico descreve. Se essa marca for usada em um tópico, ela deverá ser usada apenas uma vez. Essas informações também podem ser fornecidas como um parâmetro que é passado para o Help Indexer. |
| \< meta name="Microsoft.Help.Category" content="[string]"/> | Usado por produtos para identificar subseções de conteúdo. Você pode identificar várias subseções para um tópico ou omitir essa marca se não quiser links para identificar subseções. Essa marca é usada para armazenar os atributos para TargetOS e TargetFrameworkMoniker quando um tópico é convertido de uma versão anterior da Ajuda. O formato do conteúdo é AttributeName:AttributeValue. |
| \< meta name="Microsoft.Help.TopicVersion content="[topic version number]"/> | Especifica essa versão do tópico quando existem várias versões em um catálogo. Como Microsoft.Help.Id não é garantido que seja exclusivo, essa marca é necessária quando mais de uma versão de um tópico existe em um catálogo, por exemplo, quando um catálogo contém um tópico para o .NET Framework 3.5 e um tópico para o .NET Framework 4 e ambos têm o mesmo Microsoft.Help.Id. |
| \< meta name="SelfBranded" content="[TRUE or FALSE]"/> | Especifica se este tópico usa o pacote de identidade visual de start-up do Gerenciador de Biblioteca de Ajuda ou um pacote de identidade visual específico para o tópico. Essa marca deve ser TRUE ou FALSE. Se for TRUE, o pacote de identidade visual do tópico associado substituirá o pacote de identidade visual que é definido quando o Gerenciador de Biblioteca de Ajuda é iniciado para que o tópico seja renderizado conforme o esperado, mesmo que ele seja diferente da renderização de outro conteúdo. Se for FALSE, o tópico atual será renderizado de acordo com o pacote de identidade visual definido quando o Gerenciador de Biblioteca de Ajuda for iniciado. Por padrão, o Gerenciador de Biblioteca de Ajuda assume que a identidade visual é falsa, a menos que a variável SelfBranded seja declarada como TRUE; portanto, você não precisa declarar \<meta name="SelfBranded" content="FALSE"/> . |

## <a name="create-a-branding-package"></a>Criar um pacote de identidade visual

A Visual Studio versão abrange vários produtos Visual Studio, incluindo os shells isolados e integrados para Visual Studio Parceiros.  Cada um desses produtos requer algum grau de suporte de identidade visual de conteúdo da Ajuda baseado em tópico, exclusivo para o produto.  Por exemplo, Visual Studio tópicos precisam ter uma apresentação de marca consistente, enquanto o SQL Studio, que envolve o SHELL ISO, requer sua própria identidade visual de conteúdo da Ajuda exclusiva para cada tópico.  Um Parceiro do Shell Integrado pode querer que seus tópicos de Ajuda sejam dentro do conteúdo da Ajuda do Visual Studio do produto, mantendo sua própria identidade visual do tópico.

Os pacotes de identidade visual são instalados pelo produto que contém o Help Viewer.  Para Visual Studio produtos:

- Um pacote de identidade visual de fallback (Branding_ .mshc) é instalado na raiz do aplicativo \<locale> Help Viewer 2.3 (exemplo: C:\Program Files (x86)\Microsoft Help Viewer\v2.3) pelo pacote de idiomas do Help Viewer.  Isso é usado para casos em que o pacote de identidade visual do produto não está instalado (nenhum conteúdo foi instalado) ou em que o pacote de identidade visual instalado está corrompido.  Os Visual Studio (logotipo e Comentários) são ignorados quando o pacote de identidade visual de fallback raiz do aplicativo é usado.

- Quando Visual Studio conteúdo é instalado do serviço de pacote de conteúdo, um pacote de identidade visual também é instalado (pela primeira vez no cenário de instalação de conteúdo).  Se houver uma atualização para o pacote de identidade visual, a atualização será instalada quando ocorrer a próxima atualização de conteúdo ou ação adicional de instalação do pacote.

O Microsoft Help Viewer dá suporte à identidade visual de tópicos com base nos metadados do tópico.

- Em que os metadados do tópico definem a identidade visual = true, renderizar o tópico como está, não faça nada (tanto quanto a identidade visual).

- Em que os metadados do tópico definem a identidade visual = false, use o pacote de identidade visual associado ao valor de metadados TopicVendor.

- Em que os metadados do tópico definem name="Microsoft.Help.TopicVendor" content= , use o pacote \< branding package name in vendor MSHA> de identidade visual definido no valor do conteúdo.

- No catálogo Visual Studio, há um aplicativo de prioridade de Pacotes de Identidade Visual.  Primeiro Visual Studio a identidade visual padrão é aplicada e, em seguida, se definida nos metadados do tópico e tem suporte com o pacote de identidade visual associado (conforme definido no msha de instalação), a identidade visual definida pelo fornecedor é aplicada como uma substituição.

Elementos de identidade visual normalmente se enquadram em três categorias principais:

- Elementos de título (exemplos incluem link de comentários, texto de isenção de responsabilidade condicional, logotipo)

- Comportamentos de conteúdo (exemplos incluem elementos de texto de controle expandir/recolher e elementos de trecho de código)

- Elementos de rodapé (exemplo de direitos autorais)

Os itens considerados como elementos de marca incluem (detalhados nesta especificação):

- Logotipo do catálogo/produto (exemplo, Visual Studio)

- Elementos de link e email de comentários

- Texto de aviso de isenção de responsabilidade

- Texto de direitos autorais

Os arquivos de suporte no pacote de identidade Visual Studio Help Viewer incluem:

- Gráficos (logotipos, ícones, etc.)

- Arquivos de Branding.js-script com suporte a comportamentos de conteúdo

- Branding.xml-cadeias de caracteres usadas consistentemente no conteúdo do catálogo.  Observação: para elementos de texto de localização do Visual Studio na branding.xml, inclua _locID = " \<unique value> "

- Definições de estilo de marca. CSS para consistência de apresentação

- Imprimindo definições de estilo CSS para apresentação impressa consistente

Conforme observado acima, os pacotes de identidade visual são associados ao tópico:

- Quando SelfBranded = false é definido nos metadados, o tópico herda o pacote de identidade visual do catálogo

- Ou quando SelfBranded = false e houver um pacote de identidade visual exclusivo definido no MSHA e disponível quando o conteúdo for instalado

Para VSPs implementar pacotes personalizados de identidade visual (VSP, SelfBranded = true), uma maneira de prosseguir é começar com o pacote de identidade visual de fallback (instalado com o Visualizador da ajuda) e alterar o nome do arquivo conforme apropriado.  O \<locale> arquivo Branding_. mshc é um arquivo zip com a extensão de arquivo alterada para. mshc, portanto, basta alterar a extensão de. mshc para .zip e extrair o conteúdo.  Veja abaixo os elementos de pacote de identidade visual e modifique conforme apropriado (por exemplo, altere o logotipo para o logotipo VSP e a referência ao logotipo no arquivo Branding.xml, atualize Branding.xml específico de VSP etc.).

Quando todas as modificações forem concluídas, crie um arquivo ZIP contendo os elementos de identidade visual desejados e altere a extensão para. mshc.

Para associar o pacote de identidade visual personalizado, crie o MSHA, que contém a referência ao arquivo de identidade visual mshc junto com o conteúdo mshc (que contém os tópicos).  Consulte abaixo "MSHA" para saber como criar um MSHA básico.

O arquivo de Branding.xml contém uma lista de elementos usados para processar consistentemente itens específicos em um tópico quando o tópico contém \<meta name="Microsoft.Help.SelfBranded" content="false"/> .  A lista de elementos do Visual Studio no arquivo de Branding.xml está listada abaixo.  Essa lista destina-se a ser usada como um modelo para os usuários do Shell ISO, onde eles modificam esses elementos (por exemplo, logotipo, comentários e direitos autorais) para atender às suas necessidades de identidade visual do produto.

Observação: as variáveis indicadas por "{n}" têm dependências de código-a remoção ou alteração desses valores causará erros e possivelmente falha do aplicativo. Os identificadores de localização (por exemplo _locID = "CodeSnippet. n") estão incluídos no pacote de identidade Visual Studio.

**Branding.xml**

| Elemento | Descrição |
| - | - |
| Recurso: | **CollapsibleArea** |
| Use: | Expande recolhe o texto de controle de conteúdo |
| **Element** | **Valor** |
| ExpandText | Expanda |
| CollapseText | Recolher |
| Recurso: | **CodeSnippet** |
| Use: | Texto de controle de trecho de código.  Observação: o conteúdo do trecho de código com espaço "não separável" será alterado para espaço. |
| **Element** | **Valor** |
| CopyToClipboard | Copiar para a Área de Transferência |
| ViewColorizedText | Exibir colorido |
| CombinedVBTabDisplayLanguage | Visual Basic (exemplo) |
| VBDeclaration | Declaração |
| VBUsage | Uso |
| Recurso: | **Comentários, rodapé e logotipo** |
| Use: | Forneça um controle de comentários para que o cliente forneça comentários sobre o tópico atual por email.  Texto de direitos autorais do conteúdo.  Definição do logotipo. |
| **Element** | **Valor (essas cadeias de caracteres podem ser modificadas para atender à necessidade de conteúdo.)** |
| Internacionais | © 2013 Microsoft Corporation. Todos os direitos reservados. |
| SendFeedback | \<a href="{0}" {1}>Envie comentários \</a> sobre este tópico para a Microsoft. |
| FeedbackLink | |
| LogoTitle | [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] |
| LogoFileName | vs_logo_bk.gif |
| LogoFileNameHC | vs_logo_wh.gif |
| Recurso: | **Aviso de isenção de responsabilidade** |
| Use: | Um conjunto de isenções específicas do caso para conteúdo traduzido por computador. |
| **Element** | **Valor** |
| MT_Editable | Este artigo foi traduzido por máquina. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo. |
| MT_NonEditable | Este artigo foi traduzido por máquina. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo. |
| MT_QualityEditable | Este artigo foi traduzido manualmente. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo. |
| MT_QualityNonEditable | Este artigo foi traduzido manualmente. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo. |
| MT_BetaContents | Este artigo foi traduzido por máquina para uma versão preliminar. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo. |
| MT_BetaRecycledContents | Este artigo foi traduzido manualmente para uma versão preliminar. Se você tiver uma conexão com a Internet, selecione "exibir este tópico online" para exibir essa página no modo editável com o conteúdo original em inglês ao mesmo tempo. |
| Recurso: | **Linktable** |
| Use: | Suporte para links de tópico online |
| **Element** | **Valor** |
| LinkTableTitle | Vincular tabela |
| TopicEnuLinkText | Exiba a versão em inglês \</a> deste tópico que está disponível no seu computador. |
| TopicOnlineLinkText | Exibir este tópico \<a href="{0}" {1}> online\</a> |
| OnlineText | Online |
| Recurso: | **Controle de áudio de vídeo** |
| Use: | Exibir elementos e texto para conteúdo de vídeo |
| **Element** | **Valor** |
| MultiMediaNotSupported | O Internet Explorer 9 ou superior deve estar instalado para dar suporte ao {0} conteúdo. |
| VideoText | exibindo vídeo |
| AudioText | áudio de streaming |
| OnlineVideoLinkText | \<p>Para exibir o vídeo associado a este tópico, clique {0} \<a href="{1}"> {2} aqui \</a> .\</p> |
| OnlineAudioLinkText | \<p>Para ouvir o áudio associado a este tópico, clique {0} \<a href="{1}"> {2} aqui \</a> .\</p> |
| Recurso: | **Controle de conteúdo não instalado** |
| Use: | Elementos de texto (cadeias de caracteres) usados para o processamento de contentnotinstalled.htm |
| **Element** | **Valor** |
| ContentNotInstalledTitle | Nenhum conteúdo foi encontrado no seu computador. |
| ContentNotInstalledDownloadContentText | \<p>Para baixar o conteúdo para o seu computador, \<a href="{0}" {1}> clique na guia Gerenciar \</a> .\</p> |
| ContentNotInstalledText | \<p>Nenhum conteúdo está instalado em seu computador. Consulte o administrador para a instalação do conteúdo da ajuda local.\</p> |
| Recurso: | **Controle de tópico não encontrado** |
| Use: | Elementos de texto (cadeias de caracteres) usados para o processamento de topicnotfound.htm |
| **Element** | **Valor** |
| TopicNotFoundTitle | Não é possível localizar o tópico solicitado no seu computador. |
| TopicNotFoundViewOnlineText | \<p>O tópico solicitado não foi encontrado no seu computador, mas você pode \<a href="{0}" {1}> Exibir o tópico online \</a> .\</p> |
| TopicNotFoundDownloadContentText | \<p>Consulte o painel de navegação para obter links para tópicos semelhantes ou \<a href="{0}" {1}> clique na guia Gerenciar \</a> para baixar conteúdo para o seu computador.\</p> |
| TopicNotFoundText | \<p>O tópico solicitado não foi encontrado no seu computador.\</p> |
| Recurso: | **Tópico controle corrompido** |
| Use: | Elementos de texto (cadeias de caracteres) usados para o processamento de topiccorrupted.htm |
| **Element** | **Valor** |
| TopicCorruptedTitle | Não é possível exibir o tópico solicitado. |
| TopicCorruptedViewOnlineText | \<p>O Visualizador da ajuda não pode exibir o tópico solicitado. Pode haver um erro no conteúdo do tópico ou em uma dependência de sistema subjacente.\</p> |
| Recurso: | **Controle de página inicial** |
| Use: | Texto que dá suporte à exibição do conteúdo do nó de nível superior do Help Viewer. |
| **Element** | **Valor** |
| HomePageTitle | Página inicial do Help Viewer |
| HomePageIntroduction | \<p>Bem-vindo ao Microsoft Help Viewer, uma fonte essencial de informações para todos que usam ferramentas, produtos, tecnologias e serviços da Microsoft. O Help Viewer fornece acesso a informações de instruções e referência, código de exemplo, artigos técnicos e muito mais. Para localizar o conteúdo de que você precisa, procure o Sumário, use a pesquisa de texto completo ou navegue pelo conteúdo usando o índice de palavra-chave.\</p> |
| HomePageContentInstallText | \<p>\<br />Use a \<a href="{0}" {1}> guia gerenciar conteúdo \</a> para fazer o seguinte: \<ul> \<li> adicionar conteúdo ao seu computador. \</li> \<li> Verifique se há atualizações para seu conteúdo local. \</li> \<li> Remova o conteúdo do seu computador.\</li>\</ul>\</p> |
| HomePageInstalledBooks | Livros instalados |
| HomePageNoBooksInstalled | Nenhum conteúdo foi encontrado no seu computador. |
| HomePageHelpSettings | Configurações de conteúdo da ajuda |
| HomePageHelpSettingsText | \<p>Sua configuração atual é ajuda local. O Visualizador da ajuda exibe o conteúdo que você instalou em seu computador. \<br /> Para alterar a origem do conteúdo da ajuda, na barra de menus do Visual Studio, escolha \<span style="{0}"> ajuda, definir preferência de ajuda \</span> .\<br />\</p> |
| MB | MB |

**branding.js**

O arquivo de branding.js contém o JavaScript usado pelos elementos de identidade Visual Studio Help Viewer.  Abaixo está uma lista dos elementos de identidade visual e a função JavaScript de suporte.  Todas as cadeias de caracteres a serem localizadas para esse arquivo são definidas na seção "cadeias de caracteres localizáveis" na parte superior deste arquivo.  O arquivo ICL foi criado para as cadeias de caracteres Loc dentro do arquivo de branding.js.

|**Recurso de identidade visual**|**Função JavaScript**|**Descrição**|
|-|-|-|
|Var...||Definir variáveis|
|Obter o idioma do código do usuário|setUserPreferenceLang|mapeia um índice # para linguagem de código|
|Definir e obter valores de cookie|GetCookie, SetCookie||
|Membro herdado|changeMembersLabel|Expandir/recolher membro herdado|
|Quando SelfBranded = false|Carregamento|Leia a cadeia de caracteres de consulta para verificar se é uma solicitação de impressão.  Defina todos os trechos para focalizar a guia preferencial do usuário.  Se for uma solicitação de impressão, defina isPrinterFriendly como true. Verifique o modo de alto contraste.|
|Snippet de código|addSpecificTextLanguageTagSet||
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

|**Arquivo**|**Uso**|**Fonte de conteúdo exibida**|
|-|-|-|
|homepage.htm|Esta é uma página que exibe o conteúdo atualmente instalado e qualquer outra mensagem apropriada para apresentar ao usuário sobre seu conteúdo.  Esse arquivo tem o atributo de metadados adicional "Microsoft.Help.Id" content = "-1", que coloca esse conteúdo na parte superior do Sumário de conteúdo local.||
||<META_HOME_PAGE_TITLE_ADD/>|Branding.xml, marca \<HomePageTitle>|
||<HOME_PAGE_INTRODUCTION_SECTION_ADD/>|Branding.xml, marca \<HomePageIntroduction>|
||<HOME_PAGE_CONTENT_INSTALL_SECTION_ADD/>|Branding.xml, marca \<HomePageContentInstallText>|
||<HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD/>|A seção de título Branding.xml marca \<HomePageInstalledBooks> , os dados gerados do aplicativo,  \<HomePageNoBooksInstalled> quando nenhum livro é instalado.|
||<HOME_PAGE_SETTINGS_SECTION_ADD/>|Seção de título Branding.xml marca \<HomePageHelpSettings> , texto da seção \<HomePageHelpSettingsText> .|
|topiccorrupted.htm|Quando um tópico existe no conjunto local, mas por algum motivo não pode ser exibido (conteúdo corrompido).||
||<META_TOPIC_CORRUPTED_TITLE_ADD/>|Branding.xml, marca \<TopicCorruptedTitle>|
||<TOPIC_CORRUPTED_SECTION_ADD/>|Branding.xml, marca \<TopicCorruptedViewOnlineText>|
|topicnotfound.htm|Quando um tópico não é encontrado no conjunto de conteúdo local, nem está disponível online||
||<META_TOPIC_NOT_FOUND_TITLE_ADD/>|Branding.xml, marca \<TopicNotFoundTitle>|
||<META_TOPIC_NOT_FOUND_ID_ADD/>|Branding.xml, marca \<TopicNotFoundViewOnlineText> + \<TopicNotFoundDownloadContentText>|
||<TOPIC_NOT_FOUND_SECTION_ADD/>|Branding.xml, marca \<TopicNotFoundText>|
|contentnotinstalled.htm|Quando não há nenhum conteúdo local instalado para o produto.||
||<META_CONTENT_NOT_INSTALLED_TITLE_ADD/>|Branding.xml, marca \<ContentNotInstalledTitle>|
||<META_CONTENT_NOT_INSTALLED_ID_ADD/>|Branding.xml, marca \<ContentNotInstalledDownloadContentText>|
||<CONTENT_NOT_INSTALLED_SECTION_ADD/>|Branding.xml, marca \<ContentNotInstalledText>|

**Arquivos CSS**

O pacote de identidade visual do Visualizador da ajuda do Visual Studio contém dois arquivos CSS para dar suporte à apresentação de conteúdo da ajuda do Visual Studio consistente:

- Branding. css-contém elementos CSS para renderização em que SelfBranded = false

- Printer. css-contém elementos CSS para renderização em que SelfBranded = false

Os arquivos. CSS de identidade visual incluem definições para a apresentação de tópico (a limitação é que a identidade visual. css contida no Branding_ \<locale> . mshc do serviço de pacote pode ser alterada).

**Arquivos gráficos**

Visual Studio conteúdo exibe um Visual Studio, bem como outros elementos gráficos.  A lista completa de arquivos gráficos no pacote Visual Studio identidade visual do Help Viewer é mostrada abaixo.

|**Arquivo**|**Uso**|**Exemplos**|
|-|-|-|
|clear.gif|Usado para renderizar a Área Rebrável||
|footer_slice.gif|Apresentação do rodapé||
|info_icon.gif|Usado ao exibir informações|Isenção de responsabilidade|
|online_icon.gif|Esse ícone deve ser associado a links online||
|tabLeftBD.gif|Usado para renderizar o contêiner de snippet de código||
|tabRightBD.gif|Usado para renderizar o contêiner de snippet de código||
|vs_logo_bk.gif|Usado para referências de logotipo de contraste normal, conforme definido em Branding.xml marca \<LogoFileName> .  Para Visual Studio, o nome do logotipo é vs_logo_bk.gif.||
|vs_logo_wh.gif|Usado para referências de logotipo de alto contraste, conforme definido Branding.xml marca \<LogoFileNameHC> .  Para Visual Studio, o nome do logotipo é vs_logo_wh.gif.||
|ccOff.png|Gráfico de legenda||
|ccOn.png|Gráfico de legenda||
|ImageSprite.png|Usado para renderizar a Área Rebrável|gráfico expandido ou ressuado|

## <a name="deploy-a-set-of-topics"></a>Implantar um conjunto de tópicos

Este é um tutorial simples e rápido para criar um conjunto de implantação de conteúdo do Help Viewer composto por um arquivo MSHA e o conjunto de táxis ou MSHCs que contêm os tópicos. O MSHA é um arquivo XML que descreve um conjunto de cabs ou arquivos MSHC. O Help Viewer pode ler o MSHA para obter uma lista de conteúdo (o .CAB ou . Arquivos MSHC) disponíveis para instalação local.

Este é apenas um primer que descreve o esquema XML muito básico para o MSHA do Help Viewer.  Há um exemplo de implementação abaixo dessa breve visão geral e exemplo de HelpContentSetup.msha.

O nome da MSHA, para os fins deste primer, é HelpContentSetup.msha (o nome do arquivo pode ser qualquer coisa, com a extensão . MSHA). HelpContentSetup.msha (exemplo abaixo) deve conter uma lista dos cabs ou MSHCs disponíveis.  O tipo de arquivo deve ser consistente no MSHA (não dá suporte a uma combinação de tipos de arquivo MSHA e CAB). Para cada CAB ou MSHC, deve haver um \<div class="package"> ... \</div> (veja o exemplo abaixo).

Observação: no exemplo de implementação abaixo, incluímos o pacote de identidade visual. Isso é essencial para incluir para obter os elementos de renderização Visual Studio conteúdo necessários e comportamentos de conteúdo.

Arquivo HelpContentSetup.msha de exemplo: (substitua "nome do conjunto de conteúdo 1" e "nome do conjunto de conteúdo 2", etc., por seus nomes de arquivo.)

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

2. Neste exemplo, vamos usar arquivos MSHC para conter os tópicos.  Um MSHC é um zip com a extensão de arquivo alterada de .zip para . MSHC.

3. Crie o HelpContentSetup.msha abaixo como um arquivo de texto (o bloco de notas foi usado para criar o arquivo) e salve-o na pasta anotada acima (consulte a etapa 1).

A classe "Identidade Visual" existe e é exclusiva. O mshc de Identidade Visual está incluído neste primer para que o conteúdo instalado tenha identidade visual e os comportamentos de conteúdo contidos nos MSHCs terão os elementos de suporte apropriados contidos no pacote de identidade visual. Sem isso, os erros resultarão quando o sistema procura itens de suporte que não fazem parte do conteúdo edados (instalados).

Para obter o pacote de identidade visual Visual Studio, copie o arquivo Branding_en-US.mshc em C:\Arquivos de Programas (x86)\Microsoft Help Viewer\v2.3\ para a pasta de trabalho.

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

Usar e estender as etapas acima permitirá que os VSPs implantem seus conjuntos de conteúdo para o Visual Studio Help Viewer.

### <a name="add-help-to-the-visual-studio-shell-integrated-and-isolated"></a>Adicionar ajuda ao shell Visual Studio (integrado e isolado)

**Introdução**

Este passo a passo demonstra como incorporar o conteúdo da Ajuda em um Visual Studio Shell e implantá-lo.

**Requirements**

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]

2. [Visual Studio 2013 Redist do Shell Isolado](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

**Visão geral**

O Shell é uma versão do IDE na [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] qual você pode [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] basear um aplicativo. Esses aplicativos contêm o Shell Isolado junto com as extensões que você cria. Use modelos de projeto do Shell Isolado, que estão incluídos no [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] SDK, para criar extensões.

As etapas básicas para criar um aplicativo isolado baseado em Shell e sua Ajuda:

1. Obtenha o [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] iso shell redistribuível (um download da Microsoft).

2. No Visual Studio, crie uma extensão de Ajuda baseada no Shell Isolado, por exemplo, a extensão da Ajuda da Contoso descrita posteriormente neste passo a passo.

3. Envolva a extensão e o Shell ISO redistribuível em uma MSI de implantação (uma configuração de aplicativo). Este passo a passo não inclui uma etapa de instalação.

Crie um Visual Studio de conteúdo. Para o cenário do Shell Integrado, altere Visual Studio12 para o nome do catálogo de produtos da seguinte maneira:

- Crie a pasta C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15.

- Crie um arquivo chamado CatalogType.xml e adicione-o à pasta . O arquivo deve conter as seguintes linhas de código:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

Defina o armazenamento de conteúdo no Registro. Para o Shell Integrado, altere VisualStudio15 para o nome do catálogo de produtos:

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

   Chave: valor da cadeia de caracteres LocationPath: C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15\

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15\en-US

   Chave: Valor da cadeia de caracteres CatalogName: [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Documentação

**Criar o projeto**

Para criar uma extensão do Shell Isolado:

1. No Visual Studio, **em** Arquivo , escolha Novo  Projeto **,** em Outros Tipos de Projeto, escolha **Extensibilidade** e, em seguida, **escolha Visual Studio Shell Isolado.** Nomee o `ContosoHelpShell` projeto ) para criar um projeto de extensibilidade com base no Visual Studio Shell Isolado.

2. No Gerenciador de Soluções, no projeto ContosoHelpShellUI, na pasta Arquivos de Recursos, abra ApplicationCommands.vsct. Certifique-se de que essa linha seja comentada (pesquise "No_Help"): `<!-- <define name="No_HelpMenuCommands"/> -->`

3. Escolha a tecla F5 para compilar e executar **Depurar**. Na instância experimental do IDE do Shell Isolado, escolha o menu **Ajuda.** Certifique-se de que os comandos **Exibir Ajuda**, Adicionar e Remover **Conteúdo da** Ajuda e Definir **Preferência** da Ajuda apareçam.

4. No Gerenciador de Soluções, no projeto ContosHelpShell, na pasta Personalização do Shell, abra ContosoHelpShell.pkgdef. Para definir o catálogo da Ajuda da Contoso, adicione as seguintes linhas:

    ```
     [$RootKey$\Help]
    "Product"="Contoso"
    "Catalog"="Contoso"
    "Version"="100"
    "BrandingPackage"="ContosoBrandingPackage.mshc"
    ```

5. No Gerenciador de Soluções, no projeto ContosHelpShell, na pasta Personalização do Shell, abra ContosoHelpShell.Application.pkgdef. Para habilitar a Ajuda F1, adicione as seguintes linhas:

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

6. No Gerenciador de Soluções, no menu de contexto da solução ContosoHelpShell, escolha o item **de** menu Propriedades. Em **Propriedades de Configuração,** **selecione Gerenciador de Configurações**. Na coluna **Configuração,** altere cada valor de "Depuração" para "Versão".

7. Compile a solução. Isso cria um conjunto de arquivos em uma pasta de versão, que será usado na próxima seção.

Para testar isso como se estivesse implantado:

1. No computador em que você está implantando a Contoso, instale o Shell ISO baixado (acima).

2. Crie uma pasta em \\ \Arquivos de Programas (x86) \\ e nomee-a `Contoso` .

3. Copie o conteúdo da pasta de versão ContosoHelpShell para \\ a pasta \Arquivos de Programas (x86)\Contoso\.

4. Inicie o Editor do Registro escolhendo  **Executar** no menu **Iniciar** e inserindo `Regedit` . No editor do Registro, escolha **Arquivo** e, em seguida, **Importar**. Navegue até a pasta do projeto ContosoHelpShell. Na subpasta ContosoHelpShell, escolha ContosoHelpShell.reg.

5. Criar um armazenamento de conteúdo:

    Para o Shell ISO – crie um armazenamento de conteúdo da Contoso C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\ContosoDev12

    Para [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] o Shell Integrado, crie a pasta C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15

6. Crie CatalogType.xml e adicione ao armazenamento de conteúdo (etapa anterior) que contém:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <catalogType>UserManaged</catalogType>
   ```

7. Adicione as seguintes chaves do Registro:

    HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15Key: valor da cadeia de caracteres LocationPath:

    Para o Shell ISO:

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Shell Integrado:

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15en-US

    Chave: Valor da cadeia de caracteres CatalogName: [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Documentação. Para o Shell ISO, esse é o nome do catálogo.

8. Copie o conteúdo (cabs ou MSHC e MSHA) para uma pasta local.

9. Exemplo de linha de comando do Shell Integrado para testar o armazenamento de conteúdo. Para o Shell ISO, altere o catálogo e iniciando os valores de Aplicativo conforme apropriado para corresponder ao produto.

     "C:\Program Files (x86)\Microsoft Help Viewer\v2.3\HlpViewer.exe" /catalogName VisualStudio15 /helpQuery method="page&id=ContosoTopic0" /launchingApp Microsoft,VisualStudio,12.0

10. Iniciar o aplicativo Contoso (da raiz do aplicativo Contoso). No Shell ISO, escolha o item **de** menu Ajuda e altere a opção Definir **Preferência de Ajuda** para Usar Ajuda **Local.**

11. Dentro do shell, escolha o item de menu **Ajuda** e, em seguida, **Exibir Ajuda**. O Visualizador da Ajuda local deve ser lançado. Escolha a **guia Gerenciar Conteúdo.** Em **Origem da** Instalação, escolha o **botão Opção** de disco. Escolha o **botão ...** e navegue até a pasta local que contém o conteúdo da Contoso (copiada para a pasta local na etapa acima). Escolha HelpContentSetup.msha. A Contoso agora deve aparecer como um livro nas seleções de livros. Escolha **Adicionar** e, em seguida, escolha **o botão** Atualizar (canto inferior direito).

12. No IDE da Contoso, escolha a chave F1 para testar a funcionalidade F1.

## <a name="additional-resources"></a>Recursos adicionais

Para a API de Runtime, consulte [API de Ajuda do Windows.](/previous-versions/windows/desktop/helpapi/helpapi-portal)

Para obter mais informações sobre como aproveitar a API de Ajuda, consulte Exemplos de código do [Help Viewer](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples).

Você pode enviar sugestões de recursos [Developer Community](https://aka.ms/feedback/suggest?space=8).
