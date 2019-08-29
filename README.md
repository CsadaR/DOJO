# Nab's dojo
<img src=dojo.jpg width=400 /> <sup id="a1">[[1]](#f1)</sup>

# Fields
- [Codewars](https://codewars.com)
- [Project Euler](https://projecteuler.net)
- [LeetCode](https://leetcode.com)
- [AtCoder](https://atcoder.jp)
- [AWS Lambda](https://aws.amazon.com/lambda/)

# Testing
```sh
(cd {{field_directory}} && ginkgo)
```

# AWS Lambda
## Install dependencies
```sh
go mod why
```

## Dispatch on local
```sh
mage lbd:dispatch
```

## Testing
```bash
mage lbd:test
```
or
```sh
(cd aws_lambda && ginkgo)
```

## Deploy
```sh
mage lbd:deploy
```

## Clean
```sh
mage lbd:clean
```

---

## LISENCE
MIT

## EPILOGUE
>     A whale!
>     Down it goes, and more, and more
>     Up goes its tail!
>
>     -Buson Yosa

---

<b id="f1">[1]</b> "Two Buddhist monks, playing chess" (1863-1872, John Thomson) credited in Wellcome Collection is licensed by [CC 4.0 BY](https://creativecommons.org/licenses/by/4.0/) [↩](#a1)
