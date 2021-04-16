# test-case-for-stackoverflow-67114825

This is a test case to demonstrate the "implicit dependency" problem reported in the
StackOverflow question [Can I get more information about “implicit dependencies” in Gradle 7.0?](https://stackoverflow.com/questions/67114825/)

1. Clone the repo
2. Run `./gradlew doall`

Observe that you get this warning:

> Task :pointless_gzip
> Execution optimizations have been disabled for task ':pointless_gzip' to ensure correctness due to the following reasons:
> * Gradle detected a problem with the following location: '/Users/ndw/Projects/nwalsh/so-bugs/gradle7-implicit/build/pointless.tar'. Reason: Task ':pointless_gzip' uses this output of task ':copyA' without declaring an explicit or implicit dependency. This can lead to incorrect results being produced, depending on what order the tasks are executed. Please refer to https://docs.gradle.org/7.0/userguide/validation_problems.html#implicit_dependency for more details about this problem.
> Gradle detected a problem with the following location: '/Users/ndw/Projects/nwalsh/so-bugs/gradle7-implicit/build/pointless.tar'. Reason: Task ':pointless_gzip' uses this output of task ':copyA' without declaring an explicit or implicit dependency. This can lead to incorrect results being produced, depending on what order the tasks are executed. Please refer to https://docs.gradle.org/7.0/userguide/validation_problems.html#implicit_dependency for more details about this problem. This behaviour has been deprecated and is scheduled to be removed in Gradle 8.0. Execution optimizations are disabled to ensure correctness. See https://docs.gradle.org/7.0/userguide/more_about_tasks.html#sec:up_to_date_checks for more details.

It appears that any step that takes any input from a directory is
implicitly dependent on all steps that write to that directory. That
seems burdonsome to me, but I suppose one can work around it by using
different subdirectories for temporary files.
