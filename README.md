## DEPRECATED

Please switch to the official service at http://archive.archlinux.org as our service will be turned off soon.

## A.R.M - Arch Rollback Machine
Arch Linux Chinese Community A.R.M server app & configurations.

### Configuration

Server requirements:

* Linux OS
* Bash & Rsync
* Python 3.3, distribute
* Node.js 0.10.13+ with NPM

#### Rsync

config file: Sync/.

Synchronize packages and make daily copies of package database file.
Packages are synchronized under `/var/www/repo-arm`

#### archrepo2

config file: archrepo2-0.3.1/archrepo.ini

Will read packages in [testing], [core], [extra], [multilib-testing], [multilib], [community-testing] and [community].

pkginfo file path: `/var/www/repo-arm/pkginfo.db`

#### repo-arm-server

config file: repo-arm-server/config.js

HTTP API:

**Exact package search**

* Method: POST
* Path: `/exact`
* Variables:
    - `arch` : `i686` || `x86_64`
    - `pkgname` : _Exact_ package name

Example using cURL:

`curl --data-urlencode "arch=x86_64" --data-urlencode "pkgname=linux" http://arm.example.com/exact`

**Similiar package search**

* Method: POST
* Path: `/find`
* Variables:
    - `arch` : `i686` || `x86_64`
    - `pkgname` : package name criteria

Example using cURL:

`curl --data-urlencode "arch=x86_64" --data-urlencode "pkgname=linux" http://arm.example.com/find`

**Deprecated GET method**

Pattern: `/search?arch=$arch&pkgname=$pkgname`
where `arch` can be either `i686` or `x86_64`, and `$pkgname` is _exactly_ the package name(packages under `any` will be automatically added to results).

Note for GET method: Special symbol like `+` should be encoded to `%2B`, or it will be trimmed and wont return the correct result.

**Returning results**

Server will return results like:
`pkgrepo|pkgname|arch|pkgver|downloadurl|pkgrelease`. 

Note: if there are multiple versions, it will display as multiple lines. If no package found, server will simply return nothing.

**Packages in specific date**

* For users seek for packages repo in a specific day, use the following url pattern as your repo address.

`http://repo-arm.archlinuxcn.org/archive/year/month/day/repo/arch`

e.g., for packages in `[core]` in the day of 2014/04/30, use `http://repo-arm.archlinuxcn.org/archive/2014/04/30/core/$arch`


#### Nginx

config file: NGINX/*.conf

A.R.M server url: `repo-arm.archlinuxcn.org` reverse proxy to 127.0.0.1:3000 (repo-arm-server)

A.R.M download url: `repo-arm-download.archlinuxcn.org`, webroot: /var/www/repo-arm/

~~**TODO** Implement daily-repo functionality.~~



