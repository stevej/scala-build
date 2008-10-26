
Folder layout:
  src/  -- source code
    main/
      scala/
      java/
      jni/
      thrift/
      resources/  -- files to copy into dist
    test/
      scala/
      resources/  -- files needed only for tests
    scripts/
  ivy/
    ivy.xml  -- package description
    ivysettings.xml  -- repositories
  config/  -- items to package in the distribution but not in jars

Created during the build:
  target/  -- compiled files
    classes/
    test-classes/
    gen-java/  -- generated from thrift
    scripts/
  dist/
    <package>-<version>/
      libs/  -- dependent jars
      config/  -- copied over
      resources???


... tbd ...

Primary targets
---------------
  - clean
    - erase all generated/built files
  - prepare
    - resolve dependencies and download them
  - compile
    - build any java/scala source
  - test
    - build and run test suite (requires e:testclass)
  - docs
    - generate documentation
  - package
    - copy all generated/built files into distribution folder


Properties that can change behavior
-----------------------------------

- skip.download
    don't download ivy; assume it's present
- libs.extra
- dist.extra
- skip.test


Extra ivy thingies
------------------

- e:thriftpackage
- e:buildpackage
- e:testclass
- e:stresstestclass
- e:jarclassname


  tests are only built & run if:
    - ivy.xml defines "e:testclass"
    - "skip.test" is not defined
  docs are only built if:
    - "skip.docs" is not defined
  build.properties is generated only if:
    - ivy.xml defines "e:buildpackage"


  ivy attributes:
    - e:thriftpackage
      output package for generated thrift classes; causes thrift DDLs to be compiled

  ant properties:
    - libs.extra
      any extra files to copy into dist/libs/ during packaging
    - dist.extra
      any extra files to copy into dist/ during packaging
