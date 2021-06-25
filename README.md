## GraalVM container with native image
---

## Why
---
We could install graalVM and native image itself (e.g. using [sdkman](https://sdkman.io/)) but there's an alternative - docker container.
* no need to install anything (assuming that docker is already installed) & convenient
* host system agnostic (concerns Windows & Macs)

## Usage
---
`./build.sh` builds docker image containing `native-image`. Built image could be used

Executable binary (which is called also native image) could be build using following command
```sh
docker run -it 
  -v <HOST_CLASSPATH_DIRECTORY>:/opt/cp 
  -v <HOST_RESULT_DIRECTORY>:/opt/graalvm 
  graal-native-image
  "--static" 
  "-H:Name=<OUT_NAME>" 
  "<MAIN_CLASS>"
```
`HOST_CLASSPATH_DIRECTORY` - this directory has to contains all of our app dependencies (jars) including application jar itself.  
`HOST_RESULT_DIRECTORY` - directory where the result would be written
`OUT_NAME` - the name of created native image  
`MAIN_CLASS` - entrypoint of our app that contains `main` method  
`--static` - static native images are statically linked binaries which can be used without any additional library dependencies. This makes them suitable for use in a Docker container [[docs](https://www.graalvm.org/reference-manual/native-image/StaticImages/)]