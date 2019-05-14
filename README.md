> This project practices [README-driven development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html)

# hier-cms
a hierarchical git-based GraphQL CMS

## Examples

### Single File
    .
    ├── foo
    │   ├── bar.gql            # GQL input

#### Data

##### Define type interface
`bar.gql`
```gql
interface Bar {
  baz: Date!
}

{
  baz: "2019-05-14"
}
```

##### Infer type
`bar.gql`
```gql
{
  baz: "2019-05-14" # String inferred (unless parser is supplied)
}
```

##### Type directive
`bar.gql`
```gql
{
  baz: "2019-05-14" @date
}
```

#### Auto-generated Schema

```gql
type Query {
  foo: Foo!
}

type Bar {
  bar: FooBar!
}

type FooBar {
  baz: Date!
}
```

#### Query Request/Response
```gql
{
  foo {
    bar {
      baz
    }
  }
}
```
```json
{
  "data": {
    "foo": {
      "bar": {
        "baz": "2019-05-14"
      }
    }
  }
}
```
