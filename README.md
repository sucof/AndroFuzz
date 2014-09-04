## AndroFuzz

A simple file format fuzzer for android. Used by me to fuzz pdf readers, but should work for any file format.

Because of a (probably incorrect) design choice, AndroFuzz does not create any files itself but must rely on other file format fuzzers, such as SPIKEfile to create the files.  Instead of implementing this capability, I made AndroFuzz able to fuzz a number of readers at once.

This is the current mode AndroFuzz uses to work:

    1. Files generated by fuzzer (not AndroFuzz)

    2. AndroFuzz pushes files to Android emulator

    3. AndroFuzz pushes the first apk of one of the apps we are testing to the emulator and installs it

    4. The app loads the files and is fuzzed. AndroFuzz monitors logcat for buffer overflows and will alert the user if any occur

    5. Once all the files are tested on the app, the app is uninstalled and the process, starting at step 3 is started for the next app

Currently AndroFuzz is incomplete and unready for real fuzzing since it requires users to manually generate the fuzzing files using some other program.
Additionally, the above model in which not many files are tested on many apps, is probably unlikely to cause many interesting crashes.

AndroFuzz will be given a more sane, traditional model some time in the near future.
