# Publish Android Library to Jitpack


## 1. Edit Gradle

In the `build.gradle` file of your library module, add the following code to the `plugins` block:

```gradle
plugins {
    ...
    id 'maven-publish'
}
```

Then, at the bottom of the file, add the following code:

```gradle
afterEvaluate {
    publishing {
        publications {
            // Creates a Maven publication called "release".
            release(MavenPublication) {
                // Applies the component for the release build variant.
                from components.release

                // You can then customize attributes of the publication as shown below.
                groupId = 'com.github.VictorKuang25.myLibrary'
                artifactId = 'libraryName'
                version = '1.0.0'
            }
        }
    }
}
```

Replace `com.github.VictorKuang25.myLibrary`, `libraryName` and `1.0.0` with your library module's Group Id, Artifact Id, and version number. This step is used to publish your library module to the Maven Central repository, so that other users can easily reference it.

## 2. Push to Github

Use Git to push the project to Github. Make sure to include your `build.gradle` and `settings.gradle` files.

## 3. Release Repository

In Github, click on the `Releases` tab, select `Create a new release`, input the version number and relevant information, then click on `Publish release`.



## 4. Add Dependency to Project

Go to [JitPack](https://jitpack.io/) and log in with your GitHub account. Then, select your repository.

In the `settings.gradle` file, add the following code so that Gradle can get dependencies from the JitPack repository:

```gradle
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```

Add the dependencies in the `build.gradle` file:

```gradle
dependencies {
    implementation 'com.github.username:library:version'
}
```

Replace `username`, `library`, and `version` with your GitHub account, project name, and version number.
