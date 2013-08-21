##A.R.M - Arch Rollback Machine
Server scripts

###Usage

1. Install Node.js

2. `git clone https://github.com/phoenixlzx/repo-arm-server && cd repo-arm-server && npm install`

3. `node app.js`

This application reads the `pkginfo.db` file created by lilydjwg's dbutils, which will include all package info under a directory.

###TODO

* Add `repo` field to pkginfo.db so this app will read and return it to downgrade client.

* A basic webpage that could search package directly.
