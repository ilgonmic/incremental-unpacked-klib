# incremental-unpacked-klib

## First case with `inputChanges` problem

1. `./gradlew assemble --info`
2. Move `lib/src/main/kotlin/bar/barUseAB.kt` into `app/src/main/kotlin/bar`
3. `./gradlew assemble --info`

Can see in `Kotlin2JsCompile#callCompilerAsync` `inputChanges`, added and modified `~/.gradle/caches/transforms-3/b6ab9afb3656b1a4e4a4fea3d25c0b75/transformed/kotlin-stdlib-js-1.9.0-dev-1048.jar/`, but file system watch can't see any changes in such directories.

## Second case with `FileCollection` configuration cache problem

1. `./gradlew :app:test --configuration-cache`
2. `./gradlew clean`
3. `./gradlew assemble --configuration-cache`

The problem that `Kotlin2JsCompile#libraries` is not cached properly. It misses local dependencies despite the first run it works.
