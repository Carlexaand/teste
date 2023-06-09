# Golden tests
Golden tests, also called screenshot tests, let's you write tests to easily
find UI regressions. It compares the UI to saved golden screenshots, and if
there is a pixel difference the tests will fail. It gives us confidence that
code changes does not cause UI regressions.

## Updating goldens
An expected change to the UI will also cause the golden tests to fail. If this
is unintended, you will need to change your code to prevent the UI change. If
it was intended, you will then need to update the goldens by running the
following command on your machine:
```bash
flutter test --update-goldens
```

Due to slight [differences](
https://github.com/flutter/flutter/issues/36667#issuecomment-521335243)
in rendering across platforms, mostly around text, the tests will only be run
on a Linux machine on Github Actions (because it's cheaper). This means that
if you update the tests on a macOS or Windows machine the golden tests will
not pass on Github Actions. Instead you are recommended to download the
goldens directly from the failed Github Actions job, and use those inside of
your branch.

You can find the goldens under Artifacts in the top menu inside of the failed
Github Actions job. It will include the master image, your test image and the
difference.

![Where to download the golden artifacts](
https://user-images.githubusercontent.com/1770678/80202787-70f1de80-8626-11ea-9d98-58ac72f67479.png)

## Shadows in golden tests
In the golden tests the shadows are opaqued, to [reduce the likelihood of
golden file tests being flaky](https://api.flutter.dev/flutter/flutter_test/LiveTestWidgetsFlutterBinding/disableShadows.html).
A side effect of this is that we are not testing the exact rendering of shadows
inside of the goldens.
