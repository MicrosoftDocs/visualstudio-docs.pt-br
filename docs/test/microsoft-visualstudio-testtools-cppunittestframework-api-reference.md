---
title: Referência da API Microsoft.VisualStudio.TestTools.CppUnitTestFramework
ms.date: 11/04/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: reference
ms.author: mblome
manager: douge
ms.workload:
- multiple
author: mikeblome
ms.openlocfilehash: b2225ec5db308b290e932cb9d29d1c50e32d4608
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49820259"
---
# <a name="microsoftvisualstudiotesttoolscppunittestframework-api-reference"></a>Referência da API Microsoft.VisualStudio.TestTools.CppUnitTestFramework

Este tópico lista os membros públicos do namespace `Microsoft::VisualStudio::CppUnitTestFramework`. Use essas APIs para gravar testes de unidade do C++ com base em Microsoft Native Unit Test Framework. Há um [Exemplo de Uso](#example) no final do tópico.

 Os arquivos de cabeçalho estão localizados na pasta _VisualStudio2012[x86]InstallFolder_**\VC\UnitTest\include**.

 Os arquivos lib estão localizados na pasta _VisualStudio2012[x86]InstallFolder_**\VC\UnitTest\lib**.

Caminhos de cabeçalho e lib são configurados automaticamente em um projeto de teste nativo.

##  <a name="In_this_topic"></a> Neste tópico
 [CppUnitTest.h](#cppUnitTest_h)

- [Criar classes de teste e métodos](#create_test_classes_and_methods)

- [Inicialização e limpeza](#Initialize_and_cleanup)

  -   [Métodos de teste](#test_methods)

  -   [Classes de teste](#test_classes)

  -   [Módulos de teste](#test_modules)

- [Criar atributos de teste](#create_test_attributes)

  - [Atributos de método de teste](#test_method_attributes)

  - [Atributos de classe de teste](#test_class_attributes)

  - [Atributos de módulo de teste](#test_module_attributes)

  - [Atributos predefinidos](#pre_defined_attributes)

    [CppUnitTestAssert.h](#cppUnitTestAssert_h)

  - [Declarações Gerais](#general_asserts)

    -   [São iguais](#general_are_equal)

    -   [Não são iguais](#general_are_not_equal)

    -   [São os mesmos](#general_are_same)

    -   [Não são os mesmos](#general_are_not_same)

    -   [É nulo](#general_is_null)

    -   [Não é nulo](#general_is_not_null)

    -   [É True](#general_is_True)

    -   [É False](#general_is_false)

    -   [Falha](#general_Fail)

  - [Declarações do Windows Runtime](#winrt_asserts)

    -   [São iguais](#winrt_are_equal)

    -   [São os mesmos](#winrt_are_same)

    -   [Não são iguais](#winrt_are_not_equal)

    -   [Não são os mesmos](#winrt_are_not_same)

    -   [É nulo](#winrt_is_null)

    -   [Não é nulo](#winrt_is_not_null)

  - [Declarações de Exceção](#exception_asserts)

    - [Exceção de Espera](#expect_exception)

      [CppUnitTestLogger.h](#cppunittestlogger_h)

    - [Logger](#logger)

    - [Gravar Mensagem](#write_message)

  - [Exemplo de uso](#example)

##  <a name="cppUnitTest_h"></a> CppUnitTest.h

###  <a name="create_test_classes_and_methods"></a> Criar classes de teste e métodos

```cpp
TEST_CLASS(className)
```

 Necessário para cada classe que contém métodos de teste. Identifica *className* como uma classe de teste. `TEST_CLASS` deve ser declarado no escopo do namescape.

```cpp
TEST_METHOD(methodName)
{
    // test method body
}
```

 Define *methodName* como um método de teste. `TEST_METHOD` deve ser declarado no escopo da classe do método.

###  <a name="Initialize_and_cleanup"></a> Inicialização e limpeza

####  <a name="test_methods"></a> Métodos de teste

```cpp
TEST_METHOD_INITIALIZE(methodName)
{
    // method initialization code
}
```

 Define *methodName* como um método executado antes de cada método de teste ser executado. `TEST_METHOD_INITIALIZE` só pode ser definido uma vez em uma classe de teste e deve ser definido na classe de teste.

```cpp
TEST_METHOD_CLEANUP(methodName)
{
    // test method cleanup  code
}
```

 Define *methodName* como um método executado após de cada método de teste ser executado. `TEST_METHOD_CLEANUP` só pode ser definido uma vez em uma classe de teste e deve ser definido no escopo da classe de teste.

####  <a name="test_classes"></a> Classes de teste

```cpp
TEST_CLASS_INITIALIZE(methodName)
{
    // test class initialization  code
}
```

 Define *methodName* como um método executado após de cada classe de teste ser criada. `TEST_CLASS_INITIALIZE` só pode ser definido uma vez em uma classe de teste e deve ser definido no escopo da classe de teste.

```cpp
TEST_CLASS_CLEANUP(methodName)
{
    // test class cleanup  code
}
```

 Define *methodName* como um método executado após de cada classe de teste ser executada. `TEST_CLASS_CLEANUP` só pode ser definido uma vez em uma classe de teste e deve ser definido no escopo da classe de teste.

####  <a name="test_modules"></a> Módulos de teste

```cpp
TEST_MODULE_INITIALIZE(methodName)
{
    // module initialization code
}
```

 Define o método *methodName* executado quando um módulo é carregado. `TEST_MODULE_INITIALIZE` só pode ser definido uma vez em um módulo de teste e deve ser declarado no escopo do namespace.

```cpp
TEST_MODULE_CLEANUP(methodName)
```

 Define o método *methodName* executado quando um módulo é descarregado. `TEST_MODULE_CLEANUP` só pode ser definido uma vez em um módulo de teste e deve ser declarado no escopo do namespace.

###  <a name="create_test_attributes"></a> Criar atributos de teste

####  <a name="test_method_attributes"></a> Atributos de método de teste

```cpp
BEGIN_TEST_METHOD_ATTRIBUTE(testMethodName)
    TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_METHOD_ATTRIBUTE()
```

 Adiciona os atributos definidos com um ou mais macros `TEST_METHOD_ATTRIBUTE` ao método de teste *testClassName*.

 Uma macro `TEST_METHOD_ATTRIBUTE` define um atributo com o nome *attributeName* e o valor *attributeValue*.

####  <a name="test_class_attributes"></a> Atributos de classe de teste

```cpp
BEGIN_TEST_CLASS_ATTRIBUTE(testClassName)
    TEST_CLASS_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_CLASS_ATTRIBUTE()
```

 Adiciona os atributos definidos com um ou mais macros `TEST_CLASS_ATTRIBUTE` à classe de teste *testClassName*.

 Uma macro `TEST_CLASS_ATTRIBUTE` define um atributo com o nome *attributeName* e o valor *attributeValue*.

####  <a name="test_module_attributes"></a> Atributos de módulo de teste

```cpp
BEGIN_TEST_MODULE_ATTRIBUTE(testModuleName)
    TEST_MODULE_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_MODULE_ATTRIBUTE()
```

 Adiciona os atributos definidos com um ou mais macros `TEST_MODULE_ATTRIBUTE` ao módulo de teste *testModuleName*.

 Uma macro `TEST_MODULE_ATTRIBUTE` define um atributo com o nome *attributeName* e o valor *attributeValue*.

####  <a name="pre_defined_attributes"></a> Atributos predefinidos
 Essas macros de atributo predefinidas podem ser substituídas pelas macros `TEST_METHOD_ATTRIBUTE`, `TEST_CLASS_ATTRIBUTE` OU `TEST_MODULE_ATTRIBUTE` descritas anteriormente.

```cpp
TEST_OWNER(ownerAlias)
```

 Define um atributo com o nome `Owner` e o valor de atributo de *ownerAlias*.

```cpp
TEST_DESCRIPTION(description)
```

 Define um atributo com o nome `Description` e o valor de atributo de *description*.

```cpp
TEST_PRIORITY(priority)
```

 Define um atributo com o nome `Priority` e o valor de atributo de *priority*.

```cpp
TEST_WORKITEM(workitem)
```

 Define um atributo com o nome `WorkItem` e o valor de atributo de *workItem*.

```cpp
TEST_IGNORE()
```

 Define um atributo com o nome `Ignore` e o valor de atributo de `true`.

##  <a name="cppUnitTestAssert_h"></a> CppUnitTestAssert.h

###  <a name="general_asserts"></a> Declarações Gerais

####  <a name="general_are_equal"></a> São iguais
 Verifica se dois objetos são iguais

```cpp
template<typename T>
static void Assert::AreEqual(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 Verifica se dois duplos são iguais

```cpp
static void Assert::AreEqual(
    double expected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 Verifica se dois floats são iguais

```cpp
static void Assert::AreEqual(
    float expected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 Verifica se duas cadeias de caracteres char* são iguais

```cpp
static void Assert::AreEqual(
    const char* expected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 Verifica se duas cadeias de caracteres w_char* são iguais

```cpp
static void Assert::AreEqual(
    const wchar_t* expected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

####  <a name="general_are_not_equal"></a> Não são iguais
 Verifica se dois duplos não são iguais

```cpp
static void Assert::AreNotEqual(
    double notExpected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 Verifica se dois floats não são iguais

```cpp
static void Assert::AreNotEqual(
    float notExpected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 Verifica se duas cadeias de caracteres char* não são iguais

```cpp
static void Assert::AreNotEqual(
    const char* notExpected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 Verifica se duas cadeias de caracteres w_char* não são iguais

```cpp
static void Assert::AreNotEqual(
    const wchar_t* notExpected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 Verifique se duas referências não são iguais com base em operator==.

```cpp
template<typename T>
static void Assert::AreNotEqual(
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

####  <a name="general_are_same"></a> São os mesmos
 Verifica se duas referências indicam a mesma instância de objeto (identidade).

```cpp
template<typename T>
static void Assert::AreSame(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

####  <a name="general_are_not_same"></a> Não são os mesmos
 Verifica se duas referências não indicam a mesma instância de objeto (identidade).

```cpp
template<typename T>
static void Assert::AreNotSame (
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

####  <a name="general_is_null"></a> É nulo
 Verifica se um ponteiro é NULO.

```cpp
template<typename T>
static void Assert::IsNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

####  <a name="general_is_not_null"></a> Não é nulo
 Verifica se um ponteiro não é NULO

```cpp
template<typename T>
static void Assert::IsNotNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

####  <a name="general_is_True"></a> É True
 Verifica se uma condição é true

```cpp
static void Assert::IsTrue(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

####  <a name="general_is_false"></a> É False
 Verifica se uma condição é false

```cpp
static void Assert::IsFalse(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

####  <a name="general_Fail"></a> Falha
 Força a falha do resultado do caso de teste

```cpp
static void Assert::Fail(
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

###  <a name="winrt_asserts"></a> Declarações do Windows Runtime

####  <a name="winrt_are_equal"></a> São iguais
 Verifica se dois ponteiros do Windows Runtime são iguais.

```cpp
template<typename T>
static void Assert::AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

 Verifica se duas cadeias de caracteres Platform::String^ são iguais.

```cpp
template<typename T>
static void Assert::AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

####  <a name="winrt_are_same"></a> São os mesmos
 Verifica se duas referências do Windows Runtime referenciam o mesmo objeto.

```cpp
template<typename T>
static void Assert::AreSame(
    T% expected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

####  <a name="winrt_are_not_equal"></a> Não são iguais
 Verifica se dois ponteiros do Windows Runtime não são iguais.

```cpp
template<typename T>
static void Assert::AreNotEqual(
    T^ notExpected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

 Verifica se duas cadeias de caracteres Platform::String^ não são iguais.

```cpp
static void Assert::AreNotEqual(
    Platform::String^ notExpected,
    Platform::String^ actual,
    bool ignoreCase = false,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

####  <a name="winrt_are_not_same"></a> Não são os mesmos
 Verifica se duas referências do Windows Runtime não referenciam o mesmo objeto.

```cpp
template<typename T>
static void Assert::AreNotSame(
    T% notExpected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

####  <a name="winrt_is_null"></a> É nulo
 Verifica se um ponteiro do Windows Runtime é um nullptr.

```cpp
template<typename T>
static void Assert::IsNull(
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

####  <a name="winrt_is_not_null"></a> Não é nulo
 Verifica se um ponteiro do Windows Runtime não é um nullptr.

```cpp
template<typename T>
static void Assert::IsNotNull(
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

###  <a name="exception_asserts"></a> Declarações de Exceção

####  <a name="expect_exception"></a> Exceção de Espera
 Verifica se uma função gera uma exceção:

```cpp
template<typename _EXPECTEDEXCEPTION, typename _FUNCTOR>
static void Assert::ExpectException(
    _FUNCTOR functor,
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo= NULL)
```

 Verifica se uma função gera uma exceção:

```cpp
template<typename _EXPECTEDEXCEPTION, typename _RETURNTYPE>
    static void Assert::ExpectException(
    _RETURNTYPE (*func)(),
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo = NULL)
```

##  <a name="cppunittestlogger_h"></a> CppUnitTestLogger.h

###  <a name="logger"></a> Logger
 A classe de agente contém métodos estáticos para gravar na **Janela de Saída**.

###  <a name="write_message"></a> Gravar Mensagem
Gravar uma cadeia de caracteres na **Janela de Saída**

```cpp
static void Logger::WriteMessage(const wchar_t* message)
```

```cpp
static void Logger::WriteMessage(const char* message)
```

## <a name="example"></a> Exemplo
 Esse código é um exemplo de uso do VSCppUnit. Ele inclui exemplos de metadados de atributo, acessórios, testes de unidade com asserções e registro em log personalizado.

```cpp
// USAGE EXAMPLE

#include <CppUnitTest.h>

using namespace Microsoft::VisualStudio::CppUnitTestFramework;

BEGIN_TEST_MODULE_ATTRIBUTE()
    TEST_MODULE_ATTRIBUTE(L"Date", L"2010/6/12")
END_TEST_MODULE_ATTRIBUTE()

TEST_MODULE_INITIALIZE(ModuleInitialize)
{
    Logger::WriteMessage("In Module Initialize");
}

TEST_MODULE_CLEANUP(ModuleCleanup)
{
    Logger::WriteMessage("In Module Cleanup");
}

TEST_CLASS(Class1)
{

public:

    Class1()
    {
        Logger::WriteMessage("In Class1");
    }

    ~Class1()
    {
        Logger::WriteMessage("In ~Class1");
    }

    TEST_CLASS_INITIALIZE(ClassInitialize)
    {
        Logger::WriteMessage("In Class Initialize");
    }

    TEST_CLASS_CLEANUP(ClassCleanup)
    {
        Logger::WriteMessage("In Class Cleanup");
    }

    BEGIN_TEST_METHOD_ATTRIBUTE(Method1)
        TEST_OWNER(L"OwnerName")
        TEST_PRIORITY(1)
    END_TEST_METHOD_ATTRIBUTE()

    TEST_METHOD(Method1)
    {
        Logger::WriteMessage("In Method1");
        Assert::AreEqual(0, 0);
    }

    TEST_METHOD(Method2)
    {
        Assert::Fail(L"Fail");
    }
};
```

## <a name="see-also"></a>Consulte também

- [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)
- [Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)

