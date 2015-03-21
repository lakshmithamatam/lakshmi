# Running a local build
To build your own jar you will need to [install maven](http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) and [fork/clone](https://help.github.com/articles/fork-a-repo) the latest version of _ews-java-api_.

## Building without GnuPG
After the installation you can navigate to your local repository via cmd and run `mvn clean install`. This will validate the available unit-tests und build all necessary jars which afterwards may be found @ `PROJECT_ROOT\target`.

## Building with GnuPG _(for Project Team)_
_ews-java-api_ also supports the use of signing artifacts with GnuPG using the [maven-gpg-plugin](https://maven.apache.org/plugins/maven-gpg-plugin). If you want to know how to setup your environment you can find an introduction at the [sonatype-blog](http://blog.sonatype.com/2010/01/how-to-generate-pgp-signatures-with-maven/#.VQ2YW46G9zs). For building _ews-java-api_ specify the passphrase for your private key on the command line by adding the parameter `-Dgpg.passphrase=EnterPassphraseHere`. For example:
* `mvn clean install -Dgpg.passphrase=EnterPassphraseHere` or
* `mvn clean deploy -Dgpg.passphrase=EnterPassphraseHere`