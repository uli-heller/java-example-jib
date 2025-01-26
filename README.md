java-example-jib
================

This is an example project.
I use it to verify the creation
of an SBOM for a container image
with the help of TRIVY

Please note: I know that typically,
you integrate sub projects via "settings.gradle".
This is NOT what I want to do here!
I want the sub project to show up as
independent components of my java project!

Here is the test procedure:

```
./create-maven-repository.sh
./gradlew build
./gradlew jibBuildTar
# ... creates build/jib-image.tar 107M

trivy image --input build/jib-image.tar \
 --format cyclonedx --output trivy-cdx-jib-sbom.json
./cdx-2-csv-2.sh <trivy-cdx-jib-sbom.json  >trivy-cdx-jib-sbom.csv

trivy image --input build/jib-image.tar \
 --format spdx-json --output trivy-spdx-jib-sbom.json
./spdx-2-csv-2.sh <trivy-spdx-jib-sbom.json  >trivy-spdx-jib-sbom.csv
```

Here the outcome:

Format   | SBOM (json)                                        | SBOM (csv)
---------|----------------------------------------------------|-----------
CycloneDX|[trivy-cdx-jib-sbom.json](trivy-cdx-jib-sbom.json)  |[trivy-cdx-jib-sbom.csv](trivy-cdx-jib-sbom.csv)
Spdx-Json|[trivy-spdx-jib-sbom.json](trivy-spdx-jib-sbom.json)|[trivy-spdx-jib-sbom.csv](trivy-spdx-jib-sbom.csv)

Potential Problems
------------------

### Could not find cool.heller.uli:hello-world:0.9.0

You probably missed executing `./create-maven-repository.sh`!

```
uheller@uliip5:~/git/github/uli-heller/java-example-jib$ ./create-maven-repository.sh 

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller.uli:hello-world:0.8.0 to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository

BUILD SUCCESSFUL in 763ms
5 actionable tasks: 5 executed

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller.uli:hello-world:0.9.0 to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository/

BUILD SUCCESSFUL in 505ms
5 actionable tasks: 4 executed, 1 up-to-date

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller.uli:hello-world:0.9.1 to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository/

BUILD SUCCESSFUL in 512ms
5 actionable tasks: 4 executed, 1 up-to-date

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller.uli:bye-moon:0.8.0 to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository/

BUILD SUCCESSFUL in 611ms
5 actionable tasks: 5 executed

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller.uli:bye-moon:0.9.0 to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository/

BUILD SUCCESSFUL in 507ms
5 actionable tasks: 4 executed, 1 up-to-date

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller.uli:bye-moon:1.0-SNAPSHOT to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository/

BUILD SUCCESSFUL in 495ms
5 actionable tasks: 4 executed, 1 up-to-date

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller:maybe-mars:1.0.0 to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository/

BUILD SUCCESSFUL in 580ms
5 actionable tasks: 5 executed

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller:maybe-mars:1.0.1 to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository/

BUILD SUCCESSFUL in 502ms
5 actionable tasks: 4 executed, 1 up-to-date

> Task :publishJavaPublicationToLocal-registryRepository
Publishing cool.heller:maybe-mars:1.1.0-BETA to file:/home/uheller/git/github/uli-heller/java-example-jib/maven-repository/

BUILD SUCCESSFUL in 516ms
5 actionable tasks: 4 executed, 1 up-to-date
```
