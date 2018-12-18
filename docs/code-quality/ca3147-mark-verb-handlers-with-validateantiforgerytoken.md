---
title: 'CA3147: marcar manipuladores de verbo com ValidateAntiForgeryToken'
ms.date: 08/08/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
author: dotpaul
ms.author: paulming
manager: douge
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: da15a441a10f3ad3f3f84ee0cc76eeed8e4127e4
ms.sourcegitcommit: 2597236a481afbaf1ad4915743898ee1aee49760
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/10/2018
ms.locfileid: "42623645"
---
# <a name="ca3147-mark-verb-handlers-with-validateantiforgerytoken"></a>CA3147: marcar manipuladores de verbo com ValidateAntiForgeryToken

|||
|-|-|
|NomeDoTipo|MarkVerbHandlersWithValidateAntiForgeryToken|
|CheckId|CA3147|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Um método de ação do controlador MVC do ASP.NET não está marcado com [ValidateAntiForgeryTokenAttribute](/previous-versions/aspnet/web-frameworks/dd492108(v=vs.118)), ou um atributo que especifica o verbo HTTP, como [HttpGetAttribute](/previous-versions/aspnet/web-frameworks/ee470993(v%3dvs.118)) ou [ AcceptVerbsAttribute](/previous-versions/aspnet/web-frameworks/dd470553%28v%3dvs.118%29).

## <a name="rule-description"></a>Descrição da regra

Durante a criação de um controlador ASP.NET MVC, lembre-se de ataques de falsificação de solicitação entre sites. Um ataque de falsificação de solicitação entre sites pode enviar solicitações mal-intencionadas de um usuário autenticado ao seu controlador ASP.NET MVC. Para obter mais informações, consulte [prevenção de XSRF/CSRF no ASP.NET MVC e páginas da web](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages).

Esta regra verifica se esse controlador ASP.NET MVC métodos de ação ambos:

- Ter o [ValidateAntiforgeryTokenAttribute](/previous-versions/aspnet/web-frameworks/dd492108%28v%3dvs.118%29) e especifique verbos HTTP permitidos, não incluindo HTTP GET.

- Especifique o HTTP GET como um verbo permitido.

## <a name="how-to-fix-violations"></a>Como corrigir violações

- Para ações do controlador ASP.NET MVC que manipulam solicitações HTTP GET e não têm efeitos colaterais potencialmente nocivos, adicione uma [HttpGetAttribute](/previous-versions/aspnet/web-frameworks/ee470993%28v%3dvs.118%29) para o método.

   Se você tiver um ASP.NET MVC solicitações de ação do controlador que manipula a HTTP GET e tem potencialmente prejudiciais efeitos colaterais, como a modificação de dados confidenciais, seu aplicativo é vulnerável a ataques de falsificação de solicitação entre sites.  Você precisará recriar seu aplicativo para que somente as solicitações HTTP POST, PUT ou DELETE executam operações confidenciais.

- Para ações do controlador ASP.NET MVC que lidar com HTTP POST, PUT ou as solicitações de exclusão, adicione [ValidateAntiForgeryTokenAttribute](/previous-versions/aspnet/web-frameworks/dd492108(v=vs.118)) e especificando os verbos HTTP permitidos de atributos ([AcceptVerbsAttribute](/previous-versions/aspnet/web-frameworks/dd470553%28v%3dvs.118%29) [HttpPostAttribute](/previous-versions/aspnet/web-frameworks/ee264023%28v%3dvs.118%29), [HttpPutAttribute](/previous-versions/aspnet/web-frameworks/ee470909%28v%3dvs.118%29), ou [HttpDeleteAttribute](/previous-versions/aspnet/web-frameworks/ee470917%28v%3dvs.118%29)). Além disso, você precisará chamar o [HtmlHelper.AntiForgeryToken()](/previous-versions/aspnet/web-frameworks/dd504812%28v%3dvs.118%29) método do seu modo de exibição do MVC ou página da web Razor. Por exemplo, consulte [examinando os métodos edit e Editar modo de exibição](/aspnet/mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view).

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra se:

- A ação do controlador MVC do ASP.NET não tem prejudiciais efeitos colaterais.

- O aplicativo valida o token antifalsificação de maneira diferente.

## <a name="validateantiforgerytoken-attribute-example"></a>Exemplo de atributo ValidateAntiForgeryToken

### <a name="violation"></a>Violação

```csharp
namespace TestNamespace
{
    using System.Web.Mvc;

    public class TestController : Controller
    {
        public ActionResult TransferMoney(string toAccount, string amount)
        {
            // You don't want an attacker to specify to who and how much money to transfer.

            return null;
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System;
using System.Xml;

namespace TestNamespace
{
    using System.Web.Mvc;

    public class TestController : Controller
    {
        [HttpPost]
        [ValidateAntiForgeryToken]
        public ActionResult TransferMoney(string toAccount, string amount)
        {
            return null;
        }
    }
}
```

## <a name="httpget-attribute-example"></a>Exemplo de atributo HttpGet

### <a name="violation"></a>Violação

```csharp
namespace TestNamespace
{
    using System.Web.Mvc;

    public class TestController : Controller
    {
        public ActionResult Help(int topicId)
        {
            // This Help method is an example of a read-only operation with no harmful side effects.
            return null;
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
namespace TestNamespace
{
    using System.Web.Mvc;

    public class TestController : Controller
    {
        [HttpGet]
        public ActionResult Help(int topicId)
        {
            return null;
        }
    }
}
```
