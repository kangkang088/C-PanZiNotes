# 【唐老狮】Unity程序基础框架

2023年6月7日，盘子ssa，QQ2426966358

# 任务2：单例模式基类模块

为了方便我们使用单例，不重复写单例类代码，我们可以写一个单例基类，其他类只需要继承此类，即可成为单例。

## BaseManager.cs

普通单例模式基类，懒汉式。由于Unity基本上都是单线程，所以我们可以不加双重判断。

使用泛型，约束T可以new。要成为单例，只需要继承此类，然后将T写成自己即可。

注意：这里不用将构造函数设为私有，否则子类无法访问

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
//**********************************
//创建人：
//功能说明：普通单例基类（懒汉式）
//**********************************

public class BaseManager<T> where T : new()
{
    private static T _instance;

    public static T Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = new T();
            }
            return _instance;
        }
    }
    
}
```

# 任务3：继承MonoBehaviour的单例模式基类

## SingletonMono.cs

Mono单例基类，由于可能存在需要挂载到游戏对象上的单例，所以我们写一个Mono的单例基类。

使用泛型，约束T继承Mono，在Awake初始化自己。由于可能在子类当中的Awake做一些事，所以需要将Awake设为protected和virtual。

要成为Mono单例，只需要继承此类，然后将T写成本类型即可。

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
//**********************************
//创建人：
//功能说明：Mono单例
//**********************************
public class SingletonMono<T> : MonoBehaviour where T : MonoBehaviour
{
    private static T _instance;
    public static T Instance
    {
        get
        {
            return _instance;
        }
    }

    protected virtual void Awake()
    {
        _instance = this as T;
    }
}
```

## SingletonAutoMono.cs

自动Mono单例类，我们只需要调用到这个类，就会自动在场景当中创建一个物体（切换场景不销毁），然后挂载到它上面。

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
//**********************************
//创建人：
//功能说明：自动Mono单例
//**********************************

public class SingletonAutoMono<T> : MonoBehaviour where T : MonoBehaviour
{
    private static T _instance;
    public static T Instance
    {
        get
        {
            if (_instance == null)
            {
                GameObject obj = new GameObject();
                obj.name = typeof(T).Name;
                _instance = obj.AddComponent<T>();
                GameObject.DontDestroyOnLoad(obj);
            }
            return _instance;
        }
    }

    protected virtual void Awake()
    {
        _instance = this as T;
    }
}
```

# 任务4：缓存池模块基础

> [对象池(Object Pool) - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/108538606)

对象池，在Unity当中，就是利用SetActive，激活失活对象，减少实例化新对象带来的GC和性能消耗。重复利用之前已经存在的对象，通过重置属性和字段，达到重置对象的效果。

# 任务5：缓存池模块优化

为了方便的管理我们的对象池对象，当存在多个对象池时，上一个课程的代码无法处理。

所以，我们设计一个数据结构 `PoolData`（其实就是子对象池），存储每一个预制体对应的对象池。

PoolMgr当中存取对象的方法，交由PoolData实现。

又为了更好的在场景当中管理，我们设定一个father，作为其在场景当中的父节点。

```C#
using System.Collections;
using System.Collections.Generic;
using System.Xml.Linq;
using UnityEditor.Experimental.GraphView;
using UnityEngine;
//**********************************
//创建人：
//功能说明：对象池管理类
//**********************************

/// <summary>
/// 对象池数据（子对象池）
/// </summary>
public class PoolData
{
    //对象挂载的父节点
    public GameObject fatherObj;
    //对象的容器
    public List<GameObject> poolList;
    
    
    public PoolData(GameObject obj, GameObject poolObj)
    {
        //创建一个新对象，为此对象池对象的父对象
        fatherObj = new GameObject(obj.name);
        fatherObj.transform.SetParent(poolObj.transform);
        //创建容器并将对象放进容器
        poolList = new List<GameObject>();
        PushObj(obj);
    }

    //往抽屉里面压东西
    public void PushObj(GameObject obj)
    {
        //失活
        obj.SetActive(false);
        //放入容器
        poolList.Add(obj);
        //设置父对象
        obj.transform.SetParent(fatherObj.transform);

    }

    public GameObject GetObj()
    {
        GameObject obj = null;
        //却出第一个
        obj = poolList[0];
        //从列表当中移除
        poolList.RemoveAt(0);
        //失活
        obj.SetActive(true);
        //设置父对象为空
        obj.transform.SetParent(null);
        return obj;
    }
}

public class PoolMgr : BaseManager<PoolMgr>
{
    public Dictionary<string, PoolData> poolDic = new Dictionary<string, PoolData>();

    private GameObject poolObj;
    
    /// <summary>
    /// 从对象池获取对象
    /// </summary>
    /// <param name="name"></param>
    /// <returns></returns>
    public GameObject GetObj(string name)
    {
        
        GameObject obj = null;
        //如果字典内存在此对象的对象池，并且对象池不为空
        if (poolDic.ContainsKey(name) && poolDic[name].poolList.Count > 0)
        {
            //为了方便，我们直接获取第一个
            obj = poolDic[name].GetObj();
        }
        else
        {
            //如果没有此对象，那么，我们创建一个
            obj = GameObject.Instantiate(Resources.Load<GameObject>(name));
            //将新创建的对象的名字，变成和传递的名字一致，方便放回对象池
            obj.name = name;
        }
        return obj;
    }

    /// <summary>
    /// 返回给对象池对象
    /// </summary>
    public void PushObj(string name, GameObject obj)
    {
        if (poolObj == null)
        {
            poolObj = new GameObject("Pool");
        }

        if (poolDic.ContainsKey(name))
        {
            poolDic[name].PushObj(obj);
        }
        else
        {
            poolDic.Add(name, new PoolData(obj, poolObj));
        }
    }

    /// <summary>
    /// 清空缓存池方法，主要用在切换场景
    /// </summary>
    public void Clear()
    {
        poolDic.Clear();
        poolObj = null;
    }
}

```

# 任务6：事件中心模块

使用委托、字典、观察者模式，实现事件中心模块。

事件中心模块，是为了实现当场景当中有一个物体发生事件，其他多个物体需要响应其行为。

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Events;
//**********************************
//创建人：
//功能说明：
//**********************************

/// <summary>
/// 事件中心，单例模式对象
/// 1.Dictionary
/// 2.委托
/// 3.观察者设计模式
/// </summary>
public class EventCenter : BaseManager<EventCenter>
{
    //key：事件的名字（比如：怪物死亡，玩家死亡，通关等等）  
    //value：监听的事件
    private Dictionary<string, UnityAction<object>> eventDic = new Dictionary<string, UnityAction<object>>();


    /// <summary>
    /// 添加事件监听  
    /// </summary>
    /// <param name="name">事件名</param>
    /// <param name="action">处理事件的委托函数</param>
    public void AddEventListener(string name, UnityAction<object> action) {

        //有没有对应的事件监听
        //有
        if (eventDic.ContainsKey(name))
        {
            eventDic[name] += action;
        }
        //没有
        else
        {
            eventDic.Add(name, action);
        }
    }

    /// <summary>
    /// 移除对应事件监听
    /// </summary>
    /// <param name="name">事件名</param>
    /// <param name="action">对应的委托函数</param>
    public void RemoveEventListener(string name, UnityAction<object> action)
    {
        if (eventDic.ContainsKey(name))
        {
            eventDic[name] -= action;
        }
    }

    /// <summary>
    /// 事件触发
    /// </summary>
    /// <param name="name">哪一个名字的事件触发了</param>
    public void EventTrigger(string name, object data)
    {
        //只有当有人关心此事件时，才执行此事件对应的委托函数
        if (eventDic.ContainsKey(name))
        {
            eventDic[name].Invoke(data);
        }
    }

    /// <summary>
    /// 清空事件，主要用在
    /// </summary>
    public void Clear()
    {
        eventDic.Clear();
    }

}
```

# 任务7：公共Mono模块

## 为什么需要Mono公共模块？

1. 有时候，我们需要不是Mono的类也开启Unity的回调函数。
2. 我们希望不是Mono的类也可以开启协程。
3. 不想要场景上物体脚本上的Update过多（由于调用Update是通过反射，这会造成性能消耗）。
4. 我们希望控制物体的Update的调用顺序。

## 代码

主要是通过一个Mono单例，间接的使用Mono类的功能

> 注意：不能通过函数名开启不是Mono类的协程函数
>
> 进阶：设定一个计时器，实现Invoke延时调用函数

```C#
using System.Collections;
using System.Collections.Generic;
using System.ComponentModel;
using UnityEngine;
using UnityEngine.Events;
//**********************************
//创建人：
//功能说明：
//**********************************



/// <summary>
/// 1.可以提供给外部添加更新事件的方法
/// 2.可以提供给外部添加添加协程的方法
/// </summary>
public class MonoMgr : BaseManager<MonoMgr>
{
    private MonoController controller;

    public MonoMgr()
    {
        //保证了Mono对象的唯一性
        GameObject obj = new GameObject("MonoController");
        controller = obj.AddComponent<MonoController>();
    }

    /// <summary>
    /// 给外部提供的添加帧事件的函数
    /// </summary>
    /// <param name="fun"></param>
    public void AddUpdateListener(UnityAction fun)
    {
        controller.AddUpdateListener(fun);

        
    }

    /// <summary>
    /// 提供给外部，移除帧事件的函数
    /// </summary>
    /// <param name="fun"></param>
    public void RemoveUpdateListener(UnityAction fun)
    {
        controller.RemoveUpdateListener(fun);
    }

    //注意：不能使用函数名开启外部的类协程
    public void StartCoroutine(string methodName)
    {
        controller.StartCoroutine(methodName);
    }

    //注意：不能使用函数名开启外部的类协程
    public void StartCoroutine(string methodName, [DefaultValue("null")] object value)
    {
        controller.StartCoroutine(methodName, value);   
    }

    public void StartCoroutine(IEnumerator routine)
    {
        controller.StartCoroutine(routine);
    }
}
```

# 任务8：场景切换模块

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Events;
using UnityEngine.SceneManagement;
//**********************************
//创建人：
//功能说明：
//**********************************


/// <summary>
/// 场景切换模块
/// 知识点
/// 1、场景异步加载
/// 2、协程
/// 3、委托
/// </summary>
public class ScenesMgr : BaseManager<ScenesMgr>
{

    /// <summary>
    /// 切换场景，同步
    /// </summary>
    /// <param name="name"></param>
    public void LoadScene(string name, UnityAction action)
    {
        SceneManager.LoadScene(name);
        action();
    }

    /// <summary>
    /// 异步加载场景
    /// </summary>
    /// <param name="name"></param>
    /// <param name="callBack"></param>
    public void LoadScneAsyn(string name, UnityAction callBack)
    {
        MonoMgr.Instance.StartCoroutine(ReallyLoadSceneAsyn(name, callBack));
    }

    /// <summary>
    /// 协程异步加载场景
    /// </summary>
    /// <param name="name"></param>
    /// <param name="callBack"></param>
    /// <returns></returns>
    private IEnumerator ReallyLoadSceneAsyn(string name, UnityAction callBack)
    {
        AsyncOperation ao = SceneManager.LoadSceneAsync(name);
        //循环判断是否加载完成j
        while (!ao.isDone)
        {
            //事件中心，向外分发进度情况，想用就用
            EventCenter.Instance.EventTrigger("进度条更新", ao.progress);
            //这里面去更新进度条
            yield return ao.progress;
        }
        //加载完成后，执行回调函数
        callBack();
    }
}
```

