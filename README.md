# https://github.com/serverless/serverless/issues/5759

```
$ sls version
1.36.3
$ grep -v -e '^\s*$' -e '^\s*#' serverless.yml
service:
  name: sls-5759-${file(other.yml):foo, "wat"}
provider:
  name: aws
  runtime: nodejs8.10
  environment:
    SERVICE: ${self:service.name}
    STAGE: ${opt:stage, self:provider.stage}
functions:
  hello:
    handler: handler.hello
$ sls print
service:
  name: sls-5759-wat
provider:
  name: aws
  runtime: nodejs8.10
  environment:
    SERVICE: wat
    STAGE: dev
functions:
  hello:
    handler: handler.hello
