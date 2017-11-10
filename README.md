[![Docker Build Statu](https://img.shields.io/docker/build/dockerniko/gitlab-ci-react-native-android.svg)]()
[![Docker Pulls](https://img.shields.io/docker/pulls/dockerniko/gitlab-ci-react-native-android.svg)]()
[![Docker Automated buil](https://img.shields.io/docker/automated/dockerniko/gitlab-ci-react-native-android.svg)]()


# gitlab-ci-react-native-android
GitLab CI image for building react native apps in Android  
Base on https://github.com/elviejokike/docker-hub/blob/master/react-native-android/Dockerfile

# lftp deployment
`lftp -e "mirror -R $LOCAL_DIR $REMOTE_DIR" -u $USERNAME,$PASSWORD $HOST`

GitLab CI image for building react native apps in Android
Base on https://github.com/elviejokike/docker-hub/blob/master/react-native-android/Dockerfile

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
