<div align="justify">

<div align="center">

```css
‌‌‌‌‬‬‬‍‌‌‌‌‌‬‌‌ _‌‌‌‌‌﻿‌‬_, ‌‌‌‌‌﻿‌‌  _   ‌‌‌‌‌﻿‌‬__,  _  ‌‌‌‌‌﻿‌‬ ,_‌‌‌‌‌‬‌‌  ‌‌‌‌‍‬﻿﻿‌‌‌‌‍﻿‍﻿    ‌‌‌‌‍‬﻿‌  ‌‌‌‌‌﻿‍‌  ‌‌‌‌‍‬‌﻿  ‌‌‌‌‍‬‍‍
/  | |/ \_/  |‌‌‌‌‌‬‌‌ |/‌‌‌‌‌﻿﻿‌  /  | ‌‌‌‌‍‬‌‍ [G]nu[‌‌‌‌‍‬﻿‌PG]
\_/|‌‌‌‌‍﻿‍‌/|‌‌‌‌‍‬‍‍__‌‌‌‌‍﻿‌‬/ \‌‌‌‌‍‬﻿‬_/|/‌‌‌‌‍‬‌‍‌‌‌‌‍﻿‍‌|‌‌‌‌‍‬‍‍__/‌‌‌‌‌‬﻿‍   |_‌‌‌‌‍﻿‌﻿/  ‌‌‌‌‍‬‍‍ ‌‌‌‌‌﻿‍﻿ ‌‌‌‌‍‬‍‍     
 ‌‌‌‌‍‬﻿‬ /|‌‌‌‌‍‌‌‌/‌‌‌‌‍﻿‌‌|      /‌‌‌‌‍‬﻿‍|    ‌‌‌‌‌‬﻿‬ ‌‌‌‌‍‬﻿‍  ‌‌‌‌‍‬‍‍         ‌‌‌‌‌﻿﻿‬    
  \|\|      \|  Recursive Sign[er]
```

</div>

## <samp>DEPENDENCIES</samp> <img alt="" align="right" src="https://badges.pufler.dev/visits/owl4ce/gpger?style=flat-square&label=&color=000000&logo=github&logoColor=white&labelColor=000000"/>

`sh` ( `coreutils` or `busybox` or `toybox` ) `gpg`

## <samp>INSTALLATION</samp>

```sh
💲 curl -s https://raw.githubusercontent.com/owl4ce/gpger/main/gpger \
| install -m755 - ~/.local/bin/gpger # $PATH
```

## <samp>USAGE</samp>

```sh
💲 gpger -h
```

```sh
* Simplify life with GnuPG Recursive Signer

USAGE
  gpger [options]

OPTIONS
  -s /path/to/your_files	[  sign  ]
  -v /path/to/your_files	[ verify ]
  -h				[  help  ]

ENVIRONMENT
  GPGER_SHA_BITS		Set the SHA bits to be used.
				1/224/256/384/512. Default 256.

https://github.com/owl4ce/gpger
```

Recursive example:

```sh
💲 # For `bash`, enable globstar (**) first.
💲 shopt -s globstar
```

```sh
💲 GPGER_SHA_BITS=512 gpger -s **/*
```

```sh
-x- Signing 'archiveexample.tar.xz' with detached signature file ...
gpg: using pgp trust model
gpg: writing to 'archiveexample.tar.sign'
gpg: RSA/SHA512 signature from: "xxxxxxxxxxxxxxxx xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>"

-x- Signing 'xyz.zip' with detached signature file ...
gpg: using pgp trust model
gpg: writing to 'xyz.zip.sign'
gpg: RSA/SHA512 signature from: "xxxxxxxxxxxxxxxx xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>"

-x- Compute and signing files\' digest with SHA512 ...
gpg: using pgp trust model
gpg: writing to 'sha512sums.asc'
gpg: RSA/SHA512 signature from: "xxxxxxxxxxxxxxxx xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>"

Everything is OK.
```

```sh
💲 GPGER_SHA_BITS=512 gpger -v **/*
```

```sh
-x- Verifying 'archiveexample.tar.xz' with detached signature file ...
gpg: armor header: Comment: This signature is for the .tar version of the archive
gpg: Signature made Thu Mar 31 23:25:07 2022 WIB
gpg:                using RSA key xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
gpg: using pgp trust model
gpg: Good signature from "xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>" [ultimate]
gpg: binary signature, digest algorithm SHA512, key algorithm rsa4096

-x- Verifying 'xyz.zip' with detached signature file ...
gpg: armor header: Comment: This signature is for the .zip version of the archive
gpg: Signature made Thu Mar 31 23:25:07 2022 WIB
gpg:                using RSA key xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
gpg: using pgp trust model
gpg: Good signature from "xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>" [ultimate]
gpg: binary signature, digest algorithm SHA512, key algorithm rsa4096

-x- Verifying signed files\' digest with SHA512 ...
gpg: armor header: Hash: SHA512
gpg: armor header: Version: GnuPG v2.2.34 (GNU/Linux)
gpg: original file name=''
gpg: Signature made Thu Mar 31 23:25:07 2022 WIB
gpg:                using RSA key xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
gpg: using pgp trust model
gpg: Good signature from "xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>" [ultimate]
gpg: textmode signature, digest algorithm SHA512, key algorithm rsa4096

-x- Checking SHA512 files\' digest ...
archiveexample.tar.xz: OK
klmnopqrstuvw/xyz.zip: OK

Everything is OK.
```

```sh
💲 # Disable globstar (**) if unnecessary.
💲 shopt -u globstar
```

## <samp>KNOWN RECURSIVE ISSUE</samp>

Sorts the first file found in globs, it will be terminated if the first found is a file from subdirectory.

Alphabetically, it's shell specific, find out ...

Reproduce the issue:

```sh
💲 printf '%s\n' dir/**/*
```

```sh
dir/archives
dir/archives/Gladient_JfD.tar.xz
dir/cherry-blossoms_FHD.jpg
dir/fonts
dir/fonts/Feather.ttf
dir/fonts/Material.ttf
```

```sh
💲 gpger -s dir/**/*
```

```sh
-x- Signing 'Gladient_JfD.tar.xz' with detached signature file ...
gpg: using pgp trust model
gpg: writing to 'Gladient_JfD.tar.sign'
gpg: RSA/SHA256 signature from: "xxxxxxxxxxxxxxxx xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>"

-x- Compute and signing files\' digest with SHA256 ...
sha256sum: dir/cherry-blossoms_FHD.jpg: No such file or directory
sha256sum: dir/fonts/Feather.ttf: No such file or directory
sha256sum: dir/fonts/Material.ttf: No such file or directory
Terminated
gpg: using pgp trust model
gpg: writing to 'sha256sums.asc'
gpg: RSA/SHA256 signature from: "xxxxxxxxxxxxxxxx xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>"
```

Current resolution:

```sh
💲 unset _; gpger -s dir/cherry-blossoms_FHD.jpg dir/[\!$_]**/*
```

```sh
-x- Signing 'Gladient_JfD.tar.xz' with detached signature file ...
gpg: using pgp trust model
gpg: writing to 'Gladient_JfD.tar.sign'
gpg: RSA/SHA256 signature from: "xxxxxxxxxxxxxxxx xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>"

-x- Compute and signing files\' digest with SHA256 ...
gpg: using pgp trust model
gpg: writing to 'sha256sums.asc'
gpg: RSA/SHA256 signature from: "xxxxxxxxxxxxxxxx xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>"

Everything is OK.
```

```sh
💲 unset _; gpger -v dir/cherry-blossoms_FHD.jpg dir/[\!$_]**/*
```

```sh
-x- Verifying 'Gladient_JfD.tar.xz' with detached signature file ...
gpg: armor header: Comment: This signature is for the .tar version of the archive
gpg: Signature made Thu Mar 31 23:19:36 2022 WIB
gpg:                using RSA key xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
gpg: using pgp trust model
gpg: Good signature from "xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>" [ultimate]
gpg: binary signature, digest algorithm SHA256, key algorithm rsa4096

-x- Verifying signed files\' digest with SHA256 ...
gpg: armor header: Hash: SHA256
gpg: armor header: Version: GnuPG v2.2.34 (GNU/Linux)
gpg: original file name=''
gpg: Signature made Thu Mar 31 23:19:37 2022 WIB
gpg:                using RSA key xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
gpg: using pgp trust model
gpg: Good signature from "xxxxx xxxx (xxxxxx) <xxxxxxxxxxxxxxx@xx.xx>" [ultimate]
gpg: textmode signature, digest algorithm SHA256, key algorithm rsa4096

-x- Checking SHA256 files\' digest ...
cherry-blossoms_FHD.jpg: OK
archives/Gladient_JfD.tar.xz: OK
fonts/Feather.ttf: OK
fonts/Material.ttf: OK

Everything is OK.
```

After the options, then input the file path that takes precedence before the files from subdirectory
and exclude the same file in globstar (\*\*) by making use of **$_** to not duplicate, so **shasum**
will be done there [dir] as the root directory. Remember that the `dir` directory is the same as
the demo in [usage](#usage), the difference is that we don't enter it as current directory.
Apart from that, for non-recursive (\*) and for recursive (\*\*/\*) with first file
found not from subdirectory no problem at all. Also, see https://shattered.io.

</div>
