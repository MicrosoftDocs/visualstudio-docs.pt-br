---
title: Exibir informações personalizadas usando DebuggerDisplay | Microsoft Docs
ms.date: 01/09/2019
ms.topic: how-to
helpviewer_keywords:
- attributes, debugger
- DebuggerDisplay attribute
- DebuggerDisplayAttribute class
ms.assetid: f4eb7c76-af4e-493b-9ab6-9cb05949d9b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2387c5e9a920f0811a65ca400d8da48aa81dccd3
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418776"
---
# <a name="tell-the-debugger-what-to-show-using-the-debuggerdisplay-attribute-c-visual-basic-f-ccli"></a>Diga ao depurador o que mostrar usando o atributo DebuggerDisplay (C#, Visual Basic, F #, C++/CLI)

O <xref:System.Diagnostics.DebuggerDisplayAttribute> controla como um objeto, propriedade ou campo é exibido nas janelas da variável do depurador. Esse atributo pode ser aplicado a tipos, delegados, propriedades, campos e assemblies. Se aplicado a um tipo base, o atributo também se aplicará a uma subclasse.

O atributo `DebuggerDisplay` tem um único argumento, que é uma cadeia de caracteres a ser exibida na coluna de valor para instâncias do tipo. Essa cadeia de caracteres pode conter chaves (`{` e `}`). O texto dentro de um par de chaves é avaliado como um campo, propriedade ou método.

Se uma classe tiver um `ToString()` método substituído, o depurador usará o método substituído em vez do padrão `{<typeName>}` . Portanto, se você tiver substituído o `ToString()` método, o depurador usará o método substituído em vez do padrão `{<typeName>}` , e você não precisará usar `DebuggerDisplay` . Se você usar ambos, o `DebuggerDisplay` atributo terá precedência sobre o `ToString()` método substituído. O `DebuggerDisplay` atributo também tem precedência sobre o `ToString()` método substituído em uma subclasse.

Se o depurador avaliar essa chamada implícita `ToString()` depende de uma configuração de usuário na caixa de diálogo **ferramentas/opções/depuração** .

> [!IMPORTANT]
> Se a caixa de seleção **Mostrar estrutura bruta de objetos em variáveis do Windows** estiver marcada na caixa de diálogo **ferramentas/opções/depuração** , o `DebuggerDisplay` atributo será ignorado.

> [!NOTE]
> Para código nativo, esse atributo tem suporte apenas no código C++/CLI.

A tabela a seguir mostra alguns usos possíveis do atributo `DebuggerDisplay` e saídas de exemplo.

|Atributo|Saída aparecendo na coluna Valor|
|---------------| - |
|`[DebuggerDisplay("x = {x} y = {y}")]`<br /><br /> Usado em um tipo com campos `x` e `y`.|`x = 5 y = 18`|
|`[DebuggerDisplay("String value is {getString()}")]`A sintaxe de parâmetro pode variar entre linguagens. Em virtude disso, use com cuidado.|`String value is [5, 6, 6]`|

`DebuggerDisplay` também pode aceitar parâmetros nomeados.

|Parâmetros|Finalidade|
|----------------|-------------|
|`Name`, `Type`|Esses parâmetros afetam as colunas **Nome** e **Tipo** das janelas variáveis. (Podem ser definidos como cadeias de caracteres usando a mesma sintaxe que o construtor.) Usar esses parâmetros demais ou usá-los incorretamente pode causar uma saída confusa.|
|`Target`, `TargetTypeName`|Especifica o tipo de destino quando o atributo é usado no nível de assembly.|

O arquivo autoexp.cs usa o atributo DebuggerDisplay no nível do assembly. O arquivo autoexp.cs determina as expansões padrão que o Visual Studio usa para objetos .NET. Você pode examinar o arquivo autoexp.cs para obter exemplos de como usar o atributo DebuggerDisplay ou pode modificar e compilar o arquivo autoexp.cs para alterar as expansões padrão. Faça backup do arquivo autoexp.cs antes de modificá-lo.

Para criar o autoexp.cs, abra um Prompt de Comando do Desenvolvedor para VS2015 e execute os comandos a seguir

```cmd
cd <directory containing autoexp.cs>
csc /t:library autoexp.cs
```

As alterações a autoexp.dll serão selecionadas na próxima sessão de depuração.

## <a name="using-expressions-in-debuggerdisplay"></a>Usando expressões em DebuggerDisplay
Embora você possa usar uma expressão geral entre as chaves em um atributo DebuggerDisplay, esta prática não é recomendada.

Uma expressão geral em DebuggerDisplay tem acesso implícito ao ponteiro `this` somente para a instância atual do tipo de destino. A expressão não tem acesso a alias, locais ou ponteiros. Se a expressão fizer referência a propriedades, os atributos nessas propriedades não serão processados. Por exemplo, o código C# `[DebuggerDisplay("Object {count - 2}")]` exibiria `Object 6` se o campo `count` fosse 8.

Usar expressões em DebuggerDisplay pode resultar nos seguintes problemas:

- Avaliar expressões é a operação mais cara no depurador e a expressão é avaliada toda vez que é exibida. Isso pode causar problemas de desempenho ao depurar o código. Por exemplo, uma expressão complexa que é usada para exibir os valores em uma coleção ou lista poderá ser muito lenta quando o número de elementos for grande.

- As expressões são avaliadas pelo avaliador de expressão da linguagem do quadro de pilhas atual e não pelo avaliador da linguagem na qual a expressão foi gravada. Isso pode causar resultados imprevisíveis quando as linguagens são diferentes.

- Avaliar uma expressão pode alterar o estado do aplicativo. Por exemplo, uma expressão que define o valor de uma propriedade transforma o valor da propriedade no código de execução.

  Uma maneira de reduzir os possíveis problemas de avaliação da expressão é criando uma propriedade privada que executa a operação e retorna uma cadeia de caracteres. O atributo DebuggerDisplay pode em seguida exibir o valor dessa propriedade privada. O exemplo a seguir implementa esse padrão:

```csharp
[DebuggerDisplay("{DebuggerDisplay,nq}")]
public sealed class MyClass
{
    public int count { get; set; }
    public bool flag { get; set; }
    private string DebuggerDisplay
    {
        get
        {
            return string.Format("Object {0}", count - 2);
        }
    }
}
```

O sufixo ", NQ" informa o avaliador de expressão para remover as aspas ao exibir o valor final (NQ = sem aspas).

## <a name="example"></a>Exemplo
O exemplo de código a seguir mostra como usar `DebuggerDisplay` junto com `DebuggerBrowseable` e `DebuggerTypeProxy`. Quando exibido em uma janela variáveis de depurador, como, por exemplo, a janela **Inspeção**, ele produz uma expansão semelhante ao seguinte:

|**Nome**|**Valor**|**Tipo**|
|--------------|---------------|--------------|
|Chave|"three"|object {string}|
|Valor|3|object {int}|

```csharp
[DebuggerDisplay("{value}", Name = "{key}")]
internal class KeyValuePairs
{
    private IDictionary dictionary;
    private object key;
    private object value;
    public KeyValuePairs(IDictionary dictionary, object key, object value)
    {
        this.value = value;
        this.key = key;
        this.dictionary = dictionary;
    }

    public object Key
    {
        get { return key; }
        set
        {
            object tempValue = dictionary[key];
            dictionary.Remove(key);
            key = value;
            dictionary.Add(key, tempValue);
        }
    }

    public object Value
    {
        get { return this.value; }
        set
        {
            this.value = value;
            dictionary[key] = this.value;
        }
    }
}

[DebuggerDisplay("{DebuggerDisplay,nq}")]
[DebuggerTypeProxy(typeof(HashtableDebugView))]
class MyHashtable
{
    public Hashtable hashtable;

    public MyHashtable()
    {
        hashtable = new Hashtable();
    }

    private string DebuggerDisplay { get { return "Count = " + hashtable.Count; } }

    private class HashtableDebugView
    {
        private MyHashtable myhashtable;
        public HashtableDebugView(MyHashtable myhashtable)
        {
            this.myhashtable = myhashtable;
        }

        [DebuggerBrowsable(DebuggerBrowsableState.RootHidden)]
        public KeyValuePairs[] Keys
        {
            get
            {
                KeyValuePairs[] keys = new KeyValuePairs[myhashtable.hashtable.Count];

                int i = 0;
                foreach (object key in myhashtable.hashtable.Keys)
                {
                    keys[i] = new KeyValuePairs(myhashtable.hashtable, key, myhashtable.hashtable[key]);
                    i++;
                }
                return keys;
            }
        }
    }
}
```

## <a name="see-also"></a>Veja também

- [Usando o atributo DebuggerTypeProxy](../debugger/using-debuggertypeproxy-attribute.md)
- [Criar exibições personalizadas de objetos gerenciados](../debugger/create-custom-views-of-managed-objects.md)
- [Especificadores de formato em C #](../debugger/format-specifiers-in-csharp.md)
- [Melhorando a depuração com os atributos de exibição do depurador](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)
