## 0.6.1 ([commit log](https://github.com/japgolly/scalajs-react/compare/v0.6.0...v0.6.1))

##### Core module
* Changed overloaded `classSet` methods into `classSet{,1}{,M}`.
* Styles now given to React in camel case. No more warnings.

##### Test module
* `ComponentOrNode` moved to test module and renamed to `ReactOrDomNode`.
* `ReactTestUtils` now accept plain old `ReactElement`s.
* Added `Sel.findFirstIn`.
* Added `simulateKeyDownUp` and `simulateKeyDownPressUp` to `KeyboardEventData` in the test module.
* In rare circumstances, `Simulation.run` targets can go out of date. Targets are now stored by-name.

# 0.6.0 ([commit log](https://github.com/japgolly/scalajs-react/compare/v0.5.4...v0.6.0))

This release brings scalajs-react in line with React 0.12.
**React version 0.12.0 or later is now required.**

Read about React 0.12 changes here:
*  https://github.com/facebook/react/releases/tag/v0.12.0
*  https://facebook.github.io/react/blog/2014/10/28/react-v0.12.html
*  https://facebook.github.io/react/docs/glossary.html

##### Scala 2.10 is no longer supported.
If this affects you please come to [issue #39](https://github.com/japgolly/scalajs-react/issues/39) to discuss,
or continue to using the 0.5.x series.

##### Other changes in this release:
* Deprecated `ReactOutput` and `VDom` in favour of `ReactElement` or in rare cases, `ReactNode`. (*[glossary](https://facebook.github.io/react/docs/glossary.html)*)
* `.asJsArray: Seq[A] → JArray[A]` renamed to `toJsArray`
* `.toJsArray: Seq[A] → JArray[ReactElement]` is no longer needed.
* Renamed `ComponentSpec` to `ReactComponentSpec`. *(Internal. Extremely unlikely anyone using it directly.)*
* Changed signatures of `ReactS.callback` and brethren from `(c)(a)` to `(a,c)`.
* Renamed `ReactS` methods for consistency and added a few missing ones.

Here are a few commands to ease migration.
```
find -name '*.scala' -exec perl -pi -e 's/(?<!\w)(vdom\.)?ReactOutput(?!\w)/ReactElement/g' {} +
find -name '*.scala' -exec perl -pi -e 's/(?<!\w)VDom(?!\w)/ReactElement/g' {} +
find -name '*.scala' -exec perl -pi -e 's/(?<!\w)asJsArray(?!\w)/toJsArray/g' {} + // careful...
find -name '*.scala' -exec perl -pi -e 's/(?<=[ .]render)Component//g' {} +
```
