---
title: Parâmetros de modelo de projeto e de item Visual do Studio
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Visual Studio templates, parameters
- template parameters [Visual Studio]
- project templates, parameters
- item templates, parameters
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 4c76eaf68f63b4f3b8a5713d0b206b395ee7c9f1
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39178628"
---
# <a name="template-parameters"></a>Parâmetros de modelo

Você poderá substituir os valores do modelo quando for criada uma instância dele. Para configurar essa funcionalidade, use *parâmetros de modelo*. Os parâmetros de modelo podem ser usados para substituir valores, como nomes de classes e namespaces, no modelo. O assistente de modelo que é executado em segundo plano quando um usuário adiciona um novo item ou projeto substitui esses parâmetros.

## <a name="declaring-and-enabling-template-parameters"></a>Declarando e habilitando parâmetros de modelo

Parâmetros de modelo são declarados no formato $*parâmetro*$. Por exemplo:

- $safeprojectname$

- $guid1$

- $guid5$

### <a name="to-enable-parameter-substitution-in-templates"></a>Para habilitar a substituição de parâmetro nos modelos

1. No arquivo *.vstemplate* do modelo, localize o elemento `ProjectItem` que corresponde ao item para o qual você deseja habilitar a substituição de parâmetro.

1. Defina o atributo `ReplaceParameters` do elemento `ProjectItem` como `true`.

1. No arquivo de código do item de projeto, inclua parâmetros conforme apropriado. Por exemplo, o parâmetro a seguir especifica que o nome do projeto seguro é usado para o namespace em um arquivo:

    ```csharp
    namespace $safeprojectname$
    ```

## <a name="reserved-template-parameters"></a>Parâmetros de modelo reservados

A tabela a seguir lista os parâmetros de modelo reservados que podem ser usados por qualquer modelo.

|Parâmetro|Descrição|
|---------------|-----------------|
|clrversion|Versão atual do CLR (Common Language Runtime).|
|guid[1-10]|Um GUID usado para substituir o GUID do projeto em um arquivo de projeto. Você pode especificar até 10 GUIDs exclusivos (por exemplo, `guid1`).|
|itemname|O nome fornecido pelo usuário na caixa de diálogo **Adicionar Novo Item**.|
|machinename|O nome do computador atual (por exemplo, Computer01).|
|projectname|O nome fornecido pelo usuário na caixa de diálogo **Novo Projeto**.|
|registeredorganization|O valor da chave do Registro de HKLM\Software\Microsoft\Windows NT\CurrentVersion\RegisteredOrganization.|
|rootnamespace|O namespace raiz do projeto atual. Esse parâmetro se aplica somente a modelos de item.|
|safeitemname|O nome fornecido pelo usuário na caixa de diálogo **Adicionar Novo Item**, com todos os caracteres desprotegidos e espaços removidos.|
|safeprojectname|O nome fornecido pelo usuário na caixa de diálogo **Novo Projeto**, com todos os caracteres desprotegidos e espaços removidos.|
|hora|A hora atual no formato DD/MM/AAAA 00:00:00.|
|SpecificSolutionName|O nome da solução. Quando "criar diretório da solução" estiver marcado, `SpecificSolutionName` terá o nome da solução. Quando "criar diretório da solução" não estiver marcado, `SpecificSolutionName` estará em branco.|
|userdomain|O domínio do usuário atual.|
|username|O nome de usuário atual.|
|webnamespace|O nome do site atual. Este parâmetro é usado no modelo de formulário da Web para garantir nomes de classe exclusivos. Se o site estiver no diretório raiz do servidor Web, esse parâmetro de modelo será resolvido para o diretório raiz do servidor Web.|
|ano|O ano atual no formato AAAA.|

> [!NOTE]
> Parâmetros de modelo diferenciam maiúsculas de minúsculas.

## <a name="custom-template-parameters"></a>Parâmetros de modelo personalizados

Você pode especificar seus próprios valores e parâmetros de modelo, além dos parâmetros de modelo reservados padrão, que são usados durante a substituição de parâmetros. Para obter mais informações, consulte [Elemento CustomParameters (modelos do Visual Studio)](../extensibility/customparameters-element-visual-studio-templates.md).

## <a name="example-use-the-project-name-for-a-file-name"></a>Exemplo: usar o nome do projeto para um nome de arquivo

Você pode especificar nomes de arquivo variáveis para itens de projeto usando um parâmetro no atributo `TargetFileName`.

O exemplo a seguir especifica que o nome de um arquivo executável usa o nome do projeto, especificado por `$projectname$`.

```xml
<TemplateContent>
    <ProjectItem
        ReplaceParameters="true"
        TargetFileName="$projectname$.exe">
            File1.exe
    </ProjectItem>
      ...
</TemplateContent>
```

## <a name="example-use-the-safe-project-name-for-the-namespace-name"></a>Exemplo: usar o nome seguro do projeto para o nome do namespace

Para usar o nome seguro do projeto para o namespace em um arquivo de classe C#, use a seguinte sintaxe:

```csharp
namespace $safeprojectname$
{
    public class Class1
    {
        public Class1()
        { }
    }
}
```

No arquivo *.vstemplate* do modelo de projeto, inclua o atributo `ReplaceParameters="true"` quando fizer referência ao arquivo:

```xml
<TemplateContent>
    <ProjectItem ReplaceParameters="true">
        Class1.cs
    </ProjectItem>
    ...
</TemplateContent>
```

## <a name="see-also"></a>Consulte também

- [Personalizar modelos](../ide/customizing-project-and-item-templates.md)
- [Como criar modelos de projeto](../ide/how-to-create-project-templates.md)
- [Referência de esquema de modelo](../extensibility/visual-studio-template-schema-reference.md)
