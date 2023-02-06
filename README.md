# incremental-unpacked-klib

1. `./gradlew assemble --info`
0. Move `lib/src/main/kotlin/bar/barUseAB.kt` into `app/src/main/kotlin/bar`
0. `./gradlew assemble --info`

Can see in `Kotlin2JsCompile#callCompilerAsync` `inputChanges`, added and modified `~/.gradle/caches/transforms-3/b6ab9afb3656b1a4e4a4fea3d25c0b75/transformed/kotlin-stdlib-js-1.9.0-dev-1048.jar/`, but file system watch can't see any changes in such directories.
