---
title: Estendendo o JavaScript IntelliSense | Microsoft Docs
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
- JavaScript, intellisense object
- extending JavaScript IntelliSense
- customizing JavaScript IntelliSense
- JavaScript, extending IntelliSense
- IntelliSense [JavaScript], extending
ms.assetid: 004e1ab6-bd7a-4327-9e01-89b9be96ba2f
caps.latest.revision: 43
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 239416a1638940207a8dcb78b395ed1915e8a93a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49867060"
---
# <a name="extending-javascript-intellisense"></a>Estendendo JavaScript IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O recurso de extensibilidade JavaScript IntelliSense permite que você personalize os resultados do IntelliSense no editor de JavaScript para bibliotecas de terceiros. Isso pode melhorar a experiência de desenvolvedores que usam essas bibliotecas.  
  
 O serviço de linguagem JavaScript fornece recursos do IntelliSense para bibliotecas de JavaScript de terceiros que são adicionadas a um projeto. Para a maioria das bibliotecas, preenchimento de declaração é fornecido automaticamente pelo serviço de linguagem. A ilustração a seguir mostra um exemplo de conclusão de instrução:  
  
 ![Exemplo de preenchimento de declaração](../ide/media/js-intellisense-completion.png "js_intellisense_completion")  
  
 Se sua biblioteca inclui descrições das variáveis, funções e objetos em marcas de comentário JavaScript padrão (/ /), você automaticamente se beneficiar, por padrão, de recursos de extensibilidade do IntelliSense, que fornecem informações descritivas em uma caixa pop-up que é exibida à direita de elementos em uma lista de conclusão ou quando você digita o parêntese de abertura em uma chamada de função. Os comentários na caixa pop-up contêm a descrição do membro. O exemplo a seguir mostra a caixa pop-up para uma lista de conclusão.  
  
 ![Exemplo de um pop de informações rápidas&#45;caixa de](../ide/media/js-intellisense-quickinfo.png "js_intellisense_quickinfo")  
  
 Para melhorar ainda mais a experiência do desenvolvedor, você talvez queira fornecer informações de tipo para os desenvolvedores na caixa pop-up. Você pode fornecer informações de tipo usando JavaScript [comentários da documentação XML](../ide/xml-documentation-comments-javascript.md) em vez de marcas de comentário padrão. Você pode adicionar comentários de documentação XML usando marcas de comentário de barra tripla (/ / /) e um conjunto definido de elementos XML.  
  
 Como alternativa, você pode fornecer informações de tipo usando a extensibilidade do IntelliSense do JavaScript. Esse recurso permite que você personalize os resultados do IntelliSense Criando extensões de JavaScript e adicioná-los para o contexto de script. Na extensão, que é um arquivo JavaScript, você assina os eventos que são expostos pelo `intellisense` objeto do serviço de linguagem. Extensibilidade do IntelliSense do JavaScript é a melhor solução para bibliotecas se um padrão de comportamento na biblioteca impede que o serviço de linguagem JavaScript oferecendo o nível desejado de suporte do IntelliSense e se uma alternativa ao XML declarativa Comentários da documentação também é necessário. Personalizando os resultados do IntelliSense, você pode criar uma experiência de IntelliSense de primeira classe, independentemente dos padrões comportamentais que poderia restringir os recursos padrão do serviço de linguagem. Para obter mais informações, consulte [preenchimento de declaração para identificadores](../ide/statement-completion-for-identifiers.md).  
  
## <a name="adding-an-extension-to-the-script-context"></a>Adicionar uma extensão para o contexto de Script  
 Para uma extensão do IntelliSense ser executado, ele precisa ser adicionado ao contexto do script atual. A extensão pode ser adicionada automaticamente ao contexto de script do mecanismo de descoberta automática, ou você pode adicionar a extensão para o contexto de script manualmente usando grupos de referência ou a diretiva de referência.  
  
 O mecanismo de descoberta automática permite que o serviço de linguagem localizar automaticamente extensões que seguem a convenção de nomenclatura de arquivo *libraryname*. intellisense.js e que estão localizados no mesmo diretório que a biblioteca que se aplica a extensão. Por exemplo, uma extensão válida para a biblioteca jQuery seria jQuery.intellisense.js. Extensões do jQuery mais restritiva, você pode usar nomes de arquivo, como jQuery-1.7.1.intellisense.js (uma extensão específica da versão) ou jQuery.ui.intellisense.js (uma extensão para uma biblioteca jQuery com escopo). A versão mais restritiva da extensão será usada se mais de uma extensão for encontrada para uma determinada biblioteca.  
  
 Se você quiser usar a extensão para todos os arquivos de projeto JavaScript, você pode em vez disso, optar por adicionar a extensão a um grupo de referência. Há vários tipos de grupos de referência, aqueles que incluem referências implícitas e aquelas que incluem referências de trabalho dedicada. Para adicionar uma extensão, você normalmente precisa adicionar o arquivo como um grupo de referência implícita, tanto **implícitas (Windows)**, **implícito (Web)**. Referências implícitas estão no escopo de cada arquivo. js aberto no Editor de código. Quando você usa esse método, você precisará adicionar a extensão e o arquivo que a extensão é complementar.  
  
 Use o **IntelliSense** página do **opções** caixa de diálogo para adicionar uma extensão como um grupo de referência. Você pode acessar o **IntelliSense** página escolhendo **ferramentas**, **opções** na barra de menus e, em seguida, escolhendo **Editor de texto**, **JavaScript**, **IntelliSense**, **referências**. Para obter mais informações sobre grupos de referência, consulte [JavaScript IntelliSense](../ide/javascript-intellisense.md) e [opções, Editor de texto, JavaScript, IntelliSense](../ide/reference/options-text-editor-javascript-intellisense.md).  
  
 Se você quiser usar a extensão para um conjunto específico de arquivos, use uma diretiva de referência. Quando você usa esse método, você precisará fazer referência a extensão e o arquivo que é complementar a extensão. Para obter informações sobre como usar a diretiva de referência, consulte [JavaScript IntelliSense](../ide/javascript-intellisense.md).  
  
## <a name="handling-intellisense-events"></a>Manipulação de eventos do IntelliSense  
 O recurso de extensibilidade permite que você personalize os resultados do IntelliSense ao assinar eventos, como o `statementcompletion` eventos do serviço de linguagem `intellisense` objeto. O exemplo a seguir mostra uma simples extensão que é usada pelo serviço de linguagem para ocultar membros que começam com um sublinhado da conclusão de instrução. Esse código está contido no underscorefilter.js e está no \\ \\ *caminho de instalação do Visual Studio*\JavaScript\References pasta.  
  
```javascript  
intellisense.addEventListener('statementcompletion', function (event) {  
    if (event.targetName === "this") return;  
  
    var filterRegex;  
  
    if (event.target === undefined || event.target === window)  
        filterRegex = /^_.*\d{2,}/;  
    else  
        filterRegex = /^_.*/;  
  
    event.items = event.items.filter(function (item) {  
        return !filterRegex.test(item.name);  
    });  
});  
```  
  
 No código anterior, a extensão verifica a [targetName propriedade](#TargetName) e [propriedade de destino](#Target) propriedades do `statementcompletion` objeto event para excluir objetos como `this` e `window`e para garantir que uma lista de conclusão de instrução válida pode ser identificada. Se uma lista de preenchimento pode ser identificada, a extensão atualiza o preenchimento de declaração [itens de propriedade](#Items) coleção pela filtragem de membros que começam com um sublinhado.  
  
 Para obter exemplos adicionais, examine os \\ \\ *caminho de instalação do Visual Studio*\JavaScript\References pasta. O arquivo showPlainComments.js nesta pasta fornece exemplos de uso de outros eventos para fornecer suporte ao IntelliSense de padrão para marcas de comentário JavaScript padrão (/ /). Como underscorefilter.js, showPlainComments.js já está disponível como uma extensão do trabalho e você pode ver as informações de IntelliSense resultantes ao usar marcas de comentário no seu código para variáveis, funções e objetos. Para obter exemplos adicionais, consulte [exemplos de código](#CodeExamples).  
  
> [!WARNING]
>  Se você modificar os arquivos de extensão incluídos com o Visual Studio, você pode desabilitar o JavaScript IntelliSense ou o recurso compatível com a extensão.  
  
 Em seu código de extensão, você pode criar manipuladores para os seguintes tipos de evento usando `addEventListener`:  
  
- `statementcompletion`, que adiciona um manipulador para um evento de conclusão de instrução. Preenchimento de declaração fornece uma lista de membros para um tipo específico que aparece depois que você digita um caractere especial como um ponto (.) ou uma lista de identificadores que aparece enquanto você digita ou quando você pressiona CTRL + J. O manipulador recebe um objeto de evento do tipo `CompletionEvent`, que suporta os seguintes membros: [itens de propriedade](#Items), [propriedade de destino](#Target), [targetName propriedade](#TargetName), e [definir o escopo de propriedade](#Scope).  
  
- `signaturehelp`, que adiciona um manipulador para informações de parâmetro do IntelliSense. Informações de parâmetro fornece informações sobre o número, nomes e tipos de parâmetros necessários para uma função. O manipulador recebe um objeto de evento do tipo `SignatureHelpEvent`, que suporta os seguintes membros: [propriedade de destino](#Target), [parentObject propriedade](#ParentObject), [functionComments propriedade](#FunctionComments), [functionHelp propriedade](#FunctionHelp).  
  
- `statementcompletionhint`, que adiciona um manipulador para informações rápidas do IntelliSense. A caixa pop-up de informações rápidas mostra a declaração completa de identificadores em seu código. O manipulador recebe um objeto de evento do tipo `CompletionHintEvent`, que suporta os seguintes membros: [completionItem propriedade](#CompletionItem), e [symbolHelp propriedade](#SymbolHelp).  
  
  Para obter exemplos que mostram os recursos como preenchimento de declaração, informações de parâmetro e informações rápidas do IntelliSense, consulte [usando o IntelliSense](../ide/using-intellisense.md).  
  
> [!NOTE]
>  No JavaScript, informações rápidas refere-se à caixa pop-up que aparece à direita de uma lista de conclusão. Você não é possível invocar informações rápidas.  
  
##  <a name="intellisenseObject"></a> IntelliSense de objeto  
 A tabela a seguir mostra as funções que estão disponíveis para o `intellisense` objeto. O `intellisense` objeto está disponível somente em tempo de design.  
  
|Função|Descrição|  
|--------------|-----------------|  
|`addEventListener(type, handler);`|Adiciona um manipulador de eventos para um evento de IntelliSense.<br /><br /> `type` é um valor de cadeia de caracteres. Os valores válidos incluem `statementcompletion`, `signaturehelp`, e `statementcompletionhint`.<br /><br /> `handler` é uma função de manipulador de eventos que recebe um objeto de evento de um dos seguintes tipos:<br /><br /> -   `CompletionEvent`, usado para o `statementcompletion` eventos.<br />-   `SignatureHelpEvent`, usado para o `signaturehelp` eventos.<br />-   `CompletionHintEvent`, usado para o `statementcompletionhint` eventos.<br /><br /> Para obter exemplos que usam essa função, consulte [exemplos de código](#CodeExamples).|  
|`annotate(obj, doc);`|Especifica a documentação para um objeto, copiando os comentários da documentação de um objeto para outro objeto.<br /><br /> `obj` Especifica o objeto no qual copiar a documentação.<br /><br /> `doc` Especifica o objeto do qual copiar a documentação.<br /><br /> Para obter um exemplo que mostra como usar essa função, consulte [adicionar anotações de IntelliSense](#Annotations).|  
|`getFunctionComments(func);`|Retorna os comentários para uma função especificada.<br /><br /> `func` Especifica a função para o qual os comentários são retornados.<br /><br /> Você pode definir as `func` parâmetro usando `completionItem.value`.<br /><br /> Retornado `functionComments` objeto inclui os seguintes membros: `above`, `inside`, e `paramComment`. Para obter mais informações, consulte o [functionComments propriedade](#FunctionComments) propriedade.<br /><br /> `getFunctionComments` pode ser chamado apenas de dentro de um dos manipuladores de eventos que são registrados por `addEventListener`.<br /><br /> Para obter um exemplo que mostra como usar essa função, consulte \\ \\ *caminho de instalação do Visual Studio*\JavaScript\References\showPlainComments.js.|  
|`logMessage(msg);`|Envia mensagens de diagnóstico para a janela de saída.<br /><br /> `msg` é uma cadeia de caracteres que contém a mensagem.<br /><br /> Para obter um exemplo que mostra como usar essa função, consulte [enviando mensagens para a janela de saída](#Logging).|  
|`nullWithCompletionsOf(value);`|Retorna um valor nulo especial para o qual a lista de preenchimento é determinada pelo objeto passado a `value` parâmetro.<br /><br /> `value` Determina a lista de conclusão para o valor retornado. `value` pode ser qualquer tipo.<br /><br /> O valor de retorno nulo é tratado como null em tempo de design, mas a lista de conclusão para o valor retornado é o mesmo que a lista de conclusão para o `value` parâmetro.<br /><br /> Um uso para essa função é para fornecer o IntelliSense para um valor retornado quando o tipo de retorno é previsível em tempo de execução, mas o valor retornado é `null` em tempo de design.|  
|`redirectDefinition(func, definition);`|Instrui o IntelliSense para usar a função de definição fornecida em vez da função func original quando a Ajuda do parâmetro ou **ir para definição** é solicitada.<br /><br /> `func` Especifica a função de destino.<br /><br /> `definition` Especifica a função a ser usado em vez da função de destino para obter informações de parâmetro e **ir para definição**.|  
|`setCallContext(func, thisArg);`|Define o contexto de chamada ou o escopo para a função especificada.<br /><br /> `func` Especifica a função para o qual definir o escopo.<br /><br /> `thisArg` é um objeto literal para o qual o `this` palavra-chave pode se referir a, que especifica o novo escopo para o membro. Você pode incluir os argumentos para passar esse parâmetro, por exemplo, `intellisense.setCallContext(func, { thisArg: "", args: [23,2] });`<br /><br /> `setCallContext` Fornece um comportamento semelhante ao `Function.prototype.bind`, exceto que ele usado apenas para suporte ao IntelliSense de tempo de design. Você pode usar `setCallContext` para definir o escopo da função, se você precisa para simular uma chamada para o código que é não caso contrário, pode ser acessado, de forma que quando você chama a função, a chamada de função incluirá o escopo correto e os argumentos.|  
|`undefinedWithCompletionsOf(value);`|Retorna um valor indefinido especial para o qual a lista de preenchimento é determinada pelo objeto passado a `value` parâmetro.<br /><br /> `value` Determina a lista de conclusão para o valor retornado. `value` pode ser qualquer tipo.<br /><br /> Retorna o indefinido valor é tratado como indefinido no tempo de design, mas após a conclusão lista para o valor retornado é o mesmo que a lista de conclusão para o `value` parâmetro.<br /><br /> Um uso para essa função é fornecer o IntelliSense para um valor retornado quando o tipo de retorno é previsível em tempo de execução, mas o valor retornado será indefinido em tempo de design.|  
|`version()`|Retorna a versão do Visual Studio.|  
  
## <a name="event-members"></a>Membros de evento  
 As seções a seguir descrevem os membros que são expostos no objeto de evento para os seguintes eventos: `statementcompletion`, `signaturehelp`, e `statementcompletionhint`.  
  
###  <a name="CompletionItem"></a> completionItem propriedade  
 Retorna o identificador, conhecido como o item de conclusão, para o qual uma caixa pop-up de informações rápidas é solicitada. Essa propriedade está disponível para o `statementcompletionhint` objeto de evento e para o [itens de propriedade](#Items) propriedade do `statementcompletion` objeto de evento.  
  
 Valor de retorno: `completionItem` objeto  
  
 A seguir é os membros do `completionItem` objeto:  
  
-   `name`. Leitura/gravação quando usado na `items` coleção; caso contrário, somente leitura. Retorna uma cadeia de caracteres que identifica o item de conclusão.  
  
-   `kind`. Leitura/gravação quando usado na `items` coleção; caso contrário, somente leitura. Retorna uma cadeia de caracteres que representa o tipo de item de conclusão. Os valores possíveis são o método, campo, propriedade, parâmetro, variável e reservados.  
  
-   `glyph`. Leitura/gravação quando usado na `items` coleção; caso contrário, somente leitura. Retorna uma cadeia de caracteres que representa um ícone que é exibido na lista de conclusão. Os valores possíveis para `glyph` use o seguinte formato: vs:*glyphType*, onde *glyphType* corresponde aos membros independente de linguagem no <xref:Microsoft.VisualStudio.Language.Intellisense.StandardGlyphGroup> enumeração. Por exemplo, `vs:GlyphGroupMethod` é um valor possível para `glyph`. Quando `glyph` não for definido, o `kind` propriedade determina o ícone padrão.  
  
-   `parentObject`. Somente leitura. Retorna o objeto pai.  
  
-   `value`. Somente leitura. Retorna um objeto que representa o valor do item de conclusão.  
  
-   `comments`. Somente leitura. Retorna uma cadeia de caracteres que contém os comentários que estão acima do campo ou variável.  
  
-   `scope`. Somente leitura. Retorna o escopo de item de conclusão. Os valores possíveis são globais, locais, parâmetros e membro.  
  
###  <a name="Items"></a> itens de propriedade  
 Obtém ou define a matriz de instrução itens de conclusão. Cada elemento na matriz é um [completionItem propriedade](#CompletionItem) objeto. O `items` propriedade está disponível para o `statementcompletion` objeto de evento.  
  
 Valor de retorno: matriz  
  
###  <a name="FunctionComments"></a> functionComments propriedade  
 Retorna os comentários para a função. Essa propriedade está disponível para o `signaturehelp` objeto de evento.  
  
 Valor de retorno: `comments` objeto  
  
 A seguir é os membros do `comments` objeto:  
  
-   `above`. Retorna os comentários acima da função.  
  
-   `inside`. Retorna os comentários dentro da função, normalmente no formato de VSDoc.  
  
-   `paramComments`. Retorna uma matriz que representa o comentário para cada parâmetro na função. Os membros da matriz incluem:  
  
    -   `name`. Retorna uma cadeia de caracteres que representa o nome do parâmetro.  
  
    -   `comment`. Retorna uma cadeia de caracteres que contém o comentário do parâmetro.  
  
###  <a name="FunctionHelp"></a> functionHelp propriedade  
 Retorna a Ajuda para a função. Essa propriedade está disponível para o `signaturehelp` objeto de evento.  
  
 Valor de retorno: `functionHelp` objeto  
  
 A seguir é os membros do `functionHelp` objeto:  
  
-   `functionName`. Leitura/gravação. Retorna uma cadeia de caracteres que contém o nome da função.  
  
-   `signatures`. Leitura/gravação. Obtém ou define a matriz de assinaturas de função. Cada elemento na matriz é um `signature` objeto. Alguns `signature` propriedades, tais como `locid`, correspondem aos comuns [comentários da documentação XML](../ide/xml-documentation-comments-javascript.md) atributos.  
  
     Os membros do `signature` objeto incluem:  
  
    -   `description`. Leitura/gravação. Retorna uma cadeia de caracteres que descreve a função.  
  
    -   `locid`. Leitura/gravação. Retorna um identificador de cadeia de caracteres que contém informações sobre a função de localização.  
  
    -   `helpKeyword`. Leitura/gravação. Retorna uma cadeia de caracteres que contém a palavra-chave ajuda.  
  
    -   `externalFile`. Leitura/gravação. Retorna uma cadeia de caracteres que representa o arquivo que contém a ID do membro.  
  
    -   `externalid`. Leitura/gravação. Retorna uma cadeia de caracteres que representa a ID de membro da função.  
  
    -   `params`. Leitura/gravação. Obtém ou define a matriz de parâmetros para a função. Cada elemento na matriz de parâmetros é um `parameter` que tem propriedades que correspondem aos seguintes atributos do objeto de [ \<param >](../ide/param-javascript.md) elemento:  
  
        -   `name`. Leitura/gravação. Retorna uma cadeia de caracteres que representa o nome do parâmetro.  
  
        -   `type`. Leitura/gravação. Retorna uma cadeia de caracteres que representa o tipo de parâmetro.  
  
        -   `elementType`. Leitura/gravação. Se o tipo for `Array`, retorna uma cadeia de caracteres que representa o tipo dos elementos na matriz.  
  
        -   `description`. Leitura/gravação. Retorna uma cadeia de caracteres que descreve o parâmetro.  
  
        -   `locid`. Leitura/gravação. Retorna um identificador de cadeia de caracteres que contém informações sobre a função de localização.  
  
        -   `optional`. Leitura/gravação. Retorna uma cadeia de caracteres que indica se o parâmetro é opcional. `true` indica que o parâmetro é opcional; `false` indica que ele não está.  
  
    -   `returnValue`. Leitura/gravação. Obtém ou define um objeto de valor de retorno com propriedades que correspondem aos seguintes atributos do [ \<retorna >](../ide/returns-javascript.md) elemento:  
  
        -   `type`. Leitura/gravação. Retorna uma cadeia de caracteres que representa o tipo de retorno.  
  
        -   `elementType`. Leitura/gravação. Se o tipo for `Array`, retorna uma cadeia de caracteres que representa o tipo dos elementos na matriz.  
  
        -   `description`. Leitura/gravação. Retorna uma cadeia de caracteres que descreve o valor de retorno.  
  
        -   `locid`. Leitura/gravação. Retorna um identificador de cadeia de caracteres que contém informações sobre a função de localização.  
  
        -   `helpKeyword`. Leitura/gravação. Retorna uma cadeia de caracteres que contém a palavra-chave ajuda.  
  
        -   `externalFile`. Leitura/gravação. Retorna uma cadeia de caracteres que representa o arquivo que contém a ID do membro.  
  
        -   `externalid`. Leitura/gravação. Retorna uma cadeia de caracteres que representa a ID de membro da função.  
  
###  <a name="ParentObject"></a> parentObject propriedade  
 Retorna o objeto pai de uma função de membro. Por exemplo, para `document.getElementByID`, `parentObject` retorna o `document` objeto. Essa propriedade está disponível para o `signaturehelp` objeto de evento.  
  
 Valor de retorno: objeto  
  
###  <a name="Target"></a> Propriedade de destino  
 Retorna um objeto que representa o item à esquerda do caractere disparador, que é um ponto (.). Para funções, `target` retorna a função para a qual as informações do parâmetro é solicitada. Essa propriedade está disponível para o `statementcompletion` e `signaturehelp` objetos de evento.  
  
 Valor de retorno: objeto  
  
###  <a name="TargetName"></a> targetName propriedade  
 Retorna uma cadeia de caracteres que representa o destino. Por exemplo, para "this.", `targetName` retorna "this". Para "B" (quando o cursor depois de "B"), `targetName` retorna "B". Essa propriedade está disponível para o `statementcompletion` objeto de evento.  
  
 Valor de retorno: cadeia de caracteres  
  
###  <a name="SymbolHelp"></a> symbolHelp propriedade  
 Retorna o item de conclusão para a qual uma caixa pop-up de informações rápidas é solicitada. Essa propriedade está disponível para o `statementcompletionhint` objeto de evento.  
  
 Valor de retorno: `symbolHelp` objeto.  
  
 Algumas propriedades do `symbolHelp` objeto, como `locid`, correspondem aos comuns [comentários da documentação XML](../ide/xml-documentation-comments-javascript.md) atributos.  
  
 A seguir é os membros do `symbolHelp` objeto:  
  
-   `name`. Leitura/gravação. Retorna uma cadeia de caracteres que contém o nome do identificador.  
  
-   `symbolType`. Leitura/gravação. Retorna uma cadeia de caracteres que representa o tipo de símbolo. Os valores possíveis incluem desconhecido, booleano, número, cadeia de caracteres, objeto, função, matriz, data e Regex.  
  
-   `symbolDisplayType`. Leitura/gravação. Retorna uma cadeia de caracteres que contém o nome de tipo para exibir. Se `symbolDisplayType` não for definido, `symbolType` é usado.  
  
-   `elementType`. Leitura/gravação. Se o `symbolType` é `Array`, retorna uma cadeia de caracteres que representa o tipo dos elementos na matriz.  
  
-   `scope`. Leitura/gravação. Retorna uma cadeia de caracteres que representa o escopo do símbolo. Os valores possíveis incluem um parâmetro global e local e o membro.  
  
-   `description`. Leitura/gravação. Retorna uma cadeia de caracteres que contém uma descrição do símbolo.  
  
-   `locid`. Leitura/gravação. Retorna um identificador de cadeia de caracteres que contém informações sobre o símbolo de localização.  
  
-   `helpKeyword`. Leitura/gravação. Retorna uma cadeia de caracteres que contém a palavra-chave ajuda.  
  
-   `externalFile`. Leitura/gravação. Retorna uma cadeia de caracteres que representa o arquivo que contém a ID do membro.  
  
-   `externalid`. Leitura/gravação. Retorna uma cadeia de caracteres que representa a ID de membro do símbolo.  
  
-   `functionHelp`. Leitura/gravação. Retorna um [functionHelp propriedade](#FunctionHelp), que podem conter informações quando o `symbolType` é a função.  
  
###  <a name="Scope"></a> definir o escopo de propriedade  
 Retorna o escopo de conclusão do evento. Os valores possíveis para a conclusão do escopo são global e membros. Essa propriedade está disponível para o `statementcompletion` objeto de evento.  
  
 Valor de retorno: cadeia de caracteres  
  
## <a name="debugging-intellisense-extensions"></a>Depurando extensões do IntelliSense  
 Você não pode depurar extensões, mas você pode usar o [intellisense objeto](#intellisenseObject) função para enviar informações para a janela de saída do Visual Studio. Para obter um exemplo que mostra como usar essa função, consulte [enviando mensagens para a janela de saída](#Logging) mais adiante neste tópico. Para `logMessage` para trabalhar, o manipulador de pelo menos um evento deve ser registrado em uma extensão.  
  
##  <a name="CodeExamples"></a> Exemplos de código  
 Esta seção inclui exemplos de código que mostram como usar as APIs de extensibilidade do IntelliSense. Também há outras maneiras de usar essas APIs. Para obter exemplos adicionais, consulte os seguintes arquivos na \\ \\ *caminho de instalação do Visual Studio*\JavaScript\References pasta. Eles estão trabalhando exemplos usados pelo serviço de linguagem JavaScript.  
  
-   underscoreFilter.js. Esse código oculta membros privados do IntelliSense. Ele inclui manipuladores de eventos para o `statementcompletion` eventos.  
  
-   showPlainComments.js. Esse código fornece suporte ao IntelliSense para comentários de padrão. Ele inclui manipuladores de eventos para o `signaturehelp` e `statementcompletionhint` eventos.  
  
###  <a name="Annotations"></a> Adicionando anotações do IntelliSense  
 O procedimento a seguir mostra como fornecer suporte de documentação do IntelliSense para uma biblioteca de terceiros, sem modificar a biblioteca diretamente. Para fazer isso, você pode usar `intellisense.annotate` em uma extensão.  
  
 Para esse exemplo funcione, é necessário os seguintes arquivos JavaScript em seu projeto:  
  
-   demoLib.js, que é um arquivo de projeto que representa uma biblioteca de terceiros.  
  
-   demoLib.intellisense.js, que é a extensão do IntelliSense. Esse arquivo não precisa ser incluído no projeto, mas ele precisa estar na mesma pasta que exampleLib.js.  
  
-   appCode.js, que é um arquivo de projeto que representa o código do aplicativo.  
  
##### <a name="to-add-an-intellisense-annotation"></a>Para adicionar uma anotação do IntelliSense  
  
1.  Adicione o seguinte código ao demoLib.js.  
  
    ```javascript  
    function someFunc(a) { };  
    var rectangle;  
  
    ```  
  
2.  Adicione o seguinte código ao demoLib.intellisense.js.  
  
    ```javascript  
    intellisense.annotate(someFunc, function (a) {  
        /// <signature>  
        /// <summary>Description of someFunc</summary>  
        /// <param name="a">Param a</param>  
        /// </signature>  
    });  
  
    intellisense.annotate(window, {  
        // This is a comment on a global variable named rectangle.  
        rectangle: undefined  
    });  
    ```  
  
3.  Adicione a seguinte diretiva de referência como a primeira linha no appCode.js. O caminho usado aqui indica que os arquivos JavaScript estão na mesma pasta.  
  
    ```javascript  
    /// <reference path="demoLib.js" />  
  
    ```  
  
4.  Na appCode.js, digite o código a seguir. Você verá os comentários da documentação XML na extensão exibidos como informações de parâmetro do IntelliSense.  
  
     ![Exemplo mostrando o uso de intellisense.annotate](../ide/media/js-intellisense-annotate-paraminfo.png "js_intellisense_annotate_paraminfo")  
  
5.  Na appCode.js, digite o código a seguir. Enquanto você digita, você verá os comentários padrão na extensão exibidos como informações rápidas do IntelliSense.  
  
     ![Exemplo mostrando o uso de intellisense.annotate](../ide/media/js-intellisense-annotations.png "js_intellisense_annotations")  
  
###  <a name="Logging"></a> Enviando mensagens para a janela de saída  
 O procedimento a seguir mostra como enviar mensagens para a janela de saída. Você pode enviar mensagens para ajudar a depurar extensões do IntelliSense.  
  
 Para esse exemplo funcione, é necessário os seguintes arquivos JavaScript em seu projeto:  
  
-   exampleLib.js, que é um arquivo de projeto que representa uma biblioteca de terceiros.  
  
-   exampleLib.intellisense.js, que é a extensão do IntelliSense. Esse arquivo não precisa ser incluído no projeto, mas ele precisa estar na mesma pasta que exampleLib.js.  
  
-   appCode.js, que é um arquivo de projeto que representa o código do aplicativo.  
  
##### <a name="to-send-a-message-to-the-output-window"></a>Para enviar uma mensagem na janela Saída  
  
1.  Adicione o seguinte código ao exampleLib.js.  
  
    ```javascript  
    var someVar = {  
        a: 1,  
        b: 'hello'  
    };  
    ```  
  
2.  Adicione o seguinte código ao exampleLib.intellisense.js.  
  
    ```javascript  
    intellisense.addEventListener('statementcompletion', function (e) {  
        // Prints out statement completion info: Either (1) the member   
        // list, if the trigger character was typed, or (2) the   
        // statement completion identifiers.  
        // e.target represents the object left of the trigger character.  
        intellisense.logMessage(  
            e.target ? 'member list requested, target: ' + e.targetName : 'statement completion for current scope requested');  
  
        // Prints out all statement completion items.  
        e.items.forEach(function (item) {  
            intellisense.logMessage('[completion item] ' + item.name + ', kind:' + item.kind + ', scope:' + item.scope + ', value:' + item.value);  
        });  
    });  
    ```  
  
3.  Adicione a seguinte diretiva de referência como a primeira linha no appCode.js. O caminho usado aqui indica que os arquivos JavaScript estão na mesma pasta.  
  
    ```javascript  
    /// <reference path="exampleLib.js" />  
  
    ```  
  
4.  Na janela de saída, escolha **serviço de linguagem JavaScript** na **Mostrar saída de** lista. (Para exibir a janela de saída, selecione **saída** no menu Exibir.)  
  
5.  Na appCode.js, digite o código a seguir. Enquanto você digita, a janela saída mostra mensagens do serviço de linguagem. A primeira mensagem na janela de saída indica que o preenchimento de declaração para o escopo atual foi solicitado.  
  
    ```javascript  
    some  
    ```  
  
     A seguir está uma exibição parcial da saída, você verá.  
  
    ```scr  
    03:16:14.3113: statement completion for current scope requested  
    03:16:14.3113: [completion item] break, kind:reserved, scope:undefined, value:undefined  
    03:16:14.3113: [completion item] case, kind:reserved, scope:undefined, value:undefined  
    03:16:14.3113: [completion item] catch, kind:reserved, scope:undefined, value:undefined  
  
    …  
    ```  
  
6.  Escolha o **Limpar tudo** botão na janela de saída.  
  
7.  Digite o código a seguir. A primeira mensagem na janela de saída indica que uma lista de membros foi solicitada.  
  
    ```javascript  
    someVar.  
    ```  
  
     A seguir está uma exibição parcial da saída, você verá:  
  
    ```scr  
    03:17:43.4032: member list requested, target: someVar  
    03:17:43.4032: [completion item] a, kind:field, scope:member, value:1  
    03:17:43.4032: [completion item] b, kind:field, scope:member, value:hello  
    03:17:43.4032: [completion item] constructor, kind:method, scope:member, value:  
  
    …  
    ```  
  
###  <a name="Icons"></a> Alterar os ícones do IntelliSense  
 O procedimento a seguir mostra como alterar os ícones exibidos pelo IntelliSense, por padrão. Isso pode ser útil quando você fornece informações sobre conceitos de biblioteca específico, como namespaces, classes, interfaces e enumerações do IntelliSense.  
  
 Para obter valores de ícone disponíveis, consulte <xref:Microsoft.VisualStudio.Language.Intellisense.StandardGlyphGroup>.  
  
 Para esse exemplo funcione, é necessário os seguintes arquivos JavaScript em seu projeto:  
  
-   exampleLib.js, que é um projeto de arquivos dessa biblioteca represens por terceiros.  
  
-   exampleLib.intellisense.js, que é a extensão do IntelliSense. Esse arquivo não precisa ser incluído no projeto, mas ele precisa estar na mesma pasta que exampleLib.js.  
  
-   appCode.js, que é um arquivo de projeto que representa o código do aplicativo.  
  
##### <a name="to-change-the-icons"></a>Para alterar os ícones  
  
1.  Adicione o seguinte código ao exampleLib.js.  
  
    ```javascript  
    function Namespace(name) {  
        this._isNamespace = true;  
        window[name] = this;  
    };  
  
    function Enum(values) {  
        var e = Object.create(values);  
        e._isEnum = true;  
        return e;  
    };  
  
    var SomeNamespace = new Namespace('SomeNamespace');  
    // A constructor function is considered a class.  
    SomeNamespace.SomeClass1 = function () { }  
    SomeNamespace.Enum1 = new Enum({ VALUE1: 0, VALUE2: 1 });  
    ```  
  
2.  Adicione o seguinte código ao exampleLib.intellisense.js.  
  
    ```javascript  
    intellisense.addEventListener('statementcompletion', function (e) {  
        e.items.forEach(function (item) {  
            // Detect a namespace by using the _isNamespace flag.  
            if (item.value && item.value._isNamespace) {  
                item.glyph = 'vs:GlyphGroupNamespace';  
                }  
  
            if (item.parentObject && item.parentObject._isNamespace) {  
                // The item is a member of a namespace.   
  
                // All constructor functions that are part of a namespace   
                // are considered classes.   
                // A constructor function starts with  
                // an uppercase letter by convention.    
                if (typeof item.value == 'function' && (item.name[0].toUpperCase()   
                    == item.name[0])) {  
                    item.glyph = 'vs:GlyphGroupClass';  
                }  
  
                // Detect an enumeration by using the _isEnum flag.  
                if (item.value && item.value._isEnum) {  
                    item.glyph = 'vs:GlyphGroupEnum';  
                }  
            }  
        });  
    });  
  
    intellisense.addEventListener('statementcompletionhint', function (e) {  
        if (e.completionItem.value) {  
            if (e.completionItem.value._isNamespace) {  
                e.symbolHelp.symbolDisplayType = 'Namespace';  
            }  
            if (e.completionItem.value._isEnum) {  
                e.symbolHelp.symbolDisplayType = 'Enum';  
            }  
        }  
    });  
    ```  
  
3.  Adicione a seguinte diretiva de referência como a primeira linha no appCode.js. O caminho usado aqui indica que os arquivos JavaScript estão na mesma pasta.  
  
    ```javascript  
    /// <reference path="exampleLib.js" />  
  
    ```  
  
4.  Na appCode.js, digite o código a seguir. Enquanto você digita, você verá que o ícone para o namespace foi alterado para "{}", conforme é usado em c#.  
  
     ![Exemplo mostrando o uso da propriedade de glifo](../ide/media/js-intellisense-glyph-namespace.png "js_intellisense_glyph_namespace")  
  
5.  Na appCode.js, digite o código a seguir. Enquanto você digita, você verá um novo ícone de enumeração para o membro Enum1 e um novo ícone de classe para o membro SomeClass1.  
  
     ![Exemplo mostrando o uso da propriedade glifo](../ide/media/js-intellisense-glyph-class-enum.png "js_intellisense_glyph_class_enum")  
  
###  <a name="Overriding"></a> Evitar efeitos de tempo de execução nos resultados do IntelliSense  
 O serviço de linguagem JavaScript executa o código para fornecer dinamicamente as informações de IntelliSense. Como resultado, o comportamento de tempo de execução, ocasionalmente, pode interferir com os resultados desejados. O procedimento a seguir mostra como substituir os resultados do IntelliSense ao comportamento de tempo de execução resulta no IntelliSense incorreto.  
  
 Para esse exemplo funcione, é necessário os seguintes arquivos JavaScript em seu projeto:  
  
-   exampleLib.js, que é um arquivo de projeto que representa uma biblioteca de terceiros.  
  
-   exampleLib.intellisense.js, que é a extensão do IntelliSense. Esse arquivo não precisa ser incluído no projeto, mas ele precisa estar na mesma pasta que exampleLib.js.  
  
-   appCode.js, que é um arquivo de projeto que representa o código do aplicativo.  
  
##### <a name="to-avoid-run-time-effects-on-intellisense-results"></a>Para evitar efeitos de tempo de execução nos resultados do IntelliSense  
  
1.  Adicione o seguinte código ao exampleLib.js.  
  
    ```javascript  
    function after(count, func) {  
        return function () {  
            if (--times < 1) {  
                return func.apply(this, arguments);  
            }  
        };  
    };  
    ```  
  
     No código anterior, a função encapsulada ignora chamadas inicias, com base no valor de `count`e não retorna resultados.  
  
2.  Adicione a seguinte diretiva de referência como a primeira linha no appCode.js. O caminho usado aqui indica que os arquivos JavaScript estão na mesma pasta.  
  
    ```javascript  
    /// <reference path="exampleLib.js" />  
  
    ```  
  
3.  Na appCode.js, digite o código a seguir. A lista de identificador é exibida em vez de IntelliSense porque a função encapsulada nunca é chamada, o que significa que o `throttled` função não retornará nenhum resultado.  
  
     ![Exemplo de resultados do intellisense de substituição](../ide/media/js-intellisense-override.png "js_intellisense_override")  
  
4.  Adicione o seguinte código ao exampleLib.intellisense.js. Isso alterará o comportamento de tempo de design para que o IntelliSense é mostrado para a função encapsulada, conforme o esperado.  
  
    ```javascript  
    window.after = function (count, func) {  
        // Just return func.   
        return func;  
    };  
    ```  
  
5.  No appCode.js, teste os resultados digitando o mesmo código que você digitou anteriormente. Neste momento, o IntelliSense fornece as informações desejadas.  
  
     ![Exemplo de resultados do IntelliSense de substituição](../ide/media/js-intellisense-override-fixed.png "js_intellisense_override_fixed")  
  
## <a name="see-also"></a>Consulte também  
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)   
 [Preenchimento de declaração para identificadores](../ide/statement-completion-for-identifiers.md)



