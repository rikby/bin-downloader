# bin-downloader
Binary file downloader.

## Help output
```
GitHub binary scripts downloader
Version: 0.1.0

USING
  Download your binary file
    $ curl -Ls https://raw.github.com/rikby/bin-downloader/master/download \
          --repo|-p your-vendor/some-name \
          --repo-file|-r dir/some-file.sh \
          --version|-v v0.2.1

OPTIONS
  --versions    Show created tags.
  --version|-v  Created tag name or branch name.
                Default: last tag or master if there is no tags.
  --repo|-p     Repository full name "vendor/name" in github.com.
  --repo-file|-r
                Requested file in the passed repository.
  --file|-f     Path to save downloaded file.
  --filename|-n Name to downloaded file by default path.
                (/usr/local/bin or /usr/bin)
  --finish-message
                This will be showed in the end of downloading.
                %s will be replaced with full path to downloaded file.
                Default: "Binary file: %s\n"
```
