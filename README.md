<div align="center">
  <h1>
    <br/>
    <br/>
    👍
    <br />
    react-use
    <br />
    <br />
    <br />
    <br />
  </h1>
  <sup>
    <br />
    <br />
    <a href="https://www.npmjs.com/package/react-use">
       <img src="https://img.shields.io/npm/v/react-use.svg" alt="npm package" />
    </a>
    <a href="https://circleci.com/gh/streamich/react-use">
      <img src="https://img.shields.io/circleci/project/github/streamich/react-use/master.svg" alt="CircleCI master" />
    </a>
    <a href="https://www.npmjs.com/package/react-use">
      <img src="https://img.shields.io/npm/dm/react-use.svg" alt="npm downloads" />
    </a>
    <a href="http://streamich.github.io/react-use">
      <img src="https://img.shields.io/badge/demos-🚀-yellow.svg" alt="demos" />
    </a>
    <br />
    Collection of essential <a href="https://reactjs.org/docs/hooks-intro.html">React Hooks</a>.</em>
    <em>Port of</em> <a href="https://github.com/streamich/libreact"><code>libreact</code></a>.
    <br />
    Translations: <a href="https://github.com/zenghongtu/react-use-chinese/blob/master/README.md">🇨🇳 汉语</a>
  </sup>
  <br />
  <br />
  <br />
  <br />
  <pre>npm i <a href="https://www.npmjs.com/package/react-use">react-use</a></pre>
  <br />
  <br />
  <br />
  <br />
  <br />
</div>

# 阅读有感

当前进度：406af205e37af2e16c20fa3f699287f5600a1c20

TypeScript 自带了 DOM 和 ESxxxx 的类型定义，可以在 node_modules/typescript/lib/ 下找到

## 常见 Pattern

### 使用 useMemo 确保尽可能返回 memorized value

好处：

1. callback function object id 唯一
2. expensive calc 无需每次 render 都重新计算

### 使用 useRef + useUpdate 代替 useState

疑问：why?  
猜测：首先 useRef 不会触发组件 re-render，而 useUpdate 强制组件 re-render（通过使用 useState），所以通过使用 useRef + useUpdate 的组合可以让组件 re-render 的行为变得人为可控。

**但是这么做有什么好处呢？** 我能想到的唯一好处就是多个 ref 变量修改时可以仅触发一次 re-render。

- [**Sensors**](./docs/Sensors.md)

  - :white_check_mark: [`useBattery`](./docs/useBattery.md) &mdash; tracks device battery state. [![][img-demo]](https://codesandbox.io/s/qlvn662zww)  
    获取设备实时电量信息
  - :white_check_mark: [`useGeolocation`](./docs/useGeolocation.md) &mdash; tracks geo location state of user's device. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-usegeolocation--demo)  
    获取设备实时地理位置信息
  - :white_check_mark: [`useHover` and `useHoverDirty`](./docs/useHover.md) &mdash; tracks mouse hover state of some element. [![][img-demo]](https://codesandbox.io/s/zpn583rvx)  
    获取鼠标当前是否悬停（hover）在当前组件上
  - [`useIdle`](./docs/useIdle.md) &mdash; tracks whether user is being inactive.
  - [`useIntersection`](./docs/useIntersection.md) &mdash; tracks an HTML element's intersection. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-useintersection--demo)
  - [`useKey`](./docs/useKey.md), [`useKeyPress`](./docs/useKeyPress.md), [`useKeyboardJs`](./docs/useKeyboardJs.md), and [`useKeyPressEvent`](./docs/useKeyPressEvent.md) &mdash; track keys. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-usekeypressevent--demo)
  - :white_check_mark: [`useLocation`](./docs/useLocation.md) and [`useSearchParam`](./docs/useSearchParam.md) &mdash; tracks page navigation bar location state.  
    获取浏览器地址栏内容和地址 History
  - [`useLongPress`](./docs/useLongPress.md) &mdash; tracks long press gesture of some element.
  - [`useMedia`](./docs/useMedia.md) &mdash; tracks state of a CSS media query. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-usemedia--demo)
  - [`useMediaDevices`](./docs/useMediaDevices.md) &mdash; tracks state of connected hardware devices.
  - [`useMotion`](./docs/useMotion.md) &mdash; tracks state of device's motion sensor.
  - [`useMouse` and `useMouseHovered`](./docs/useMouse.md) &mdash; tracks state of mouse position. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-usemouse--docs)
  - [`useNetwork`](./docs/useNetwork.md) &mdash; tracks state of user's internet connection.
  - [`useOrientation`](./docs/useOrientation.md) &mdash; tracks state of device's screen orientation.
  - [`usePageLeave`](./docs/usePageLeave.md) &mdash; triggers when mouse leaves page boundaries.
  - [`useScroll`](./docs/useScroll.md) &mdash; tracks an HTML element's scroll position. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-usescroll--docs)
  - [`useScrolling`](./docs/useScrolling.md) &mdash; tracks whether HTML element is scrolling.
  - :white_check_mark::thumbsup: [`useSize`](./docs/useSize.md) &mdash; tracks an HTML element's size.  
    获取元素实时大小（长宽）
    使用场景：

    1. 元素随窗口长、宽修改而自适应，如：block 元素的宽度
    2. 浏览器自身支持 zoom-in/out，此时也会影响 block 元素的宽度

    实现方式：

    1. 给 ReactElement 增加一个隐藏的 iframe 子节点
    2. 利用父节点的 position: relative 和子节点的 position: absolute + (top-0, left-0, height-100%, width 100%)，则子节点的 offsetHeight 和 offsetWidth 即等于父节点的 height 和 width

  - [`useStartTyping`](./docs/useStartTyping.md) &mdash; detects when user starts typing.
  - [`useWindowScroll`](./docs/useWindowScroll.md) &mdash; tracks `Window` scroll position. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-usewindowscroll--docs)
  - :white_check_mark: [`useWindowSize`](./docs/useWindowSize.md) &mdash; tracks `Window` dimensions. [![][img-demo]](https://codesandbox.io/s/m7ln22668)  
    监听 windonw.innerHeight/Width 的改变，并用 useRafState 进行了优化
  - :white_check_mark::thumbsup: [`useMeasure`](./docs/useMeasure.md) &mdash; tracks an HTML element's dimensions using the Resize Observer API.[![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-usemeasure--demo)  
    使用场景同 useSize  
    使用方式不同（useSize 是 Higher-Order Component，useMeasue 通过 ref 实现）  
    实现方式不同
  - [`createBreakpoint`](./docs/createBreakpoint.md) &mdash; tracks `innerWidth`
  - [`useScrollbarWidth`](./docs/useScrollbarWidth.md) &mdash; detects browser's native scrollbars width. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/sensors-usescrollbarwidth--demo)
    <br/>
    <br/>

- [**UI**](./docs/UI.md)
  - [`useAudio`](./docs/useAudio.md) &mdash; plays audio and exposes its controls. [![][img-demo]](https://codesandbox.io/s/2o4lo6rqy)
  - [`useClickAway`](./docs/useClickAway.md) &mdash; triggers callback when user clicks outside target area.
  - [`useCss`](./docs/useCss.md) &mdash; dynamically adjusts CSS.
  - [`useDrop` and `useDropArea`](./docs/useDrop.md) &mdash; tracks file, link and copy-paste drops.
  - [`useFullscreen`](./docs/useFullscreen.md) &mdash; display an element or video full-screen. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/ui-usefullscreen--demo)
  - [`useSlider`](./docs/useSlider.md) &mdash; provides slide behavior over any HTML element. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/ui-useslider--demo)
  - [`useSpeech`](./docs/useSpeech.md) &mdash; synthesizes speech from a text string. [![][img-demo]](https://codesandbox.io/s/n090mqz69m)
  - [`useVibrate`](./docs/useVibrate.md) &mdash; provide physical feedback using the [Vibration API](https://developer.mozilla.org/en-US/docs/Web/API/Vibration_API). [![][img-demo]](https://streamich.github.io/react-use/?path=/story/ui-usevibrate--demo)
  - [`useVideo`](./docs/useVideo.md) &mdash; plays video, tracks its state, and exposes playback controls. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/ui-usevideo--demo)
    <br/>
    <br/>
- [**Animations**](./docs/Animations.md)

  - [`useRaf`](./docs/useRaf.md) &mdash; re-renders component on each `requestAnimationFrame`.
  - [`useInterval`](./docs/useInterval.md) and [`useHarmonicIntervalFn`](./docs/useHarmonicIntervalFn.md) &mdash; re-renders component on a set interval using `setInterval`.
  - [`useSpring`](./docs/useSpring.md) &mdash; interpolates number over time according to spring dynamics.
  - [`useTimeout`](./docs/useTimeout.md) &mdash; re-renders component after a timeout.
  - [`useTimeoutFn`](./docs/useTimeoutFn.md) &mdash; calls given function after a timeout. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/animation-usetimeoutfn--demo)
  - [`useTween`](./docs/useTween.md) &mdash; re-renders component, while tweening a number from 0 to 1. [![][img-demo]](https://codesandbox.io/s/52990wwzyl)
  - :white_check_mark: [`useUpdate`](./docs/useUpdate.md) &mdash; returns a callback, which re-renders component when called.  
    强制触发组件更新

    使用场景：

    1. ref 作为类的成员变量使用时，其值的修改并不会触发组件更新，使用 useUpdate 可以强制触发组件更新
       <br/>
       <br/>

- [**Side-effects**](./docs/Side-effects.md)
  - [`useAsync`](./docs/useAsync.md), [`useAsyncFn`](./docs/useAsyncFn.md), and [`useAsyncRetry`](./docs/useAsyncRetry.md) &mdash; resolves an `async` function.
  - [`useBeforeUnload`](./docs/useBeforeUnload.md) &mdash; shows browser alert when user try to reload or close the page.
  - [`useCookie`](./docs/useCookie.md) &mdash; provides way to read, update and delete a cookie. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/side-effects-usecookie--demo)
  - [`useCopyToClipboard`](./docs/useCopyToClipboard.md) &mdash; copies text to clipboard.
  - [`useDebounce`](./docs/useDebounce.md) &mdash; debounces a function. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/side-effects-usedebounce--demo)
  - [`useError`](./docs/useError.md) &mdash; error dispatcher. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/side-effects-useerror--demo)
  - [`useFavicon`](./docs/useFavicon.md) &mdash; sets favicon of the page.
  - [`useLocalStorage`](./docs/useLocalStorage.md) &mdash; manages a value in `localStorage`.
  - [`useLockBodyScroll`](./docs/useLockBodyScroll.md) &mdash; lock scrolling of the body element.
  - [`useRafLoop`](./docs/useRafLoop.md) &mdash; calls given function inside the RAF loop.
  - [`useSessionStorage`](./docs/useSessionStorage.md) &mdash; manages a value in `sessionStorage`.
  - [`useThrottle` and `useThrottleFn`](./docs/useThrottle.md) &mdash; throttles a function. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/side-effects-usethrottle--demo)
  - :white_check_mark: [`useTitle`](./docs/useTitle.md) &mdash; sets title of the page.  
    更新 page title
  - [`usePermission`](./docs/usePermission.md) &mdash; query permission status for browser APIs.
    <br/>
    <br/>
- [**Lifecycles**](./docs/Lifecycles.md)
  - :white_check_mark: [`useEffectOnce`](./docs/useEffectOnce.md) &mdash; a modified [`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect) hook that only runs once.  
    useEffect 的语义级封装
  - [`useEvent`](./docs/useEvent.md) &mdash; subscribe to events.
  - :white_check_mark: [`useLifecycles`](./docs/useLifecycles.md) &mdash; calls `mount` and `unmount` callbacks.  
    useEffect 的语义级封装
  - [`useMountedState`](./docs/useMountedState.md) and [`useUnmountPromise`](./docs/useUnmountPromise.md) &mdash; track if component is mounted.
  - [`usePromise`](./docs/usePromise.md) &mdash; resolves promise only while component is mounted.
  - [`useLogger`](./docs/useLogger.md) &mdash; logs in console as component goes through life-cycles.
  - :white_check_mark: [`useMount`](./docs/useMount.md) &mdash; calls `mount` callbacks.  
    useEffect 的语义级封装
  - :white_check_mark: [`useUnmount`](./docs/useUnmount.md) &mdash; calls `unmount` callbacks.  
    useEffect 的语义级封装
  - :white_check_mark: [`useUpdateEffect`](./docs/useUpdateEffect.md) &mdash; run an `effect` only on updates.  
    useEffect 的语义级封装。仅当 update 时触发的 effect，mount/unmount 时均不触发
  - [`useIsomorphicLayoutEffect`](./docs/useIsomorphicLayoutEffect.md) &mdash; `useLayoutEffect` that does not show warning when server-side rendering.
  - [`useDeepCompareEffect`](./docs/useDeepCompareEffect.md), [`useShallowCompareEffect`](./docs/useShallowCompareEffect.md), and [`useCustomCompareEffect`](./docs/useCustomCompareEffect.md) &mdash; run an `effect` depending on deep comparison of its dependencies
    <br/>
    <br/>
- [**State**](./docs/State.md)
  - [`createMemo`](./docs/createMemo.md) &mdash; factory of memoized hooks.
  - :white_check_mark::thumbsup: [`createReducer`](./docs/createReducer.md) &mdash; factory of reducer hooks with custom middleware.  
    可以给 local reducer 添加 middleware  
    :question: 代码还没有完全看懂消化
  - [`createReducerContext`](./docs/createReducerContext.md) and [`createStateContext`](./docs/createStateContext.md) &mdash; factory of hooks for a sharing state between components.
  - [`useDefault`](./docs/useDefault.md) &mdash; returns the default value when state is `null` or `undefined`.
  - :white_check_mark: [`useGetSet`](./docs/useGetSet.md) &mdash; returns state getter `get()` instead of raw state.  
    为一个变量增加 getter and setter
  - [`useGetSetState`](./docs/useGetSetState.md) &mdash; as if [`useGetSet`](./docs/useGetSet.md) and [`useSetState`](./docs/useSetState.md) had a baby.
  - [`usePrevious`](./docs/usePrevious.md) &mdash; returns the previous state or props. [![][img-demo]](https://codesandbox.io/s/fervent-galileo-krgx6)
  - [`usePreviousDistinct`](./docs/usePreviousDistinct.md) &mdash; like `usePrevious` but with a predicate to determine if `previous` should update.
  - [`useObservable`](./docs/useObservable.md) &mdash; tracks latest value of an `Observable`.
  - :white_check_mark: [`useRafState`](./docs/useRafState.md) &mdash; creates `setState` method which only updates after `requestAnimationFrame`. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-userafstate--demo)  
    使用 requestAnimationFrame 对 setState 进行优化。  
    使用场景：对高频更新事件的监听，如：windon.resize
  - [`useSetState`](./docs/useSetState.md) &mdash; creates `setState` method which works like `this.setState`. [![][img-demo]](https://codesandbox.io/s/n75zqn1xp0)
  - [`useStateList`](./docs/useStateList.md) &mdash; circularly iterates over an array. [![][img-demo]](https://codesandbox.io/s/bold-dewdney-pjzkd)
  - :white_check_mark: [`useToggle` and `useBoolean`](./docs/useToggle.md) &mdash; tracks state of a boolean. [![][img-demo]](https://codesandbox.io/s/focused-sammet-brw2d)  
    对单个布尔变量及其操作的封装。
  - :white_check_mark: [`useCounter` and `useNumber`](./docs/useCounter.md) &mdash; tracks state of a number. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-usecounter--demo)  
    对 Counter 类数值变量及其操作的封装
  - :white_check_mark: [`useList`](./docs/useList.md) ~and [`useUpsert`](./docs/useUpsert.md)~ &mdash; tracks state of an array. [![][img-demo]](https://codesandbox.io/s/wonderful-mahavira-1sm0w)  
    对 List 类型数据及其操作的封装
  - :white_check_mark: [`useMap`](./docs/useMap.md) &mdash; tracks state of an object. [![][img-demo]](https://codesandbox.io/s/quirky-dewdney-gi161)  
    对 Map 类型数据及其操作的封装
  - [`useSet`](./docs/useSet.md) &mdash; tracks state of a Set. [![][img-demo]](https://codesandbox.io/s/bold-shtern-6jlgw)
  - [`useQueue`](./docs/useQueue.md) &mdash; implements simple queue.
  - [`useStateValidator`](./docs/useStateValidator.md) &mdash; tracks state of an object. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-usestatevalidator--demo)
  - [`useStateWithHistory`](./docs/useStateWithHistory.md) &mdash; stores previous state values and provides handles to travel through them. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-usestatewithhistory--demo)
  - [`useMultiStateValidator`](./docs/useMultiStateValidator.md) &mdash; alike the `useStateValidator`, but tracks multiple states at a time. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-usemultistatevalidator--demo)
  - [`useMediatedState`](./docs/useMediatedState.md) &mdash; like the regular `useState` but with mediation by custom function. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-usemediatedstate--demo)
  - [`useFirstMountState`](./docs/useFirstMountState.md) &mdash; check if current render is first. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-usefirstmountstate--demo)
  - [`useRendersCount`](./docs/useRendersCount.md) &mdash; count component renders. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-userenderscount--demo)
  - [`createGlobalState`](./docs/createGlobalState.md) &mdash; cross component shared state.[![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-createglobalstate--demo)
  - [`useMethods`](./docs/useMethods.md) &mdash; neat alternative to `useReducer`. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-usemethods--demo)
    <br/>
    <br/>
- [**Miscellaneous**]()
  - [`useEnsuredForwardedRef`](./docs/useEnsuredForwardedRef.md) and [`ensuredForwardRef`](./docs/useEnsuredForwardedRef.md) &mdash; use a React.forwardedRef safely. [![][img-demo]](https://streamich.github.io/react-use/?path=/story/state-useensuredforwardedref--demo)

<br />
<br />
<br />
<br />
<br />
<br />
<br />

<p align="center">
  <a href="./docs/Usage.md"><strong>Usage</strong></a> &mdash; how to import.
  <br />
  <a href="./LICENSE"><strong>Unlicense</strong></a> &mdash; public domain.
  <br />
  <a href="https://opencollective.com/react-use/contribute"><strong>Support</strong></a> &mdash; add yourself to backer list below.
</p>

<br />
<br />
<br />
<br />
<br />

[img-demo]: https://img.shields.io/badge/demo-%20%20%20%F0%9F%9A%80-green.svg

<div align="center">
  <h1>Contributors</h1>
</div>

<br />
<br />

<a href="https://github.com/streamich/react-use/graphs/contributors"><img src="https://opencollective.com/react-use/contributors.svg?width=890&button=false" /></a>

<br />
<br />
<br />
<br />
<br />
