# Compilation Error Example

The following code in the com.schuetz.Context class produces a compilation error:

```kotlin
package com.schuetz

object Context {
    fun <K : Any, V : Any> record(slice: Slice<K, V>, key: K, value: V): Unit = TODO("Not important for example")
    fun <K : Any, V : Any> get(slice: Slice<K, V>, key: K): V? = TODO("Not important for example")

    interface Slice<K: Any, V: Any>

    object Slices {
        object GENERAL: Slice<GENERAL.Key<*>, Any> {
            interface Key<T: Any> { // <- Error: Unresolved reference: Any
                fun get(): T {
                    return Context.get(GENERAL, this) as T
                }
                fun record(value: T) {
                    Context.record(GENERAL, this, value as Any)
                }
            }

            object Test: Key<String>
        }
    }
}
```
