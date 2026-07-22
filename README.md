# maven-repository-template

[![GitHub license](https://img.shields.io/github/license/HighCapable/maven-repository-template?color=blue&style=flat-square)](https://github.com/HighCapable/maven-repository-template/blob/main/LICENSE)

This is a simple Maven repository by using GitHub to manage dependencies.



## Usage

The directory `repository` is the repository, which contains two parts: `releases` (release version) and `snapshots` (snapshots), where all Maven project artifacts are stored.

Reference this repository using the link below.

> Releases

```
https://raw.githubusercontent.com/randomusert/maven-repository/main/repository/releases
```

> SnapShots

```
https://raw.githubusercontent.com/randomusert/maven-repository/main/repository/snapshots
```

### Usage in Gradle Projects

You can use this repository in any Gradle project.

#### Configure Repository

```kotlin
repositories {
    maven {
        name = "personal-maven-repository-releases"
        setUrl("https://raw.githubusercontent.com/[organization name or username]/[repository name]/[branch name]/repository/releases")
    }
    maven {
        name = "personal-maven-repository-snapshots"
        setUrl("https://raw.githubusercontent.com/[organization name or username]/[repository name]/[branch name]/repository/snapshots")
    }
}
```

#### Publish Artifacts to Repository

It is recommended to use vanniktech's [gradle-maven-publish-plugin](https://vanniktech.github.io/gradle-maven-publish-plugin) to publish Maven artifacts.

Below is a reference for how to configure a repository to publish to.

You can publish the repository directly to the `.gradle/personal-maven-repository` directory under your local user directory, and then set `personal-maven-repository` as a git repository.

Connect the `personal-maven-repository` directory to GitHub.

After each release of artifacts, perform a `git commit` and `git push` to synchronize the current repository.

```kotlin
publishing {
    repositories {
        val repositoryDir = gradle.gradleUserHomeDir
            .resolve("personal-maven-repository")
            .resolve("repository")
        maven {
            name = "PersonalMavenReleases"
            url = repositoryDir.resolve("releases").toURI()
        }
        maven {
            name = "PersonalMavenSnapShots"
            url = repositoryDir.resolve("snapshots").toURI()
        }
    }
}
```


## License

- [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

```
Apache License Version 2.0

Copyright (C) 2026 Randomusert

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

Copyright © 2026 Randomusert
