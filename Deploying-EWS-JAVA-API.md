> The following steps can only be done by authorized persons

### Init/Checks
* Checkout the latest fresh branch from `https://github.com/OfficeDev/ews-java-api` or make sure your local copy contains no further or uncommited changes and is up-to-date (`git pull && git status -s`)
  * if your branch contains local changes wipe them <br/>`git add -A && git commit -qm 'WIPE SAVEPOINT' && git reset HEAD~1 --hard`
* make sure you are on the correct branch (master for instance)

### Update pom.xml to new Version
* edit `pom.xml` change `<version>X.X-SNAPSHOT</version>` to `<version>X.X</version>`
* commit the actual changes (pom.xml) to the local repository **(dont push)**

### Announce public key (if not already done)
* Your public key needs to be announced once. To do this you can:
  * `gpg --list-keys`
  * `gpg --keyserver hkp://pgp.mit.edu --send-keys <public key name>`<br/>_keyname could be: C7FFB27B for instance_

### Deployment
* run `mvn clean deploy -Dgpg.passphrase=$GPGPASS`

### Create a TAG for that Version
* run `git tag -a ews-java-api-`**x.x**` -m 'Tag: ews-java-api-x.x'` 
* if something was wrong delete that tag <br/>`git tag -d ews-java-api-x.x`
* before pushing make sure there are no other local tags you probably dont want to push <br/>`git tag -l` 
* push the current tag `git push --tags`

### Revert the commited changes (we dont want them on the central repo)
* make sure the latest commit was the pom.xml change
* wipe it: <br/> `git reset --hard HEAD~1`

### Update gh-pages
* run `mvn clean site`
* navigate to the folder where you store your github repositories
* checkout a fresh copy of gh-pages or update your local copy<br/>
  `git clone -b gh-pages --single-branch https://github.com/OfficeDev/ews-java-api.git gh-pages && cd gh-pages`
* copy mvn generated files to gh-pages
  * `mkdir -m777 -v -p "./docs/releases/<version>"`
  * copy all the files to the new dir<br/>
`cp -Rf "<ews-java-api-repo>/target/site/*"` "./docs/releases/<version>"
  * add new files to git `git add . `
  * commit new files <br/> `git commit -m "Release mvn site to [gh-pages]`

> if current Version is ALPHA/Beta you can skip the next steps an goto [[Be social and celebrate :checkered_flag:|Deploying-EWS-JAVA-API#be-social-and-celebrate-checkered_flag]]

### Delete actual branch
* _[Optional]_ maybe development on that actual branch is finished now. If thats true delete that branch _(if not master :wink: )_ <br/> `git push origin --delete <branchName>`

### New Version / new Branch
* Think of a new Version regarding the actual roadmap. New Versionnumber should match [Semantic Versioning](http://semver.org/)
* Create a new branch <br/> `git checkout -b <newBranchName>`
* edit `pom.xml` change `<version>X.X</version>` to `<version><newVersion>-SNAPSHOT</version>`
* commit latest changes
* Push that branch to remote `git push <remote-name> <newBranchName>`

### See travis building the new Snapshot Version
* [travis:builds](https://travis-ci.org/OfficeDev/ews-java-api/builds)

### Be social and celebrate :checkered_flag:
* let others know that there has been a new release and branch to work with
  * inform others on [gitter](https://gitter.im/OfficeDev/ews-java-api)
* celebrate the new release :palm_tree: :tada: :dancers: 