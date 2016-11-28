# bin-downloader
Binary file downloader.

One point with downloading your binary file from a repository.

## Using
## Create your own downloader
Create your "download" script in your master branch in the repository root.
In this case the link will similar: https://raw.github.com/your-vendor/some-name/master/download

Add template below and replace following:
- `your-vendor/some-name` -vendor name and repository name
- `--app-name "My_Name_downloader"` - Title for downloader
- `dir/some-file.sh` - target file
- `--filename some-file` - output filename (it will be store in /usr/local/bin or in /usr/bin)

```bash
#!/usr/bin/env bash
# Fetch binary file
#   $ curl -Ls https://raw.github.com/your-vendor/some-name/master/download | bash
# See help:
#   $ curl -Ls https://raw.github.com/your-vendor/some-name/master/download | bash -s -- --help
set -o errexit
set -o pipefail
set -o nounset
#set -o xtrace

# Download
curl -Ls https://raw.github.com/rikby/bin-downloader/master/download | bash -s -- \
    your-vendor/some-name \
    dir/some-file.sh --app-name "My_Name_downloader" -- \
    --filename some-file \$@
```
Underscores in `My_Name_downloader` will be replaced with spaces.

### Add a link into a documentation

> Fetch binary file<br>
>   `$ curl -Ls https://raw.github.com/your-vendor/some-name/master/download | bash`<br>
> See help:<br>
>   `$ curl -Ls https://raw.github.com/your-vendor/some-name/master/download | bash -s -- --help`<br>

### Allowed "help" for end users
```
$ curl -Ls https://raw.github.com/your-vendor/some-name/master/download | bash -s -- --help
My Name downloader

USING
  Download your binary file
    $ curl -Ls https://raw.github.com/your-vendor/some-name/master/download | bash

  Or use some options
    $ curl -Ls https://raw.github.com/your-vendor/some-name/master/download | bash -s -- \
          --filename|-f some-file \
          --version|-v v0.2.1

OPTIONS
  --versions    Show created tags.
  --version|-v  Created tag name or branch name.
                Default: last tag or master if there is no tags.
  --file|-f     Path to save downloaded file.
  --filename|-n Name of downloaded file by default path.
                (/usr/local/bin or /usr/bin)
  --help        Show this help.

```

## Main "help" output
```
GitHub binary scripts downloader
Version: 0.1.0

USING
  Download your binary file
    $ curl -Ls https://raw.github.com/rikby/bin-downloader/master/download | bash -s -- \
          your-vendor/some-name \
          dir/some-file.sh -- \
          --filename|-f some-file \
          --version|-v v0.2.1

    $ curl URL | bash -s -- REPO FILE \
      [--end-message "message"|--app-name "my name"] -- \
      [--file FILE|-f FILE|--filename NAME|-n NAME|--versions|--version 0.1.2]

    $ curl URL | bash -s -- REPO FILE [SCRIPT OPTIONS] -- [USER OPTIONS]

SCRIPT SPECIFIC OPTIONS
  REPO          Repository full name "vendor/name" in github.com.
  FILE          Requested file in the passed repository.
  --end-message This will be showed in the end of downloading.
                %s will be replaced with full path to downloaded file.
                Default: "Binary file: %s\n"
  --app-name    Use passed name in 3rd party downloader help.
                Use "_" instead spaces in the name. "_" will be replaced with spaces.
  --downloader  Custom 3rd party downloader path in repository.
                Uses in 3rd party downloader help.
                Example: my-branch/my/path/downloader
                Default: master/downloader
                Where "master" is a branch name.
  --help        Show this help.

END USER OPTIONS
  --versions    Show created tags.
  --version|-v  Created tag name or branch name.
                Default: last tag or master if there is no tags.
  --file|-f     Path to save downloaded file.
  --filename|-n Name to downloaded file by default path.
                (/usr/local/bin or /usr/bin)
  --help        Show help for 3rd party downloader.
```

## Short link
[Downloader link](https://raw.github.com/rikby/bin-downloader/master/download) has a short link: https://goo.gl/ve2Xvw
```
curl -Ls https://goo.gl/ve2Xvw | bash -s -- --help
```

See example in [semversort project](/../../../../rikby/semversort/blob/master/download)
