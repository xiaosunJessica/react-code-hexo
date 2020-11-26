---
title: fiber结构分析
date: 2020-11-26 13:30:44
---
<html>
    <table style="margin-left: auto; margin-right: auto;">
        <tr>
            <td>
                <!--左侧内容-->
                左侧
            </td>
            <td>
                <!--右侧内容-->
                export type Fiber = { 
                  // Tag identifying the type of fiber.
                  // 主要是用于标记fiber元素类型，FunctionComponent=0/ClassComponent=1/IndeterminateComponent=2/HostRoot=3
                  // 详细见文件ReactWorkTags
                  tag: WorkTag,

                  // Unique identifier of this child.
                  // 唯一性标志，和jsx里的key一样
                  key: null | string,

                  // The value of element.type which is used to preserve the identity during
                  // reconciliation of this child.
                  // 一般是虚拟DOM的type值
                  elementType: any,

                  // The resolved function/class/ associated with this fiber.
                  type: any,

                  // The local state associated with this fiber.
                  // stateNode记录当前fiber, 在completeWork执行完成后，记录是的浏览器的DOM节点
                  stateNode: any,

                  // 作为链表结构中的一环，它返回的是父节点parentFiber
                  return: Fiber | null,

                  // 作为链表结构中的一环，它返回的是子节点的第一个child
                  child: Fiber | null,

                  // 作为链表结构中的一环，它返回的是兄弟节点
                  sibling: Fiber | null,
                  // 在reconcileChild的过程中，记录第几个子元素有用到
                  index: number,

                  // 同jsx的ref
                  ref: null | (((handle: mixed) => void) & {_stringRef: ?string}) | RefObject,

                  // 此次更新中的props
                  pendingProps: any, 
                  // 上次更新的props
                  memoizedProps: any, 

                  // A queue of state updates and callbacks.
                  // 更新的update
                  updateQueue: UpdateQueue<any> | null,

                  // 上次更新的state
                  memoizedState: any,

                  // Dependencies (contexts, events) for this fiber, if it has any
                  // 依赖的上下文和事件
                  dependencies: Dependencies | null,

                  // Bitfield that describes properties about the fiber and its subtree. E.g.
                  // the ConcurrentMode flag indicates whether the subtree should be async-by-
                  // default. When a fiber is created, it inherits the mode of its
                  // parent. Additional flags can be set at creation time, but after that the
                  // value should remain unchanged throughout the fiber's lifetime, particularly
                  // before its child fibers are created.
                  // legacy noMode /concurrent/ StrictMode /ProfileMode/BatchedMode
                  mode: TypeOfMode,

                  // Effect
                  effectTag: SideEffectTag,

                  // Singly linked list fast path to the next fiber with side-effects.
                  nextEffect: Fiber | null,

                  // The first and last fiber with side-effect within this subtree. This allows
                  // us to reuse a slice of the linked list when we reuse the work done within
                  // this fiber.
                  firstEffect: Fiber | null,
                  lastEffect: Fiber | null,

                  // Represents a time in the future by which this work should be completed.
                  // Does not include work found in its subtree.
                  expirationTime: ExpirationTime,

                  // This is used to quickly determine if a subtree has no pending changes.
                  childExpirationTime: ExpirationTime,

                  // This is a pooled version of a Fiber. Every fiber that gets updated will
                  // eventually have a pair. There are cases when we can clean up pairs to save
                  // memory if we need to.
                  alternate: Fiber | null,

                  // Time spent rendering this Fiber and its descendants for the current update.
                  // This tells us how well the tree makes use of sCU for memoization.
                  // It is reset to 0 each time we render and only updated when we don't bailout.
                  // This field is only set when the enableProfilerTimer flag is enabled.
                  actualDuration?: number,

                  // If the Fiber is currently active in the "render" phase,
                  // This marks the time at which the work began.
                  // This field is only set when the enableProfilerTimer flag is enabled.
                  actualStartTime?: number,

                  // Duration of the most recent render time for this Fiber.
                  // This value is not updated when we bailout for memoization purposes.
                  // This field is only set when the enableProfilerTimer flag is enabled.
                  selfBaseDuration?: number,

                  // Sum of base times for all descendants of this Fiber.
                  // This value bubbles up during the "complete" phase.
                  // This field is only set when the enableProfilerTimer flag is enabled.
                  treeBaseDuration?: number,

                  // Conceptual aliases
                  // workInProgress : Fiber ->  alternate The alternate used for reuse happens
                  // to be the same as work in progress.
                  // __DEV__ only
                  _debugID?: number,
                  _debugSource?: Source | null,
                  _debugOwner?: Fiber | null,
                  _debugIsCurrentlyTiming?: boolean,
                  _debugNeedsRemount?: boolean,

                  // Used to verify that the order of hooks does not change between renders.
                  _debugHookTypes?: Array<HookType> | null,
                |};
            </td>
        </tr>
    </table>
</html>

