
![www](https://github.com/Wang-2019/first/blob/C%2B%2Bhomework/build.png)
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

当使用ASSERT_EQ函数测试elapsedInUSec函数是会报错
![Pfailed](https://github.com/Wang-2019/first/blob/C%2B%2Bhomework/failed.png)

这样说明使用elapsedInUSec函数是会出现一定程度的误差，这样的误差可能是由于函数自身精度的问题所造成的，即小数点保留位数问题

当迭代次数过多时也会报错
![Nfailed]()
