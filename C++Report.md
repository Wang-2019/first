
**测试time类中的elapsedInUSec函数**
```C++
uint64_t Duration::elapsedInUSec() const {
    uint64_t ticks = isPaused_ ? accumulated_ : readTsc() - startTick_ + accumulated_;
    return ticks * ticksPerUSecFactor.load();
}
```
```C++
TEST(Duration, elapsedInMicroSeconds) {
    Duration dur;
    for (int i = 0; i< 10; i++) {
        dur.reset();
        auto start = std::chrono::steady_clock::now();
        usleep(3);
        auto diff = std::chrono::steady_clock::now() - start;
        dur.pause();
        ASSERT_LE(std::chrono::duration_cast<std::chrono::microseconds>(diff).count() - 3,
                    dur.elapsedInUSec()) << "Inaccuracy in iteration " << i;
        ASSERT_GE(std::chrono::duration_cast<std::chrono::microseconds>(diff).count() + 3,
                    dur.elapsedInUSec()) << "Inaccuracy in iteration " << i;
        ASSERT_EQ(std::chrono::duration_cast<std::chrono::microseconds>(diff).count(),
                  dur.elapsedUInSec()) << "Inaccuracy in iteration " << i;

    }
}
```

![Pfailed](https://github.com/Wang-2019/first/blob/C%2B%2Bhomework/failed.png)

当使用ASSERT_EQ函数测试elapsedInUSec函数是会报错
这样说明使用elapsedInUSec函数是会出现一定程度的误差，这样的误差可能是由于函数自身精度的问题所造成的，即小数点保留位数问题
****************************************************************************************************************************************
```C++
TEST(Duration, elapsedInMicroSeconds) {
    Duration dur;
    for (int i = 0; i< 10000; i++) {
        dur.reset();
        auto start = std::chrono::steady_clock::now();
        usleep(3);
        auto diff = std::chrono::steady_clock::now() - start;
        dur.pause();
        ASSERT_LE(std::chrono::duration_cast<std::chrono::microseconds>(diff).count() - 3,
                    dur.elapsedInUSec()) << "Inaccuracy in iteration " << i;
        ASSERT_GE(std::chrono::duration_cast<std::chrono::microseconds>(diff).count() + 3,
                    dur.elapsedInUSec()) << "Inaccuracy in iteration " << i;
    }
}
```
![Nfailed](https://github.com/Wang-2019/first/blob/C%2B%2Bhomework/Nfaild.png)

当迭代次数增加时也会报错
这样说明迭代次数越多，误差越明显
****************************************************************************************************************************************
```C++
TEST(Duration, elapsedInMicroSeconds) {
    Duration dur;
    for (int i = 0; i< 150; i++) {
        dur.reset();
        auto start = std::chrono::steady_clock::now();
        usleep(3);
        auto diff = std::chrono::steady_clock::now() - start;
        dur.pause();
        ASSERT_LE(std::chrono::duration_cast<std::chrono::microseconds>(diff).count() - 2,
                    dur.elapsedInUSec()) << "Inaccuracy in iteration " << i;
        ASSERT_GE(std::chrono::duration_cast<std::chrono::microseconds>(diff).count() + 2,
                    dur.elapsedInUSec()) << "Inaccuracy in iteration " << i;

    }
}
```
![passed](https://github.com/Wang-2019/first/blob/C%2B%2Bhomework/build.png)

当迭代次数为150时，elapsedInUSec函数误差可以控制在4以内
 
**心得体会：**
    不要被庞大的数据吓到，当你先看一小部分，慢慢理解，会发现这些代码并不像自己想象中的那么难，困难总是有的，但是一点一点磨，也肯定能够看明白一些，在专研的过程中也让我们学到了不少东西。C++这门课程让我们真正接触到了一些企业级的编程，虽然不多也不够深入，但却和之前c语言与数据结构有所不同。如果说c语言是我们编程的入门，数据结构是我们编程的进阶，那么C++这门课程便是让我们将编程与实际联系起来的那一条纽带，为我们以后，不论是实习工作或是考研深造都奠定了基础。
