# Android 基础



> Android四大组件：Activity、BroadcastReceiver、Service、ContentProvider。

## Activity（四大组件之一）

### 生命周期

![](<../../.gitbook/assets/image (9).png>)

为了在 Activity 生命周期的各个阶段之间导航转换，Activity 类提供六个核心回调：`onCreate()`、`onStart()`、`onResume()`、`onPause()`、`onStop()` 和 `onDestroy()`。当 Activity 进入新状态时，系统会调用其中每个回调。

* `onCreate()`：您必须实现此回调，它会在系统首次创建 Activity 时触发。Activity 会在创建后进入“已创建”状态。在 `onCreate()` 方法中，您需执行基本应用启动逻辑，该逻辑在 Activity 的整个生命周期中只应发生一次。例如，[`onCreate()`](https://developer.android.google.cn/reference/android/app/Activity#onCreate\(android.os.Bundle\)) 的实现可能会将数据绑定到列表，将 Activity 与 [`ViewModel`](https://developer.android.google.cn/reference/androidx/lifecycle/ViewModel) 相关联，并实例化某些类作用域变量。`onCreate()` 方法完成执行后，Activity 进入“已开始”状态，系统会相继调用 `onStart()` 和 `onResume()` 方法。
* `onStart()`：当 Activity 进入“已开始”状态时，系统会调用此回调。`onStart()` 调用使 Activity 对用户可见，因为应用会为 Activity 进入前台并支持互动做准备。`onStart()` 方法会非常快速地完成，并且与“已创建”状态一样，Activity 不会一直处于“已开始”状态。一旦此回调结束，Activity 便会进入“已恢复”状态，系统将调用 `onResume()` 方法。
* `onResume()`：Activity 会在进入“已恢复”状态时来到前台，然后系统调用 `onResume()` 回调。这是应用与用户互动的状态。应用会一直保持这种状态，直到某些事件发生，让焦点远离应用。此类事件包括接到来电、用户导航到另一个 Activity，或设备屏幕关闭。当发生中断事件时，Activity 进入“已暂停”状态，系统调用 `onPause()` 回调。如果 Activity 从“已暂停”状态返回“已恢复”状态，系统将再次调用 `onResume()` 方法。因此，您应实现 `onResume()`，以初始化在 [`onPause()`](https://developer.android.google.cn/reference/android/app/Activity#onPause\(\)) 期间释放的组件，并执行每次 Activity 进入“已恢复”状态时必须完成的任何其他初始化操作。
* `onPause()`：统将此方法视为用户将要离开您的 Activity 的第一个标志（尽管这并不总是意味着 Activity 会被销毁）；此方法表示 Activity 不再位于前台（尽管在用户处于多窗口模式时 Activity 仍然可见）。使用 [`onPause()`](https://developer.android.google.cn/reference/android/app/Activity#onPause\(\)) 方法暂停或调整当 [`Activity`](https://developer.android.google.cn/reference/android/app/Activity) 处于“已暂停”状态时不应继续（或应有节制地继续）的操作，以及您希望很快恢复的操作。您还可以使用 [`onPause()`](https://developer.android.google.cn/reference/android/app/Activity#onPause\(\)) 方法释放系统资源、传感器（例如 GPS）手柄，或当您的 Activity 暂停且用户不需要它们时仍然可能影响电池续航时间的任何资源。`onPause()` 方法的完成并不意味着 Activity 离开“已暂停”状态。相反，Activity 会保持此状态，直到其恢复或变成对用户完全不可见。如果 Activity 恢复，系统将再次调用 `onResume()` 回调。如果 Activity 变为完全不可见，系统会调用 `onStop()`。
* `onStop()`：如果您的 Activity 不再对用户可见，说明其已进入“已停止”状态，因此系统将调用 `onStop()` 回调。在 `onStop()` 方法中，应用应释放或调整在应用对用户不可见时的无用资源。您还应使用 `onStop()` 执行 CPU 相对密集的关闭操作。例如，如果您无法找到更合适的时机来将信息保存到数据库，可以在 `onStop()` 期间执行此操作。当您的 Activity 进入“已停止”状态时，`Activity` 对象会继续驻留在内存中：该对象将维护所有状态和成员信息，但不会附加到窗口管理器。Activity 恢复后，Activity 会重新调用这些信息。
* `onDestroy()`：销毁 Ativity 之前，系统会先调用 [`onDestroy()`](https://developer.android.google.cn/reference/android/app/Activity#onDestroy\(\))。如果 Activity 即将结束，onDestroy() 是 Activity 收到的最后一个生命周期回调。[`onDestroy()`](https://developer.android.google.cn/reference/android/app/Activity#onDestroy\(\)) 回调应释放先前的回调（例如 [`onStop()`](https://developer.android.google.cn/reference/android/app/Activity#onStop\(\))）尚未释放的所有资源。

稍微简洁一点的生命周期相关定义可以见《第一行代码》中「活动的生命周期」一节：

![图源：《第一行代码》郭霖](<../../.gitbook/assets/image (6) (1).png>)

## Service（四大组件之一）

### 生命周期

## BroadcastReceiver（四大组件之一）

## ContentProvider（四大组件之一）

## Fragment

生命周期、在Activity的基础上添加了几个方法。

## 消息机制

{% embed url="https://hit-alibaba.github.io/interview/Android/basic/Android-handler-thread-looper.html" %}

以及android-interview中的消息机制部分

post和sendmessage的区别：

{% embed url="https://www.jianshu.com/p/43d6cd7b06f1" %}

{% embed url="https://www.jianshu.com/p/5e4c01497cf7" %}
looper拿到更新ui的代码交给handler去处理，所以和使用sendmessage效果一致，也是在主线程中更新UI
{% endembed %}

## Android 多线程

* AsyncTask
* HandlerThread
* IntentService

看android-interview

## AsyncTask

内部封装了两个线程池和一个Handler

主要是五个核心方法：onPreExecute、doInBackground、publishProgress、onProgressUpdate、onPostExecute。

## HandlerThread

{% embed url="https://www.jianshu.com/p/741295000e5a" %}

注意点：

* 有俩Handler，mWorkerHandler和mUIHandler，mWorkerHandler使用子线程（DownloadThread，继承自HandlerThread）的looper，子线程的looper取出消息队列里的消息，调用子线程的handlermessage进行耗时操作，做完了之后就mUIHandler.sendMessage通知主线程，主线程的handler，即mUIHandler，就可以在handlerMessage里根据传来的信息更新UI啦。
* 这样，HandlerThread里可以进行多个耗时的下载任务，都在子线程的MessageQueue中排队等着。Looper会一个个取出来执行的。

## IntentService

> 看android-interview

主要是重写 onHandleIntent

发多少个 intent 过去都要老实排队，按照顺序执行。



