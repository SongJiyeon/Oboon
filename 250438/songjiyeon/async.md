---
marp: true
theme: beam
---

<!-- _class: title -->

# 나만 몰랐나 async 이름의 비밀

부제: await으로 synchronously 동작하게 하는데 왜 이름은 async인가

---

# 우리가 알고있던 async와 sync

<p width="100%">
    <img width="80%" src="./asyncSync.png" />
</p>

---

# 그치만 실제 사용하는 async function은..

```swift
func asyncMethod() async -> Void {
    await A()
    await B()
    C()
}
```

---

# async 마크는 내부 로직에 대한 것이 아니었다 (반전)

async를 함수에 씀으로서 스레드를 suspend 하겠다고 컴파일러에게 말하는 것

---

# suspend가 async인 이유?!

<br>

<p width="100%">
    <img width="80%" src="./blocking-vs-suspension.png" />
</p>

---

# Playground에서 확인해보기

```swift
func printAsync(num: Int, second: Int = 1) async {
    try? await Task.sleep(for: .seconds(second))
    print("♻️ printAsync \(num)")
}

func printBlocking(num: Int, second: Int = 1) {
    print("❗ Starting printBlocking \(num)")
    Thread.sleep(forTimeInterval: Double(second))
    print("❗ Finished printBlocking \(num)")
}

func printSync(num: Int) {
    print("⭐ printSync \(num)")
}
```

---

# Playground에서 확인해보기

```swift
func printAsync(num: Int, second: Int = 1) async {
    try? await Task.sleep(for: .seconds(second))
    print("♻️ printAsync \(num)")
}

func printBlocking(num: Int, second: Int = 1) async {
    print("❗ Starting printBlocking \(num)")
    Thread.sleep(forTimeInterval: Double(second))
    print("❗ Finished printBlocking \(num)")
}

func printSync(num: Int) {
    print("⭐ printSync \(num)")
}
```

---

# Playground에서 확인해보기

```swift
func printAsync(num: Int, second: Int = 1) async {
    try? await Task.sleep(for: .seconds(second))
    print("♻️ printAsync \(num)")
}

func printBlocking(num: Int, second: Int = 1) {
    print("❗ Starting printBlocking \(num)")
    try await Task.sleep(forTimeInterval: Double(second))
    print("❗ Finished printBlocking \(num)")
}

func printSync(num: Int) {
    print("⭐ printSync \(num)")
}
```

---

## 끗

---

# Refernces

<br>

<small>

Apple Developer Documentation: Concurrency
<a href="https://developer.apple.com/documentation/swift/concurrency">https://developer.apple.com/documentation/swift/concurrency</a>

Swift.org Documentation: Swift Concurrency
<a href="https://docs.swift.org/swift-book/documentation/the-swift-programming-language/concurrency/">https://docs.swift.org/swift-book/documentation/the-swift-programming-language/concurrency/</a>

WWDC 2021: Meet async/await in Swift
<a href="https://developer.apple.com/videos/play/wwdc2021/10132/">https://developer.apple.com/videos/play/wwdc2021/10132/</a>

WWDC 2021: Explore structured concurrency in Swift
<a href="https://developer.apple.com/videos/play/wwdc2021/10134/">https://developer.apple.com/videos/play/wwdc2021/10134/</a>

Swift Evolution Proposal: SE-0296 Async/await
<a href="https://github.com/apple/swift-evolution/blob/main/proposals/0296-async-await.md">https://github.com/apple/swift-evolution/blob/main/proposals/0296-async-await.md</a>

Swift Evolution Proposal: SE-0304 Structured Concurrency
<a href="https://github.com/apple/swift-evolution/blob/main/proposals/0304-structured-concurrency.md">https://github.com/apple/swift-evolution/blob/main/proposals/0304-structured-concurrency.md</a>

</small>
