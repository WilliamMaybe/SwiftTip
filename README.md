#Swift Tip
##访问控制
类型|权限
---|---
open|可以被任何人使用，包括override和继承。
public|可以被任何人访问。但其他module中不可以被override和继承，而在module内可以被override和继承。
internal|internal访问级别所修饰的属性或方法在源代码所在的整个模块都可以访问。如果是框架或者库代码，则在整个框架内部都可以访问，框架由外部代码所引用时，则不可以访问。如果是App代码，也是在整个App代码，也是在整个App内部可以访问。
fileprivate|fileprivate访问级别所修饰的属性或者方法在当前的Swift源文件里可以访问。
private|private访问级别所修饰的属性或者方法只能在当前类里访问。

在学习RxSwift的过程中，遇到的关于访问权限的问题，工程使用pod倒入RxSwift搭建demo，很想使用`castOrThrow<T>`这个func，但是就是用不了，在`RxCocoa.swift`中明明就没有使用private、fileprivate的字眼，怎么就不能用了呢。

```
func castOrThrow<T>(_ resultType: T.Type, _ object: Any) throws -> T {
    guard let returnValue = object as? T else {
        throw RxCocoaError.castingError(object: object, targetType: resultType)
    }

    return returnValue
}

```
这个方法是一个全局方法，而不写权限默认使用的是`internal`，所以如果是直接将源码添加到工程的话，即满足在同个module下的概念，是可以用的。
###听说使用好权限可以增加编译速度😱
