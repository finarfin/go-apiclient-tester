# go-apiclient-tester
[![GoDoc-Postman](https://godoc.org/github.com/finarfin/go-apiclient-tester/postman?status.svg)](https://godoc.org/github.com/finarfin/go-apiclient-tester/postman)
[![GoDoc-Tester](https://godoc.org/github.com/finarfin/go-apiclient-tester/tester?status.svg)](https://godoc.org/github.com/finarfin/go-apiclient-tester/tester)

A simple, easy to use library to test HTTP based API clients.

Main use-case for this library is to be able to use [Postman Collections](https://learning.postman.com/docs/postman/collections/intro-to-collections/) for unit testing. Create requests/examples in [Postman](https://www.postman.com/); then export as "Collection v2.1" format. It can verify that requests from your API client match to the ones in the collection and respond with the recorded response.

## Example

```go
    package awesomeclient

    import (
        "testing"
        "github.com/finarfin/go-apiclient-tester/postman"
        "github.com/finarfin/go-apiclient-tester/tester"
        "github.com/stretchr/testify/assert"
    )

    func TestUserCreateSuccess(t *testing.T) {
        tester, err := postman.NewTester("testdata/collection.json")        
        if err != nil {
            t.Fatal(err)
        }
        defer tester.Close()
        tester.Setup("user", "create_success")

        _, err = c.CreateUser("user1")
        if err != nil {
            t.Fatal(err)
        }
    }

    func TestUserCreateFailure(t *testing.T) {
        tester, err := postman.NewTester("testdata/collection.json")
        if err != nil {
            t.Fatal(err)
        }
        defer tester.Close()
        tester.Setup("user", "create_failure")

        _, err = c.CreateUser("user1")
        assert.Error(t, err)
    }
```

## License

[MIT](LICENSE)
