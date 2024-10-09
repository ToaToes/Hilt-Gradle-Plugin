# To implement Room database in android app && To create DAO (Data Access Object), entity to integrate database in android

To solve ksp, dependency reference not found problem: 

Link: https://kotlinlang.org/docs/ksp-quickstart.html
<br/> Link: https://developer.android.com/build/migrate-to-ksp
<br/> Link: https://stackoverflow.com/questions/62882730/the-hilt-android-gradle-plugin-is-applied-but-no-com-google-daggerhilt-android

## Hilt-Gradle-Plugin
The Hilt Android Gradle plugin, and the dependency problems


For using **version catalog** and **KSP** in lib.version.toml (version catalog)

In toml file:
```

[versions]
agp = "8.2.2"
kotlin = "1.9.21"
ksp-version = "1.9.22-1.0.17"
hilt-version = "2.44"


[libraries]
...
hilt-android = { group = "com.google.dagger", name = "hilt-android", version.ref = "hilt-version" }
hilt-compiler = { group = "com.google.dagger", name = "hilt-android-compiler", version.ref = "hilt-version" }


[plugins]
ksp = { id = "com.google.devtools.ksp", version.ref = "ksp-version" }
hilt = { id = "com.google.dagger.hilt.android", version.ref = "hilt-version"}

```

In build.gradle.kts(project)
```
plugins {

  ...

  alias(libs.plugins.ksp) apply false
  alias(libs.plugins.hilt) apply false
}
```

In build.gradle.kts(Module:app)
```

plugins{

  ...

  alias(libs.plugins.ksp)
  alias(libs.plugins.hilt)
}

android{

  ...

  compileOptions{
    sourceCompatibility = JavaVersion.VERSION_17
    targetCompatibility = JavaVersion.VERSION_17
  }
  kotlinOptions{
    jvmTarget = "17"
  }

}

dependencies{

  ...

  implementation(libs.hilt.android)
  ksp(libs.hilt.compiler)

}
```
