# DKSplit-Go

Go implementation of [DKSplit](https://github.com/ABTdomain/dksplit) - fast word segmentation for text without spaces.

Built with BiLSTM-CRF model and ONNX Runtime.

## Performance

| CPU | Mode | QPS |
|-----|------|-----|
| Intel Core i9-14900K | Single | 1,995/s |
| Intel Core i9-14900K | Batch | 8,101/s |
| Intel Core i9-9900K | Single | 1,444/s |
| Intel Core i9-9900K | Batch | 3,596/s |

Batch mode is **4.6x** faster than single mode.

Compared to Python version:
- Single: **2.7x** faster
- Batch: **5.6x** faster

## Install
```bash
go get github.com/ABTdomain/dksplit-go
```

## Usage
```go
package main

import (
    "fmt"
    "log"

    dksplit "github.com/ABTdomain/dksplit-go"
)

func main() {
    splitter, err := dksplit.New("models")
    if err != nil {
        log.Fatal(err)
    }
    defer splitter.Close()

    // Single
    result, _ := splitter.Split("chatgptlogin")
    fmt.Println(result)
    // Output: [chatgpt login]

    // Batch
    results, _ := splitter.SplitBatch([]string{"openaikey", "microsoftoffice"}, 256)
    fmt.Println(results)
    // Output: [[openai key] [microsoft office]]
}
```

## Examples

| Input | Output |
|-------|--------|
| chatgptlogin | chatgpt login |
| kubernetescluster | kubernetes cluster |
| microsoftoffice | microsoft office |
| mercibeaucoup | merci beaucoup |
| gutenmorgen | guten morgen |

## Requirements

- Go 1.21+
- Linux x64

## Links

- Website: [domainkits.com](https://domainkits.com), [ABTdomain.com](https://ABTdomain.com)
- Python version: [github.com/ABTdomain/dksplit](https://github.com/ABTdomain/dksplit)
- Documentation: [dksplit.readthedocs.io](https://dksplit.readthedocs.io)
- PyPI: [pypi.org/project/dksplit](https://pypi.org/project/dksplit)

## License

MIT