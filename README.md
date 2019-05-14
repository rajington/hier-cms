> This project practices [README-driven development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html)

# hier-cms
a hierarchical git-based GraphQL CMS

## Examples

### Single File
    .
    ├── ...
    ├── foo
    │   ├── bar.gql            # GQL input
    └── ...

#### Define type interface
`bar.gql`
```gql
interface Bar {
  qux: Date!
}

{
  qux: "2019-05-14"
}
```

#### Infer type
`bar.gql`
```gql
{
  qux: "2019-05-14" # String inferred (unless parser is supplied)
}
```

#### Type directive
`bar.gql`
```gql
{
  qux: "2019-05-14" @date
}
```
