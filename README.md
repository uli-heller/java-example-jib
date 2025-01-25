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

trivy image --input build/jib-image.tar \
 --format spdx-json --output trivy-spdx-jib-sbom.json
```
