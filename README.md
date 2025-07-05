# Blog (alhuff.com)

Source for my personal landing page + blog hosted at [alhuff.com](https://alhuff.com) - powered by Hugo & Hextra

## Local Development

Pre-requisites: [Hugo](https://gohugo.io/getting-started/installing/), [Go](https://golang.org/doc/install)

```shell
hugo mod tidy
hugo server --logLevel debug --disableFastRender -p 1313
```

### Update theme

```shell
hugo mod get -u
hugo mod tidy
```