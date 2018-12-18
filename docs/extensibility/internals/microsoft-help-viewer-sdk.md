---
title: SDK do Microsoft Help Viewer | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: af324b141815813aec9eaadfcd9982689fdeb467
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000341"
---
# <a name="microsoft-help-viewer-sdk"></a>SDK do Microsoft Help Viewer

Este artigo contém as seguintes tarefas para integradores do Visual Studio Help Viewer:

-   Criação de um tópico (suporte a F1)

-   Criando um pacote de conteúdo de identidade visual do Help Viewer

-   Implantar um conjunto de artigos

-   Adicionando Ajuda para o shell do Visual Studio (integrado ou isolado)

-   Recursos adicionais

### <a name="creating-a-topic-f1-support"></a>Criação de um tópico (suporte a F1)
Esta seção fornece uma visão geral dos componentes de um tópico apresentado, requisitos de tópico, uma breve descrição de como criar um tópico (incluindo os requisitos de suporte F1) e, finalmente, um tópico de exemplo com seu resultado renderizado.

**Visão geral de tópico do Visualizador de ajuda**

Quando um tópico é chamado para renderização, o Visualizador da Ajuda obtém os elementos de pacote de identidade visual que estão associados com o tópico no momento da instalação ou a última atualização, juntamente com o tópico XHTML e combina os dois para resultar na exibição de conteúdo apresentada (dados de identidade Visual + dados de tópico).  O pacote de marcas contém logotipos, suporte a comportamentos de conteúdo e o texto de identidade visual (direitos autoral, etc.).  Consulte "Criar pacote de identidade visual" abaixo para obter mais informações sobre os elementos de pacote de identidade visual.  Caso não há nenhum pacote de marcas associada ao tópico, o Visualizador da Ajuda usará o pacote de marcas fallback localizado na raiz do aplicativo Visualizador da Ajuda (Branding_en US.mshc).

**Requisitos de tópico do Visualizador de ajuda**

Para ser processado corretamente dentro do Visualizador da Ajuda, o conteúdo bruto do tópico deve ser W3C básico 1.1 XHTML.

Normalmente, um tópico contém duas seções:

-   Metadados (consulte a referência de metadados de conteúdo): pai dos dados sobre o tópico, por exemplo, a ID exclusiva do tópico, o valor de palavra-chave, o tópico Sumário ID, ID do nó, etc.

-   Conteúdo do corpo: em conformidade com XHTML 1.1 da básica W3C, que inclui suporte para comportamentos de conteúdo (área recolhível, trecho de código, etc. Uma lista completa é mostrada abaixo).

Pacote de identidade visual do Visual Studio com suporte a controles:

-   Links

-   Trecho de código

-   CollapsibleArea

-   Membro herdado

-   LanguageSpecificText

Suporte para cadeias de caracteres de idioma (não diferencia maiusculas de minúsculas):

-   JavaScript

-   CSharp ou c#

-   cplusplus ou visualc + + ou c + +

-   JScript

-   Visual Basic ou do vb

-   f # ou fsharp ou fs

-   si - uma cadeia de caracteres que representa um nome de idioma

**Criação de um tópico do Visualizador da Ajuda**

Criar um novo documento XHTML chamado ContosoTopic4.htm e incluir a marca de título (abaixo).

```html
<html>
<head>
<title>Contoso Topic 4</title>
</head>

<body>

</body>
</html>

```

Em seguida, adicione dados para definir como o tópico é para ser apresentado (próprio da marca ou não), como fazer referência a este tópico para F1, em que este tópico existe dentro do Sumário, sua ID (para a referência de link por outros tópicos), etc.  Consulte a tabela "Metadados de conteúdo" abaixo para obter uma lista completa de metadados com suporte.

-   Nesse caso, usaremos nosso próprio pacote de marcas, uma variante do pacote de identidade visual do Visual Studio Help Viewer.

-   Adicionar o valor e nome de meta F1 (conteúdo de "Microsoft.Help.F1" = "ContosoTopic4") que corresponderá o valor de F1 fornecido no conjunto de propriedades do IDE.  (Consulte a seção de suporte de F1 para obter mais informações).   Esse é o valor que corresponde a F1 chamar de dentro do IDE para exibir este tópico quando F1 é escolhido no IDE.

-   Adicione a ID do tópico. Isso é a cadeia de caracteres que é usada por outros tópicos para vincular a esse tópico.  É a identificação de Visualizador de ajuda para este tópico.

-   Para o Sumário, adicione nó do pai deste tópico para definir no qual este nó de Sumário do tópico serão exibidos.

-   Para o Sumário, adicione a ordem de nó deste tópico. Quando o nó pai tem um número de nós filhos, defina na ordem de nós filho local deste tópico. Por exemplo, este tópico é o número 4 de 4 tópicos de filho.)

Seção de metadados de exemplo:

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

O corpo (sem incluir o cabeçalho e rodapé) do tópico conterá links da página, uma seção de observação, uma área recolhível, um trecho de código e uma seção de texto específicos do idioma.  Consulte a seção de identidade visual para obter informações sobre essas áreas do tópico apresentada.

1.  Adicione uma marca de título do tópico:  `<div class="title">Contoso Topic 4</div>`

2.  Adicione uma seção de Observação: `<div class="alert"> add your table tag and text </div>`

3.  Adicione uma área recolhível:  `<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4.  Adicione um trecho de código:  `<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5.  Adicionar texto do código de idioma específico: `<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />` Observe que `devLangnu=` permite que você insira outras linguagens. Por exemplo, `devLangnu="Fortran"` exibe Fortran quando o trecho de código DisplayLanguage = Fortran

6.  Adicione links de página: `<a href="ms-xhelp://?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
>  Observação: para sem suporte novo "Idioma de exibição" (exemplo, F#, Cobol, Fortran) colorização de código no trecho de código poderá ser monocromático.

**Tópico Visualizador da Ajuda do exemplo** o código ilustra como definir metadados, um trecho de código, uma área recolhível e específicos do idioma de texto.

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
        <a href="ms-xhelp://?Id=ContosoTopic1">Main Topic</a>
    </div>
 </div>
</div>
</div>
</body>
</html>
```

**Suporte de F1**

No Visual Studio, selecionar F1 gera valores fornecidos do posicionamento do cursor dentro do IDE e preenche um "recipiente" com os valores fornecidos (com base no local do cursor. Quando o cursor estiver sobre o recurso x, o recurso x está ativa/em foco e preenche o recipiente de propriedades com valores.  Quando F1 é selecionado o recipiente de propriedades é preenchido e código de F1 do Visual Studio verifica se a fonte de ajuda os clientes padrão é local ou online (on-line é o padrão), em seguida, cria a cadeia de caracteres apropriada com base nos usuários definindo (on-line é o padrão) - execução do shell (consulte o guia de administrador Ajuda do exe iniciar os parâmetros) com parâmetros para o Visualizador da Ajuda local + as palavras-chave do recipiente de se a Ajuda local é o padrão ou a URL do MSDN com a palavra-chave na lista de parâmetros.

Se três cadeias de caracteres são retornadas para F1, conhecida para como uma cadeia de caracteres com vários valores, levar o primeiro termo, procure para uma ocorrência e, se encontrado, podemos terminar; Se não, avance para a próxima cadeia de caracteres.  Ordem é importante. Apresentação as palavras-chave com vários valores deve ser uma cadeia de caracteres mais longa a cadeia de caracteres mais curta.  Para verificar isso no caso de palavras-chave de vários valores, examine a cadeia de caracteres de URL F1 online, que inclui a palavra-chave escolhida.

No Visual Studio 2012, podemos intencionalmente uma divisão mais forte entre online e offline, para que se a configuração do usuário para Online, em seguida, podemos simplesmente passada a solicitação F1 diretamente ao nosso serviço de consulta on-line no MSDN em vez de roteamento por meio do agente de biblioteca de ajuda que tínhamos no Visual Studio 2010. Em seguida, podemos contar com um estado de "conteúdo do fornecedor instalado = true" para determinar se deve fazer algo diferente nesse contexto. Se for true, em seguida, executamos essa lógica de roteamento e análise, dependendo de como você deseja dar suporte a seus clientes. Se for false, podemos ir para MSDN. Se a configuração do usuário for Local, todas as chamadas de ir para o mecanismo de ajuda local.

F1 diagrama de fluxo:

![Fluxo F1](../../extensibility/internals/media/f1flow.png "F1flow")

Quando a fonte de conteúdo de Ajuda do Visualizador da Ajuda padrão é definida como on-line (lançamento em navegador):

-   Recursos do Visual Studio Partner (VSP) emitem um valor para o recipiente F1 (prefix.keyword de recipiente da propriedade e a URL on-line para o prefixo encontrado no registro): F1 envia uma URL de VSP + parâmetros para o navegador.

-   Recursos do Visual Studio (editor de linguagem, itens de menu específico do Visual Studio, etc.): F1 envia uma URL do Visual Studio para o navegador.

Quando a fonte de conteúdo de Ajuda do Visualizador da Ajuda padrão é definida como a Ajuda local (Iniciar no Help Viewer):

-   Recursos VSP onde a palavra-chave correspondem entre o recipiente de propriedades de F1 e o índice de repositório local (ou seja, o prefix.keyword de recipiente da propriedade = valor localizado no índice de repositório local): F1 renderiza o tópico no Visualizador da Ajuda.

-   Recursos do Visual Studio (nenhuma opção para VSP substituir o recipiente de emissores de recursos do Visual Studio): F1 renderiza um tópico do Visual Studio no Visualizador da Ajuda.

Defina os seguintes valores de registro para habilitar o F1 Fallback para conteúdo de Ajuda do fornecedor. Fallback de F1 significa que o Visualizador da Ajuda é definido para procurar conteúdo de ajuda de F1 online, e o conteúdo do fornecedor está instalado localmente para o disco rígido dos usuários. O Visualizador da Ajuda deve examinar a Ajuda local para o conteúdo mesmo que a configuração padrão é para obter ajuda online.

1. Defina as **VendorContent** valor sob a chave do registro ajuda 2.3:

   -   Para sistemas operacionais de 32 bits:

        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent" = DWORD: 00000001

   -   Para sistemas operacionais de 64 bits:

        HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent" = DWORD: 00000001

2. Registre o namespace de parceiro na chave do registro ajuda 2.3:

   - Para sistemas operacionais de 32 bits:

      HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Partner<em>\\< namespace\></em>

      "local"="offline"

   - Para sistemas operacionais de 64 bits:

      HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Partner<em>\\< namespace\></em>

      "local"="offline"

**Namespace nativo de análise de base**

Para ativar a análise de um namespace base nativo, no registro de adicionar um novo DWORD pelo nome do: BaseNativeNamespaces e defina seu valor como 1 (sob a chave de catálogo que desejam dar suporte).  Por exemplo, se você quiser usar o catálogo do Visual Studio, pode adicionar a chave para o caminho:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

Quando uma palavra-chave F1 no formato de QUE CABEÇALHO/método for encontrado, o caractere '/' será analisado, resultando em construção:

-   CABEÇALHO: será o namespace que pode ser usado para se registrar no registro

-   MÉTODO: isso se tornará a palavra-chave que é passada.

Por exemplo, dada uma biblioteca personalizada chamada CustomLibrary e um método chamado MyTestMethod, quando uma solicitação chega de F1 será formatada como `CustomLibrary/MyTestMethod`.

Um usuário possa registrar CustomLibrary como o namespace sob a seção de parceiros e fornecer qualquer chave local que desejar, e a palavra-chave passada para a consulta será MyTestMethod.

**Habilitar a ferramenta no IDE de depuração de ajuda**

Adicione a seguinte chave do registro e o valor:

Tecla de Ajuda do HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Dynamic: saída de depuração de exibição do valor de varejo: Sim

No IDE, sob o item de menu de Ajuda, selecione "Depurar contexto de Ajuda"

**Metadados de conteúdo**

A tabela a seguir, qualquer cadeia de caracteres que aparece entre colchetes é um espaço reservado que deve ser substituído por um valor reconhecido. Por exemplo, em \<name="Microsoft.Help.Locale meta" conteúdo = "[código do idioma]" / >, "[código de idioma]" deve ser substituído por um valor, como "en-us".


| Propriedade (representação de HTML) | Descrição |
| - | - |
| \< conteúdo de meta name="Microsoft.Help.Locale" = "[código do idioma]" / > | Define uma localidade para este tópico. Se essa marca é usada em um tópico, ele deve ser usado apenas uma vez e deve ser inserido acima quaisquer outras marcas do Microsoft Help. Se essa marca não for usada, o texto do corpo do tópico é indexado usando o separador de palavras que está associado com a localidade do produto, se for especificado; Caso contrário, en-us é usado o separador de palavras. Essa marca é compatível com ISOC RFC 4646. Para garantir que o Microsoft Help funciona corretamente, use essa propriedade em vez do atributo de idioma geral. |
| \< conteúdo de meta name="Microsoft.Help.TopicLocale" = "[código do idioma]" / > | Define uma localidade para este tópico quando outras localidades também são usadas. Se essa marca é usada em um tópico, ele deve ser usado apenas uma vez. Use essa marca quando o catálogo contém o conteúdo em mais de um idioma. Vários tópicos em um catálogo podem ter a mesma ID, mas cada um deve especificar um TopicLocale exclusivo. O tópico que especifica um TopicLocale que corresponde à localidade do catálogo é o tópico que é exibido no sumário. No entanto, todas as versões de idioma do tópico são exibidas nos resultados da pesquisa. |
| \< título > [Title] \< /title > | Especifica o título deste tópico. Essa marca é obrigatório e deve ser usada apenas uma vez em um tópico. Se o corpo do tópico não contém um título \<div > seção, esse título é exibida no tópico e no sumário. |
| \< nome da meta = "Microsoft.Help.Keywords" conteúdo = "[aKeywordPhrase]" / > | Especifica o texto de um link que é exibido no painel de índice do Visualizador da Ajuda. Quando o link é clicado, o tópico é exibido. Você pode especificar várias palavras-chave de índice para um tópico, ou você pode omitir essa marca se não quiser links deste tópico para aparecer no índice. "K" palavras-chave de versões anteriores da Ajuda podem ser convertidas para essa propriedade. |
| \< conteúdo de meta name="Microsoft.Help.Id" = "[TopicID]" / > | Define o identificador para este tópico. Essa marca é obrigatório e deve ser usada apenas uma vez em um tópico. A ID deve ser exclusiva entre tópicos no catálogo que têm a mesma configuração de localidade. Em outro tópico, você pode criar um link para este tópico usando esta ID. |
| \< meta name="Microsoft.Help.F1" content="[System.Windows.Controls.Primitives.IRecyclingItemContainerGenerator]"/ > | Especifica a palavra-chave F1 deste tópico. Você pode especificar várias palavras-chave F1 para um tópico, ou você pode omitir essa marca se você não quiser que este tópico a ser exibido quando um usuário de aplicativo pressiona F1. Normalmente, apenas uma palavra-chave de F1 é especificada para um tópico. Palavras-chave de "F" de versões anteriores da Ajuda podem ser convertidas para essa propriedade. |
| \< nome da meta = "Descrição" content = "[Descrição do tópico]" / > | Fornece um breve resumo do conteúdo neste tópico. Se essa marca é usada em um tópico, ele deve ser usado apenas uma vez. Esta propriedade é acessada diretamente pela biblioteca de consulta; ele não é armazenado no arquivo de índice. |
| conteúdo de meta name="Microsoft.Help.TocParent" = "[parent_Id]" / > | Especifica o tópico pai deste tópico no sumário. Essa marca é obrigatório e deve ser usada apenas uma vez em um tópico. O valor é o Microsoft.Help.Id do pai. Um tópico pode ter apenas um local na tabela do conteúdo. "-1" é considerado a ID do tópico para a raiz do Sumário. No [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)], essa página é a home page do Visualizador da Ajuda. Isso é o mesmo motivo que podemos adicionar especificamente TocParent =-1 para alguns tópicos para garantir que elas aparecem na parte superior nível. Home page do Help Viewer é uma página do sistema e portanto não podem ser substituídas. Se um VSP tenta adicionar uma página com uma ID de -1, ele pode obter adicionado ao conjunto de conteúdo, mas o Help Viewer sempre usará a página do sistema - início do Help Viewer |
| \< conteúdo de meta name="Microsoft.Help.TocOrder" = "[número inteiro positivo]" / > | Especifica onde este tópico no sumário aparece em relação a seus tópicos de ponto a ponto. Essa marca é obrigatório e deve ser usada apenas uma vez em um tópico. O valor é um inteiro. Um tópico que especifica um inteiro menor valor aparece acima de um tópico que especifica um valor mais alto de inteiro. |
| \< conteúdo de meta name="Microsoft.Help.Product" = "[product code]" / > | Especifica o produto descrita neste tópico. Se essa marca é usada em um tópico, ele deve ser usado apenas uma vez. Essas informações também podem ser fornecidas como um parâmetro que é passado para o indexador de Ajuda. |
| \< conteúdo de meta name="Microsoft.Help.ProductVersion" = "[número de versão]" / > | Especifica a versão do produto descrita neste tópico. Se essa marca é usada em um tópico, ele deve ser usado apenas uma vez. Essas informações também podem ser fornecidas como um parâmetro que é passado para o indexador de Ajuda. |
| \< conteúdo de meta name="Microsoft.Help.Category" = "[string]" / > | Usado por produtos para identificar subseções de conteúdo. Você pode identificar várias subseções para um tópico, ou você pode omitir essa marca se você não quiser que os links para identificar quaisquer subseções. Essa marca é usada para armazenar os atributos para TargetOS e TargetFrameworkMoniker quando um tópico é convertido de uma versão anterior da Ajuda. O formato do conteúdo é AttributeName:AttributeValue. |
| \< conteúdo da meta name="Microsoft.Help.TopicVersion ="[número de versão de tópico]"/ > | Especifica a esta versão do tópico quando há várias versões em um catálogo. Porque Microsoft.Help.Id não é garantida para ser exclusivo, essa marca é necessária quando mais de uma versão de um tópico existe em um catálogo, por exemplo, quando um catálogo contém um tópico para o .NET Framework 3.5 e um tópico para o .NET Framework 4 e ambos têm o mesmo Micro reversível. Ajuda. |
| \< nome da meta = "SelfBranded" content = "[TRUE ou FALSE]" / > | Especifica se este tópico usa o pacote de marcas de inicialização do Gerenciador de biblioteca de Ajuda ou um pacote de marcas é específico para o tópico. Essa marca deve ser verdadeiro ou falso. Se for TRUE, em seguida, o pacote de marcas para o tópico associado substitui o pacote de marcas é definido quando inicia o Help Library Manager para que o tópico é renderizado conforme o esperado, mesmo se for diferente do processamento de outros tipos de conteúdo. Se for FALSE, o tópico atual é renderizado de acordo com o pacote de marcas é definido quando o Help Library Manager é iniciado. Por padrão, o Help Library Manager presume Self identidade visual seja false, a menos que a variável SelfBranded é declarada como TRUE; Portanto, você não precisa declarar \<nome meta = "SelfBranded" content = "Falso" / >. |

### <a name="creating-a-branding-package"></a>Criando um pacote de marcas
A versão do Visual Studio abrange um número de diferentes produtos do Visual Studio, incluindo os shells integrados e isolado para parceiros do Visual Studio.  Cada um desses produtos requer um certo grau de conteúdo da Ajuda baseado em tópico exclusivo para o produto, o suporte de identidade visual.  Por exemplo, tópicos do Visual Studio precisam ter uma apresentação consistentes de marcas, enquanto SQL Studio, que encapsula o Shell do ISO, requer sua própria exclusivo ajuda conteúdo de identidade visual para cada tópico.  Um parceiro de Shell integrado pode querer seus tópicos da Ajuda para estar dentro do pai do conteúdo de Ajuda do produto Visual Studio enquanto mantém seu próprio tópico identidade visual.

Identidade visual de pacotes é instalados pelo produto que contém o Visualizador da Ajuda.  Produtos do Visual Studio:

-   Um pacote de marcas de fallback (Branding_\<localidade >. mshc) está instalado na raiz do aplicativo de Ajuda do visualizador 2.3 (exemplo: C:\Program Files (x86) \Microsoft Help Viewer\v2.3), o pacote de idiomas do Visualizador da Ajuda.  Isso é usado para casos em que o produto identidade visual do pacote não está instalado (nenhum conteúdo foi instalado) ou em que o pacote de marcas instalado está corrompido.  Os elementos do Visual Studio (logotipo e comentários) são ignorados quando o pacote de marcas aplicativo raiz fallback é usado.

-   Quando o conteúdo do Visual Studio é instalado do serviço do pacote de conteúdo, um pacote de marcas também é instalado (para o primeiro cenário de instalação de conteúdo de tempo).  Se houver uma atualização para o pacote de marcas, a atualização é instalada quando a próxima atualização de conteúdo ou uma ação de instalação de pacote adicionais ocorre.

O Microsoft Help Viewer dá suporte à identidade visual de tópicos com base nos metadados do tópico.

-   Em que os metadados de tópico definem self da marca = true, renderizar o tópico como está, não faça nada (com relação às General a identidade visual).

-   Em que os metadados de tópico definem self da marca = false, usar o pacote de marcas associado com valor de metadados TopicVendor.

-   Conteúdo em que os metadados de tópico definem name="Microsoft.Help.TopicVendor" =\< nome de pacote de identidade visual no fornecedor MSHA >, use o pacote de marcas definido no valor do conteúdo.

-   No catálogo do Visual Studio, há um aplicativo de prioridade de pacotes de identidade visual.  Primeiro o Visual Studio identidade visual padrão é aplicada e, em seguida, se definido nos metadados do tópico e tem suporte com a identidade visual associado do pacote (conforme definido na msha a instalação), o definida pelo fornecedor de identidade visual é aplicado como uma substituição.

Elementos de identidade visual normalmente se enquadram em três categorias principais:

-   Elementos de cabeçalho (os exemplos incluem um link de comentários, o texto de aviso de isenção condicional, o logotipo)

-   Conteúdo comportamentos (exemplos incluem elementos de texto do controle de expandir/recolher e elementos de trecho de código)

-   Elementos de rodapé (exemplo Copyright)

Itens considerados como incluem elementos com marca (detalhado nessa especificação):

-   Logotipo do catálogo/produto (Visual Studio exemplo)

-   Elementos de link e o email de comentários

-   Texto de aviso de isenção

-   Texto de direitos autorais

Arquivos de suporte no pacote de identidade visual do Visual Studio Help Viewer incluem:

-   Elementos gráficos (logotipos, ícones, etc.)

-   Arquivos de script de Branding.js - comportamentos de conteúdo de suporte

-   Branding.XML - cadeias de caracteres que é usado de forma consistente entre o conteúdo do catálogo.  Observação: para elementos de texto de localização do Visual Studio em branding.xml, incluem _locID = "\<valor exclusivo >"

-   Branding.CSS - definições de estilo para consistência de apresentação

-   Printing.CSS - definições de estilo para apresentação impressa consistente

Conforme observado acima, pacotes de identidade visual são associados ao tópico:

-   Quando SelfBranded = false é definido nos metadados, o tópico herda o catálogo de pacote de identidade Visual

-   Ou quando SelfBranded = false e existe é um pacote de marca exclusivo definido no MSHA e disponível quando o conteúdo está instalado

Para VSPs Implementando pacotes de identidade visual personalizados (conteúdo VSP, SelfBranded = True), uma maneira para prosseguir é começar com o pacote de marcas de fallback (instalado com o Visualizador da Ajuda) e altere o nome do arquivo conforme apropriado.  O Branding_\<localidade >. mshc arquivo é um arquivo zip com a extensão de arquivo foi alterado para. mshc, portanto, simplesmente altere a extensão de. mshc para. zip e extraia o conteúdo.  Veja a seguir para a identidade visual de elementos do pacote e modificar conforme apropriado (por exemplo, altere o logotipo para o logotipo VSP e a referência para o logotipo no arquivo Branding.xml, atualizar Branding.xml por informações específicas VSP, etc.).

Quando todas as modificações são feitas, crie um arquivo zip que contém os elementos de identidade visual desejados e altere a extensão para. mshc.

Para associar o pacote de marcas personalizado, crie MSHA, que contém a referência ao arquivo mshc identidade visual, juntamente com o conteúdo mshc (que contém os tópicos).  Veja a seguir "MSHA" para saber como criar um MSHA básico.

O arquivo Branding.xml contém uma lista de elementos usados para renderizar consistentemente itens específicos em um tópico quando o tópico contém \<meta name="Microsoft.Help.SelfBranded" conteúdo = "false" / >.  A lista do Visual Studio de elementos no arquivo Branding.xml esteja listada abaixo.  Essa lista destina-se a ser usado como um modelo para usuários pioneiros do Shell do ISO, onde eles modificarem esses elementos (por exemplo, logotipo, comentários e direitos autorais) para atender às suas próprias marca de produto precisa.

Observação: as variáveis observadas por "{n}" tem dependências de código - remover ou alterar esses valores causará erros e, possivelmente, a falha do aplicativo. Identificadores de localização (exemplo _locID="codesnippet.n") são incluídos no pacote do Visual Studio de identidade visual.

**Branding.XML**


| | |
| - | - |
| Recurso: | **CollapsibleArea** |
| Uso: | Expandir recolhe o texto do controle de conteúdo |
| **Elemento** | **Valor** |
| ExpandText | Expandir |
| CollapseText | Recolher |
| Recurso: | **Trecho de código** |
| Uso: | Texto de controle de trecho de código.  Observação: Conteúdo do trecho de código com espaço "Não-separável" será alterado para o espaço. |
| **Elemento** | **Valor** |
| CopyToClipboard | Copiar para a Área de Transferência |
| ViewColorizedText | Exibir colorido |
| CombinedVBTabDisplayLanguage | Visual Basic (exemplo) |
| VBDeclaration | Declaração |
| VBUsage | Uso |
| Recurso: | **Comentários, o rodapé e o logotipo** |
| Uso: | Fornece um controle de comentários do cliente fornecer comentários sobre o tópico atual por email.  Texto de direitos autorais para o conteúdo.  Definição de logotipo. |
| **Elemento** | **Valor (essas cadeias de caracteres podem ser modificadas para atender à necessidade de adoção de conteúdo.)** |
| Direitos autorais | © 2013 Microsoft Corporation. Todos os direitos reservados. |
| SendFeedback | \<href = "{0}" {1}> enviar comentários\</a > sobre este tópico à Microsoft. |
| FeedbackLink | |
| LogoTitle | [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] |
| LogoFileName | vs_logo_bk.gif |
| LogoFileNameHC | vs_logo_wh.gif |
| Recurso: | **Isenção de responsabilidade** |
| Uso: | Um conjunto de avisos de isenção de caso específico para a máquina conteúdo traduzido. |
| **Elemento** | **Valor** |
| MT_Editable | Este artigo foi traduzido por máquina. Se você tiver uma conexão de Internet, selecione "Veja este tópico online" para exibir esta página em modo editável junto com o conteúdo original em inglês ao mesmo tempo. |
| MT_NonEditable | Este artigo foi traduzido por máquina. Se você tiver uma conexão de Internet, selecione "Veja este tópico online" para exibir esta página em modo editável junto com o conteúdo original em inglês ao mesmo tempo. |
| MT_QualityEditable | Este artigo foi traduzido manualmente. Se você tiver uma conexão de Internet, selecione "Veja este tópico online" para exibir esta página em modo editável junto com o conteúdo original em inglês ao mesmo tempo. |
| MT_QualityNonEditable | Este artigo foi traduzido manualmente. Se você tiver uma conexão de Internet, selecione "Veja este tópico online" para exibir esta página em modo editável junto com o conteúdo original em inglês ao mesmo tempo. |
| MT_BetaContents | Este artigo foi traduzido por máquina para uma versão preliminar. Se você tiver uma conexão de Internet, selecione "Veja este tópico online" para exibir esta página em modo editável junto com o conteúdo original em inglês ao mesmo tempo. |
| MT_BetaRecycledContents | Este artigo foi traduzido manualmente para uma versão preliminar. Se você tiver uma conexão de Internet, selecione "Veja este tópico online" para exibir esta página em modo editável junto com o conteúdo original em inglês ao mesmo tempo. |
| Recurso: | **LinkTable** |
| Uso: | Suporte para links do tópico online |
| **Elemento** | **Valor** |
| LinkTableTitle | Tabela de link |
| TopicEnuLinkText | Exibir a versão em inglês\</a > deste tópico que está disponível no seu computador. |
| TopicOnlineLinkText | Veja este tópico \<href = "{0}" {1}> online\</a > |
| OnlineText | Online |
| Recurso: | **Controle de áudio de vídeo** |
| Uso: | Exibir elementos e o texto para o conteúdo de vídeo |
| **Elemento** | **Valor** |
| MultiMediaNotSupported | Internet Explorer 9 ou posterior deve estar instalado para dar suporte a {0} conteúdo. |
| VideoText | exibindo vídeo |
| AudioText | fluxo de áudio |
| OnlineVideoLinkText | \<p > para exibir o vídeo associado a este tópico, clique em {0} \<href = "{1}" >{2}aqui\</a >.\< / p > |
| OnlineAudioLinkText | \<p > para ouvir o áudio associado a este tópico, clique em {0} \<href = "{1}" >{2}aqui\</a >.\< / p > |
| Recurso: | **Controle de conteúdo não instalado** |
| Uso: | Elementos de texto (cadeias de caracteres) usados para a renderização de contentnotinstalled.htm |
| **Elemento** | **Valor** |
| ContentNotInstalledTitle | Nenhum conteúdo foi encontrado no seu computador. |
| ContentNotInstalledDownloadContentText | \<p > para baixar o conteúdo em seu computador, \<href = "{0}" {1}> clique na guia gerenciar\</a >.\< / p > |
| ContentNotInstalledText | \<p > nenhum conteúdo é instalado em seu computador. Consulte o administrador para a instalação de conteúdo de ajuda local.  \< /p > |
| Recurso: | **Controle de tópico não encontrado** |
| Uso: | Elementos de texto (cadeias de caracteres) usados para a renderização de topicnotfound.htm |
| **Elemento** | **Valor** |
| TopicNotFoundTitle | Não é possível localizar o tópico solicitado no seu computador. |
| TopicNotFoundViewOnlineText | \<p > o tópico solicitado não foi encontrado no seu computador, mas você pode \<href = "{0}" {1}> Exibir o tópico online\</a >.\< / p > |
| TopicNotFoundDownloadContentText | \<p > consulte o painel de navegação para links para tópicos semelhantes, ou \<href = "{0}" {1}> clique na guia gerenciar\</a > para baixar o conteúdo em seu computador.\< / p > |
| TopicNotFoundText | \<p > o tópico solicitado não foi encontrado no seu computador.  \< /p > |
| Recurso: | **Tópico corrompido de controle** |
| Uso: | Elementos de texto (cadeias de caracteres) usados para a renderização de topiccorrupted.htm |
| **Elemento** | **Valor** |
| TopicCorruptedTitle | Não é possível exibir o tópico solicitado. |
| TopicCorruptedViewOnlineText | \<p > o Visualizador da Ajuda é não é possível exibir o tópico solicitado. Pode haver um erro no conteúdo do tópico ou uma dependência do sistema subjacente.  \< /p > |
| Recurso: | **Controle de página inicial** |
| Uso: | Texto de oferecer suporte à exibição do conteúdo do nó de nível superior do Visualizador da Ajuda. |
| **Elemento** | **Valor** |
| HomePageTitle | Início do Help Viewer |
| HomePageIntroduction | \<p > Bem-vindo ao Microsoft Help Viewer, uma fonte essencial de informações para todos que usam ferramentas, produtos, tecnologias e serviços da Microsoft. O Visualizador da Ajuda fornece acesso a instruções e informações de referência, código de exemplo, artigos técnicos e muito mais. Para localizar o conteúdo que você precisa, procure o sumário, use a pesquisa de texto completo ou navegue pelo conteúdo usando o palavra-chave índice.  \< /p > |
| HomePageContentInstallText | \<p >\<br / > Use o \<href = "{0}" {1}> Gerenciar conteúdo\</a > guia para fazer o seguinte:\<ul >\<li > Adicionar conteúdo ao seu computador.\< / li >\<li > Verificar se há atualizações para seu conteúdo local.\< / li >\<li > Remover o conteúdo do seu computador.\< / li >\</ul > \< /p > |
| HomePageInstalledBooks | Livros instalados |
| HomePageNoBooksInstalled | Nenhum conteúdo foi encontrado no seu computador. |
| HomePageHelpSettings | Configurações de conteúdo de ajuda |
| HomePageHelpSettingsText | \<p > sua configuração atual é a Ajuda local. O Visualizador da Ajuda exibe o conteúdo que você instalou em seu computador. \<br / > para alterar a fonte de conteúdo da Ajuda, na barra de menus do Visual Studio, escolha \<span style = "{0}" > Ajuda, definir preferência da Ajuda\</span >.\< br / > \< /p > |
| Megabytes | MB |

**branding.js**

O arquivo branding.js contém JavaScript usado pelos elementos de identidade visual do Visual Studio Help Viewer.  Abaixo está uma lista de elementos de identidade visual e a função de JavaScript de suporte.  Todas as cadeias de caracteres a ser localizada para esse arquivo são definidas na seção "Cadeias de caracteres localizáveis" na parte superior desse arquivo.  Arquivo ICL foi criado para cadeias de caracteres loc dentro do arquivo branding.js.

||||
|-|-|-|
|**Recurso de identidade Visual**|**Função JavaScript**|**Descrição**|
|Var...||Definir variáveis|
|Obter a linguagem de código do usuário|setUserPreferenceLang|mapeia um índice # para a linguagem de código|
|Definir e obter valores de cookie|getCookie, setCookie||
|Membro herdado|changeMembersLabel|Expandir/recolher membro herdado|
|Quando SelfBranded = False|onLoad|Ler a cadeia de caracteres de consulta para verificar se é uma solicitação de impressão.  Defina todos os codesnippets para se concentrar na guia preferencial do usuário.  Se for uma solicitação de impressão, em seguida, defina isPrinterFriendly como true. Verificação de modo de alto contraste.|
|Trecho de código|addSpecificTextLanguageTagSet||
||getIndexFromDevLang||
||ChangeTab||
||setCodesnippetLang||
||setCurrentLang||
||CopyToClipboard||
|CollapsibleArea|addToCollapsibleControlSet|gravar todos os objetos que o controle recolhível em lista.|
||CA_Click|com base no estado da área recolhível, define qual imagem e texto para apresentar|
|Suporte de contraste do logotipo|isBlackBackground()|Chamado para determinar se o plano de fundo é preto.  Só precisa quando no modo de alto contraste.|
||isHighContrast()|usar um span colorido para detectar o modo de alto contraste|
||onHighContrast(black)|Chamado quando o alto contraste é detectado|
|Funcionalidade LST|||
||addToLanSpecTextIdSet(id)||
||updateLST(currentLang)||
||getDevLangFromCodeSnippet(lang)||
|Funcionalidade de multimídia|legenda (Iniciar, final, texto, estilo)||
||findAllMediaControls(normalizedId)||
||getActivePlayer(normalizedId)||
||captionsOnOff(id)||
||toSeconds(t)||
||getAllComments(node)||
||styleRectify (styleName, styleValue)||
||showCC(id)||
||SubTitle(ID)||

**ARQUIVOS HTM**

O pacote de marcas contém um conjunto de arquivos HTM que dão suporte a cenários para a comunicação de informações de chave para que os usuários o conteúdo de Ajuda, por exemplo uma home page que contém uma seção que descreve quais conjuntos de conteúdo são instalados e as páginas informando ao usuário quando não é possível tópicos ser encontrada no conjunto de locais de tópicos. Esses arquivos HTM podem ser modificados por produto.  Fornecedores de Shell ISO são capazes de pegar o pacote de marcas padrão e altere o comportamento e o conteúdo dessas páginas para suite sua necessidade.  Esses arquivos se referir a seu respectivo pacote de marcas para que as marcas de identidade visual para obter o conteúdo correspondente do arquivo branding.xml.

||||
|-|-|-|
|**Arquivo**|**Use**|**Fonte de conteúdo exibido**|
|HomePage|Essa é uma página que exibe conteúdo atualmente instalado e qualquer outra mensagem apropriada para apresentar ao usuário sobre seu conteúdo.  Este arquivo tem o conteúdo adicional da meta dados atributo "Microsoft.Help.Id" = "-1", que coloca esse conteúdo na parte superior do Sumário conteúdo local.||
||&LT; META_HOME_PAGE_TITLE_ADD / &GT;|Branding.XML, marca \<HomePageTitle >|
||&LT; HOME_PAGE_INTRODUCTION_SECTION_ADD / &GT;|Branding.XML, marca \<HomePageIntroduction >|
||&LT; HOME_PAGE_CONTENT_INSTALL_SECTION_ADD / &GT;|Branding.XML, marca \<HomePageContentInstallText >|
||&LT; HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD / &GT;|Título de seção marca Branding.xml\<HomePageInstalledBooks >, os dados gerados por aplicativo, \<HomePageNoBooksInstalled > quando não há livros estão instalados.|
||&LT; HOME_PAGE_SETTINGS_SECTION_ADD / &GT;|Título de seção marca Branding.xml \<HomePageHelpSettings >, seção texto \<HomePageHelpSettingsText >.|
|topiccorrupted.htm|Quando há um tópico em conjunto local, mas por algum motivo não pode ser exibido (corrompido de conteúdo).||
||&LT; META_TOPIC_CORRUPTED_TITLE_ADD / &GT;|Branding.XML, marca \<TopicCorruptedTitle >|
||&LT; TOPIC_CORRUPTED_SECTION_ADD / &GT;|Branding.XML, marca \<TopicCorruptedViewOnlineText >|
|topicnotfound.htm|Quando um tópico não é encontrado no conteúdo do local definido nem está disponível online||
||&LT; META_TOPIC_NOT_FOUND_TITLE_ADD / &GT;|Branding.XML, marca \<TopicNotFoundTitle >|
||&LT; META_TOPIC_NOT_FOUND_ID_ADD / &GT;|Branding.XML, marca \<TopicNotFoundViewOnlineText > + \<TopicNotFoundDownloadContentText >|
||&LT; TOPIC_NOT_FOUND_SECTION_ADD / &GT;|Branding.XML, marca \<TopicNotFoundText >|
|contentnotinstalled.htm|Quando não há nenhum conteúdo local instalado para o produto.||
||&LT; META_CONTENT_NOT_INSTALLED_TITLE_ADD / &GT;|Branding.XML, marca \<ContentNotInstalledTitle >|
||&LT; META_CONTENT_NOT_INSTALLED_ID_ADD / &GT;|Branding.XML, marca \<ContentNotInstalledDownloadContentText >|
||&LT; CONTENT_NOT_INSTALLED_SECTION_ADD / &GT;|Branding.XML, marca \<ContentNotInstalledText >|

**Arquivos CSS**

O pacote Visual Studio ajuda do Visualizador de identidade visual contém dois arquivos css para dar suporte à apresentação de conteúdo ajuda do Visual Studio consistente:

-   Branding.css - contém os elementos de css para a renderização de where SelfBranded = false

-   Printer.css - contém os elementos de css para a renderização de where SelfBranded = false

Arquivos branding.CSS incluem definições para apresentação de tópico do Visual Studio (limitação é que o branding.css contido no Branding_\<localidade >. mshc do serviço do pacote pode ser alterado).

**Arquivos gráficos**

Conteúdo do Visual Studio exibe um logotipo do Visual Studio, bem como outros elementos gráficos.  A lista completa de arquivos gráficos no pacote de identidade visual do Visual Studio Help Viewer é mostrada abaixo.

||||
|-|-|-|
|**Arquivo**|**Use**|**Exemplos**|
|clear.gif|Usado para renderizar a área recolhível||
|footer_slice.gif|Apresentação do rodapé||
|info_icon.gif|Usado ao exibir informações|Aviso de isenção de responsabilidade|
|online_icon.gif|Esse ícone deve ser associada com links online||
|tabLeftBD.gif|Usado para renderizar o contêiner de trecho de código||
|tabRightBD.gif|Usado para renderizar o contêiner de trecho de código||
|vs_logo_bk.gif|Usada para referências de logotipo de contraste normal, conforme definido na marca de Branding.xml \<LogoFileName >.  Para produtos do Visual Studio, o nome do logotipo é vs_logo_bk.gif.||
|vs_logo_wh.gif|Usada para referências de logotipo alta normal, conforme definido na marca de Branding.xml \<LogoFileNameHC >.  Para produtos do Visual Studio, o nome do logotipo é vs_logo_wh.gif.||
|ccOff.png|Legendas de gráfico||
|ccOn.png|Legendas de gráfico||
|ImageSprite.png|Usado para renderizar a área recolhível|expandido ou recolher gráfico|

### <a name="deploying-a-set-of-topics"></a>Implantar um conjunto de tópicos
Este é um tutorial rápido e simple para a criação de um conjunto de implantação de conteúdo do Visualizador da Ajuda composto de um arquivo MSHA e o conjunto de cabs ou MSHCs que contém os tópicos. O MSHA é um arquivo XML que descreve um conjunto de cabs ou arquivos MSHC. O Visualizador da Ajuda podem ler o MSHA para obter uma lista de conteúdo (o. CAB ou. Arquivos MSHC) disponíveis para instalação local.

Isso é apenas um livro de instruções que descrevem o esquema XML muito básico para o MSHA de Visualizador de Ajuda.  Há um exemplo de implementação abaixo neste exemplo HelpContentSetup. msha e uma breve visão geral.

O nome do MSHA, para fins deste primer é HelpContentSetup. msha (o nome do arquivo pode ser qualquer coisa, com a extensão. MSHA). HelpContentSetup. msha (exemplo abaixo) deve conter uma lista de cabs ou MSHCs disponíveis.  O tipo de arquivo deve ser consistente dentro a MSHA (não oferece suporte a uma combinação de tipos de arquivo CAB e de MSHA). Para cada CAB ou MSHC, deve haver um \<div classe = "pacote" >... \</div > (consulte o exemplo a seguir).

Observação: no exemplo a implementação abaixo, incluímos o pacote de marcas. Isso é essencial para incluir a fim de obter o necessários elementos de renderização de conteúdo do Visual Studio e comportamentos de conteúdo.

Arquivo HelpContentSetup msha exemplo: (substitua "nome 1 do conjunto de conteúdo" e "nome do conjunto 2" etc. com seus nomes de arquivo de conteúdo.)

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

1.  Crie uma pasta local, algo como "C:\SampleContent"

2.  Neste exemplo, usaremos arquivos MSHC para conter os tópicos.  Um MSHC é um zip com a extensão de arquivo alterado de. zip para. MSHC.

3.  Criar a abaixo HelpContentSetup. msha como um arquivo de texto (bloco de notas foi usado para criar o arquivo) e salve-o para a pasta mencionada acima (consulte a etapa 1).

A classe "Marca" exista e seja exclusivo. A identidade visual mshc está incluído neste primer para que o conteúdo instalado tiver a identidade visual e os comportamentos de conteúdo que estão contidos nos MSHCs terá suporte apropriado elementos contidos no pacote de identidade visual. Sem isso, haverá erros quando o sistema procura por itens de suporte que não fazem parte do copiados (instalado) conteúdo.

Para obter o pacote de identidade visual do Visual Studio, copie o arquivo de Branding_en US.mshc em C:\Program Files (x86) \Microsoft Help Viewer\v2.3\ para sua pasta de trabalho.

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

Usando e estendendo as etapas acima permitirá VSPs implantar seus conjuntos de conteúdo para o Visual Studio Help Viewer.

### <a name="adding-help-to-the-visual-studio-shell-integrated-and-isolated"></a>Adicionar uma ajuda para o Visual Studio Shell (integrado e isolado)
**Introdução**

Este passo a passo demonstra como incorporar o conteúdo da Ajuda em um aplicativo de Shell do Visual Studio e, em seguida, implantá-lo.

**Requisitos**

1.  [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]

2.  [Pacote redistribuível do Shell de isolado do Visual Studio 2013](http://www.microsoft.com/visualstudio/11/downloads#vs-shell)

**Visão geral**

O [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Shell é uma versão dos [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] IDE no qual você pode basear um aplicativo. Esses aplicativos contêm o Shell isolado junto com as extensões que você cria. Usar modelos de projeto do Shell isolado, que são incluídos no [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] SDK, a criação de extensões.

As etapas básicas para criar um aplicativo baseado no Shell isolado e da Ajuda:

1. Obter o [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] ISO redistribuível do Shell (um download da Microsoft).

2. No Visual Studio, crie uma extensão de Ajuda que é baseada no Shell isolado do, por exemplo, a extensão de Ajuda da Contoso que é descrita posteriormente neste passo a passo.

3. Encapsule a extensão e o Shell de ISO redistribuível em uma implantação de MSI (uma configuração de aplicativo). Este passo a passo não inclui uma etapa de instalação.

Crie um repositório de conteúdo do Visual Studio. Para o cenário de Shell integrado, altere Studio12 Visual para o nome do catálogo de produto da seguinte maneira:

-   Crie pasta C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15.

-   Crie um arquivo chamado Catalogtype e adicioná-lo para a pasta. O arquivo deve conter as seguintes linhas de código:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

Defina o repositório de conteúdo no registro. Para o Shell integrado, altere VisualStudio15 para o nome do catálogo de produto:

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

   Chave: Valor de cadeia de caracteres LocationPath: C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15\

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15\en-US

   Chave: Valor de cadeia de caracteres CatalogName: [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] documentação

**Criar o projeto**

Para criar uma extensão de Shell isolado:

1.  No Visual Studio, sob **arquivo**, escolha **novo projeto**, em **Other Project Types** escolha **extensibilidade**e, em seguida, escolha  **Shell do Visual Studio isolado**. Nomeie o projeto `ContosoHelpShell`) para criar um projeto de extensibilidade com base no modelo de Shell isolado do Visual Studio.

2.  No Gerenciador de soluções, no projeto ContosoHelpShellUI, na pasta arquivos de recurso, abra ApplicationCommands.vsct. Verifique se que essa linha é comentada (procure por "No_Help"): `<!-- <define name="No_HelpMenuCommands"/> -->`

3.  Escolha a tecla F5 para compilar e executar **depurar**. Na instância experimental do IDE do Shell isolado, escolha o **ajudar** menu. Certifique-se de que o **exibir ajuda**, **adicionar e remover conteúdo da Ajuda**, e **Definir preferência da Ajuda** comandos são exibidos.

4.  No Gerenciador de soluções, no projeto ContosHelpShell, na pasta de personalização do Shell, abra ContosoHelpShell.pkgdef. Para definir o catálogo de Ajuda da Contoso, adicione as seguintes linhas:

    ```
     [$RootKey$\Help]
    "Product"="Contoso"
    "Catalog"="Contoso"
    "Version"="100"
    "BrandingPackage"="ContosoBrandingPackage.mshc"
    ```

5.  No Gerenciador de soluções, no projeto ContosHelpShell, na pasta de personalização do Shell, abra ContosoHelpShell.Application.pkgdef. Para habilitar a Ajuda de F1, adicione as seguintes linhas:

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

6.  No Solution Explorer, no menu de contexto da solução ContosoHelpShell, escolha o **propriedades** item de menu. Sob **propriedades de configuração**, selecione **Configuration Manager**. No **configuração** coluna, altere todos os valores "Debug" como "Versão".

7.  Compile a solução. Isso cria um conjunto de arquivos em uma pasta de versão, que será usada na próxima seção.

Para testar isso como se implantado:

1. No computador, você está implantando Contoso para instalar o Shell da ISO (acima) baixado.

2. Crie uma pasta na \\\Program Files (x86)\\e nomeie-o `Contoso`.

3. Copie o conteúdo da pasta da versão ContosoHelpShell para \\pasta de \Contoso\ do \Program Files (x86).

4. Inicie o Editor do registro, escolhendo **executados** na **iniciar** menu e inserindo `Regedit`. No editor do registro, escolha **arquivo**e então **importação**. Navegue até a pasta do projeto ContosoHelpShell. Na subpasta ContosoHelpShell, escolha ContosoHelpShell.reg.

5. Crie um repositório de conteúdo:

    Para o Shell ISO - criar um repositório de conteúdo do Contoso C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\ContosoDev12

    Para [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Integrated Shell, crie a pasta C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15

6. Criar Catalogtype e adicionar ao repositório de conteúdo (etapa anterior) que contém:

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <catalogType>UserManaged</catalogType>
   ```

7. Adicione as seguintes chaves do registro:

    HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15Key: Valor de cadeia de caracteres LocationPath:

    Para o Shell do ISO:

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Shell integrado:

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15en-EUA

    Chave: Valor de cadeia de caracteres CatalogName: [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] documentação. Para o Shell do ISO, isso é o nome do seu catálogo.

8. Copie o conteúdo (cabs ou MSHC e MSHA) em uma pasta local.

9. Linha de comando de Shell integrado de exemplo para testar o repositório de conteúdo. Para o Shell do ISO, altere os valores de catálogo e launchingApp conforme apropriado para coincidir com o produto.

     Método de /helpQuery /catalogName VisualStudio15 "C:\Program arquivos (x86) \Microsoft Help Viewer\v2.3\HlpViewer.exe" = "página & id = ContosoTopic0" /launchingApp Microsoft VisualStudio, 12.0

10. Inicie o aplicativo da Contoso (da raiz do aplicativo Contoso). No Shell de ISO, escolha o **ajudar** item de menu e altere o **Definir preferência da Ajuda** para **usar a Ajuda Local**.

11. Dentro do shell, escolha o **ajudar** item de menu, em seguida, **exibir ajuda**. Deve iniciar o Visualizador da Ajuda local. Escolha a guia **Gerenciar Conteúdo**. Sob **fonte de instalação**, escolha o **disco** botão de opção. Escolha o **...**  botão e navegue até a pasta local que contém o conteúdo do Contoso (copiado para a pasta local na etapa anterior). Escolha o HelpContentSetup. msha. A Contoso agora deve aparecer como um livro em seleções de livro. Escolher **Add**e, em seguida, escolha o **atualização** botão (canto inferior direito).

12. Dentro do IDE de Contoso, escolha a tecla F1 para testar a funcionalidade de F1.

### <a name="additional-resources"></a>Recursos adicionais

Para a API de tempo de execução, consulte [API de Ajuda do Windows](/previous-versions/windows/desktop/helpapi/helpapi-portal).

Para obter mais informações sobre como usar a API de Ajuda, consulte [exemplos de código do Visualizador da Ajuda](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples).

Você pode enviar sugestões de recursos no [comunidade de desenvolvedores](https://developercommunity.visualstudio.com/content/idea/post.html?space=8).