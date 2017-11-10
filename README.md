[![Docker Build Statu](https://img.shields.io/docker/build/magiczvn/gitlab-ci-react-native-android.svg)]()
[![Docker Pulls](https://img.shields.io/docker/pulls/magiczvn/gitlab-ci-react-native-android.svg)]()
[![Docker Automated buil](https://img.shields.io/docker/automated/magiczvn/gitlab-ci-react-native-android.svg)]()


# gitlab-ci-react-native-android
GitLab CI image for building react native apps in Android  
Base on https://github.com/linehat/gitlab-ci-react-native-android/blob/master/Dockerfile

# .gitlab-ci.yml

```sh
image: magiczvn/gitlab-ci-react-native-android

cache:
  paths:
  - node_modules/
  - .gradle/

stages:
- build

before_script:
- export GRADLE_USER_HOME=$(pwd)/.gradle
- chmod +x ./android/gradlew

build:
  stage: build
  
  script:
  - npm install
  - cd android && ./gradlew assembleDebug --stacktrace
  - mv ./app/build/outputs/apk/app-debug.apk ../../app-debug.apk
  artifacts:
   paths:
   - app-debug.apk
```
