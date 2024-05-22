# lfm-api
![GitHub Release](https://img.shields.io/github/v/release/twangodev/lfm-api)
![GitHub License](https://img.shields.io/github/license/twangodev/lfm-api)


lfm-api is a Go package that provides an interface to interact with the [Last.fm API](https://www.last.fm/api), allowing you to retrieve information about a users recent scrobbles, without the need for an API key.

## Installation

Install the package using `go get`:

```bash
go get github.com/twangodev/lfm-api
```

## Usage

The primary function of the package is to retrieve a users recent scrobbles. To do this, you can use the `GetActiveScrobble` function:

```go

func main() {
    // Get the most recent scrobble
    scrobble, err := lfm.GetActiveScrobble("twangodev")
    if err != nil {
        fmt.Println(err)
        return
    }

    fmt.Println(scrobble)
}
```

The `GetActiveScrobble` function returns a `Scrobble` struct, which contains the following fields:

```go
type Scrobble struct {
	Active        bool      // Whether the user is actively scrobbling
	Name          string    // The name of the track
	Artist        string    // The artist of the track
	Album         string    // The album of the track
	Loved         bool      // Whether the user loves the track
	DataId        string    // A unique ID used to identify the scrobble, generated by Last.FM
	DataTimestamp time.Time // When the user began scrobbling
	DataLink      string    // A link to the track (YouTube, etc.)
	DataLinkTitle string    // A description for the dataLink
	CoverArtUrl   string    // A URL to the album cover art
}
```

!!! tip
    The `GetActiveScrobble` function will return `EmptyScrobble` if the user is not actively scrobbling.

    `EmptyScrobble` is a `Scrobble` struct with all fields set to their zero values, and `Active` set to `false`.

    ```go
    var EmptyScrobble = Scrobble{
        Active: false,
    }
    ```

> [!IMPORTANT]
> The underlying implementation used by `lfm-api` utilizes an unofficial endpoint of the Last.fm API, which allows the package to obtain information without an API key. As such, the API may change or be removed at any time. The package is provided as-is, with no guarantees of support or functionality.
> When building applications that rely on the Last.fm API, it is recommended to use the official API and obtain an API key. However, for simple applications or personal use, `lfm-api` provides a quick and easy way to retrieve scrobble information.
> It is recommended to use this package on the client-side only, as it may not scale well for server-side applications, and could potentially be rate-limited by Last.fm.
> For more information about `lfm-api`, you can view the source code on [GitHub](https://github.com/twangodev/lfm-api).

## Roadmap

The following features are planned for future releases of `lfm-api`, if the unofficial endpoint remains available, and there is interest in the features

- Retrieving more than the most recent scrobble
- Retrieving a users top tracks
- Retrieving a users top artists
- Retrieving a users top albums

If you would like to see any of these features implemented, or have any other suggestions, feel free to open an issue on the [GitHub repository](https://github.com/twangodev/lfm-api).