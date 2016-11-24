# bin-downloader
Binary file downloader.

## Main "help" output
```
GitHub binary scripts downloader
Version: 0.1.0

USING
  Download your binary file
    $ curl -Ls https://raw.github.com/rikby/bin-downloader/master/download | bash -s -- \\
          your-vendor/some-name \\
          dir/some-file.sh -- \\
          --filename|-f some-file \\
          --version|-v v0.2.1

    $ curl URL | bash -s -- REPO FILE \\
      [--end-message "message"|--help-app|--app-name "my name"] -- \\
      [--file FILE|-f FILE|--filename NAME|-n NAME|--versions|--version 0.1.2]

    $ curl URL | bash -s -- REPO FILE [SCRIPT OPTIONS] -- [USER OPTIONS]

SCRIPT SPECIFIC OPTIONS
  REPO          Repository full name "vendor/name" in github.com.
  FILE          Requested file in the passed repository.
  --end-message This will be showed in the end of downloading.
                %s will be replaced with full path to downloaded file.
                Default: "Binary file: %s\n"
  --app-help    Show help for application downloader
  --app-name    Use passed name in help.

END USER OPTIONS
  --versions    Show created tags.
  --version|-v  Created tag name or branch name.
                Default: last tag or master if there is no tags.
  --file|-f     Path to save downloaded file.
  --filename|-n Name to downloaded file by default path.
                (/usr/local/bin or /usr/bin)

```

# Create your own downloader
Create your "download" script in your master branch in the repository root.
Please replace "your-vendor/some-name" string with your path.

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
curl -Ls https://raw.github.com/rikby/bin-downloader/master/download | bash -s -- \\
    your-vendor/some-name \\
    dir/some-file.sh -- --filename some-file \$@
```

See example in [semversort project](/../../../../rikby/semversort/blob/master/download)
