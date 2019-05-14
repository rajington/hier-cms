> This project practices [README-driven development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html)

# hier-cms
a hierarchical git-based GraphQL CMS

## Example Folder structure
    .
    ├── foo.gql                # Single GraphQL
    ├── foo.yaml               # Single YAML
    ├── bar
    |   |── baz.gql            # Nesting/Namespacing

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
2019-05-14
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
