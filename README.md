> This project practices [README-driven development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html)

# hier-cms
a hierarchical git-based GraphQL CMS

## Example Folder structure
    .
    ├── foo.gql      # Single GraphQL
    ├── foo.yaml     # Single YAML
    ├── bar
    |   |── baz.gql  # Nesting/Namespacing
    |── qux          # Collections
    |   |── Qux.gql  # Interface (optional)
    |   |── a.gql    # single input
    |   |── b.gql    # single input
    |   |── c.gql    # Multiple inputs

### Explicit interface (adds validation)
`foo.gql` 
```gql
interface Foo {
  date: Date!
}

{
  date: "2019-05-14"
}
```
```gql
type Query {
  date: Foo!
}

type Foo {
  date: Date!
}
```

### Infer type
`foo.gql`
```gql
{
  date: "2019-05-14" # String inferred (unless parser is supplied)
}
```
or
`foo.yaml`
```yaml
date: 2019-05-14
```

### Explicit inline type
`foo.gql`
```gql
{
  date: "2019-05-14" @date
}
```
or
`foo.yaml`
```yaml
date: !date 2019-05-14
```

### Optional curlies
`foo.gql`
```gql
date: "2019-05-14"
```

### Optional key
`foo.gql`
```gql
"2019-05-14"
```
or
`foo.yaml`
```gql
2019-05-14
```
```gql
type Query {
  foo: String!
}
```

### Nesting/Namespacing
`bar/baz.gql`
```gql
date: "2019-05-14"
```
```gql
type Query {
  bar: Bar!
}
type Bar {
  baz: BarBaz!
}
type BarBaz {
  date: Date!
}
```

### Collection
`qux/a.gql`
```
message: "hello world"
```
generates
```gql
type Query {
  qux: Qux!
}
type Qux {
  message: String!
}
```
but adding an interface: `qux/Qux.gql`
```
interface Qux {    # interface, name, and curlies optional
  message: String!
}
```
or a second: `qux/b.gql`
```
message: "hello hier"
```
generates
```gql
type Query {
  qux: [Qux!]!
}
type Qux {
  message: String!
}
```
including multiple inputs per file: `qux/c.gql`
```gql
{ message: "hello first" }
{ message: "hello second" }
{ message: "hello third" }
```
