Repro for https://github.com/gradle/gradle/issues/13590

To repro:

1. With the code as is, dry-run `someTask`. As you can see, there is no task dependency on `otherTask`, despite the output property of `otherTask` being linked up with an input of `someTask`.
   ```
   $ ./gradlew --dry-run someTask
   :someTask SKIPPED
   ```
2. Change the `@Nested` on `SomeTask` to `@Input` - the task dependency is now linked up, which is what we'd expect in the nested case too:
   ```
   $ gw --dry-run someTask
   :otherTask SKIPPED
   :someTask SKIPPED
   ```
