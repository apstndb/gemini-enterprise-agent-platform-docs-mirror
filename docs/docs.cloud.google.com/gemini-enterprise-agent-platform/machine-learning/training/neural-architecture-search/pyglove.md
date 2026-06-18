---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/pyglove
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/pyglove
title: PyGlove language reference
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Run the Agent Platform Neural Architecture Search tutorial: [Create search spaces](https://github.com/google/vertex-ai-nas/blob/main/third_party/tutorial/vertex_tutorial2.md) to get familiar with the [PyGlove](https://github.com/google/pyglove) language.

## Constraints for PyGlove types

Value specification (for example, `pg.typing.Int()` ) can be provided when users declare members for a class using `@pg.members` or arguments for a functor using `@pg.functor` . Value specification will validate the values during construction and member assignment.

### `pg.typing.Bool`

    # Declare a required Bool type.
    pg.typing.Bool()
    # Declare a Bool type with default value set to True.
    pg.typing.Bool(default=True)
    
    # Declare a Bool type that can accept None.
    pg.typing.Bool().noneable()

### `pg.typing.Str`

    # Declare a required Str type.
    pg.typing.Str()
    # Declare a required Str type that matches a regular expression.
    pg.typing.Str(regex='.*foo')
    
    # Declare a Str type with default value set to 'x'.
    pg.typing.Str(default='x')
    
    # Declare a Str type that can accept None.
    pg.typing.Str().noneable()

### `pg.typing.Int`

    # Declare a required Int type.
    pg.typing.Int()
    # Declare a required Int type with minimum and maximum value.
    pg.typing.Int(min_value=1, max_value=10)
    
    # Declare an Int type with default value set to 10.
    pg.typing.Int(default=10)
    
    # Declare an Int type that can accept None.
    pg.typing.Int().noneable()

### `pg.typing.Float`

    # Declare a required Float type.
    pg.typing.Float()
    # Declare a required Float type with minimum and maximum value.
    pg.typing.Float(min_value=0.0, max_value=1.0)
    
    # Declare a Float type with default value set to 0.0.
    pg.typing.Float(default=0.0)
    
    # Declare a Float type that can accept None.
    pg.typing.Float().noneable()

### `pg.typing.Enum`

    # Declare a required Enum type with default value set to 1.
    pg.typing.Enum(1, [1, 'a', 'b'])
    
    # Declare a Enum type that can accept None with default value set to 1.
    pg.typing.Enum(1, [1, 'a', 'b']).noneable()

### `pg.typing.List`

    # Declare a required list of any type.
    pg.typing.List(pg.typing.Any())
    
    # Declare a required Int type (or None) list with at least two elements.
    pg.typing.List(pg.typing.Int().noneable(), min_size=2)
    
    # Declare a Float type list of fixed size (10) that can be None.
    pg.typing.List(pg.typing.Float(), size=10).noneable()
    
    # Declare a Str type list with a default value.
    pg.typing.List(pg.typing.Str(), default=['foo'])

### `pg.typing.Tuple`

    # Declare a required Int type tuple of size 2.
    pg.typing.Tuple([pg.typing.Int(), pg.typing.Int()])
    
    # Declare a tuple of (Int, Str) types, which can also be None.
    pg.typing.Tuple([pg.typing.Int(), pg.typing.Str()]).noneable()
    
    # Declare an Int type tuple of size 2 with a default value.
    pg.typing.Tuple([pg.typing.Int(), pg.typing.Int()], default=(1, 1))

### `pg.typing.Dict`

    # Declare a required dictionary of any key-value pairs.
    pg.typing.Dict()
    
    # Declare a dictionary that can accept None with field 'a' and 'b'.
    pg.typing.Dict([
      ('a', pg.typing.Int()),
      ('b', pg.typing.Str()),
    ]).noneable()
    
    # Declare a dictionary that can accept None with field 'a' and 'b'.
    pg.typing.Dict([
      ('a', pg.typing.Int(default=1)),
      ('b', pg.typing.Str()),
    ]).noneable()
    
    # Declare a dictionary with keys that match regular expression.
    pg.typing.Dict([
      (pg.typing.StrKey('.*foo'), pg.typing.Int()),
    ])

### `pg.typing.Object`

    # Declare a required instance of class A.
    pg.typing.Object(A)
    
    # Declare an instance of class A that can accept None.
    pg.typing.Object(B)

### `pg.typing.Union`

    # Declare a required union of Int and Str types.
    pg.typing.Union([pg.typing.Int(), pg.typing.Str])
    
    # Declare a union of Int and Str types that can accept None.
    pg.typing.Union([pg.typing.Int(), pg.typing.Str]).noneable()

### `pg.typing.Any`

    # Declare a required value of any type (except None) with a default value.
    pg.typing.Any(default=1)
    
    # Declare a value of any type that can accept None.
    pg.typing.Any().noneable()
