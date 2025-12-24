
# Static Inheritance with `[[inline_compose]]`

**Warning:** This is a language concept. DO NOT USE in actual code

## Table of Contents

[Overview](#overview)

[Features](#features)

[Example](#example)

[Use Cases](#use-cases)

[Limitations](#limitations)

<!-- - [Installation](#installation) -->

<!-- - [Building](#building) -->

[Status](#status)

[License](#license)

## Overview

`[[inline_compose]]` is an experimental C++ attribute for inheritance

## Features

- No vtables
- Method inlining
- Field composition
- Cache-friendly
- No RTTI

## Example

```c++
#include <iostream>
#include <type_traits>

class base
{
public:
  base() : m_value(42) { }

  virtual void foo() { std::cout << m_value << '\n'; }

private:
  int m_value;
};

class derived :
  public [[inline_compose]] base
{
public:
  void bar() { std::cout << "derived\n"; }
};

derived d;
d.foo(); // direct call // 42
d.bar(); // normal call // derived

static_assert(std::is_base_of_v<base, derived> == false);
static_assert(std::is_polymorphic_v<derived> == false);
```

## Use Cases

- Performance-critical code without virtual dispatch

- Compile-time composition over inheritance

- Value-type composition

- Mixins and traits

## Limitations

- No polymorphism

- No upcasting or downcasting to parent types

- ABI-unstable

- Friend relationship not inherited

- Complete definitions required


## Status

**Experimental** - Proof of Concept

## License

MIT - see [LICENSE](LICENSE)