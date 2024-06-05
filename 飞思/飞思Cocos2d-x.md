# Cocos2d-x

# 创建工程

```Cpp
//in cmd
cocos new ProjectName -l language -p packageName -d savePath 
//cocos new 工程名 -l 语言 -p 域名（公司名） -d 保存路径 
```

# 工程结构

1. Classes：类文件夹
2. Resources：资源文件夹
3. cocos2d：引擎源码
4. proj.xxx：特定平台文件

# 核心概念

## Director（导演）

用于管理场景对象，是一个单例

职责：

1. 访问和修改场景
2. 访问cocos2d-x的配置信息
3. 暂停，继续和停止游戏
4. 转换坐标

## Scene（场景）

构成游戏的界面，类似于电影的场景

## Layer（层）

类似Photoshop图层

## Sprite（精灵）

图片操作

# 主函数

```C#
#include "main.h"
#include "AppDelegate.h"
#include "cocos2d.h"

USING_NS_CC;

int APIENTRY _tWinMain(HINSTANCE hInstance,
                       HINSTANCE hPrevInstance,
                       LPTSTR    lpCmdLine,
                       int       nCmdShow)
{
    UNREFERENCED_PARAMETER(hPrevInstance);
    UNREFERENCED_PARAMETER(lpCmdLine);

    // 创建应用实例
    AppDelegate app;
    return Application::getInstance()->run();
}

```

# AppDelegate类

App委托类，入口类，是一个单例。

私有继承Application类

```Cpp
class  AppDelegate : private cocos2d::Application
{
public:
	// 构造
    AppDelegate();
	// 析构
    virtual ~AppDelegate();

	// 初始化OpenGL
    virtual void initGLContextAttrs();
	// 应用程序完成加载
    virtual bool applicationDidFinishLaunching();
	// 进入后台（暂停游戏，音乐音效暂停）
    virtual void applicationDidEnterBackground();
	// 回到游戏（恢复游戏，恢复音乐音效）
    virtual void applicationWillEnterForeground();
};
```

## applicationDidFinishLaunching

游戏后动时调用的函数﹐在这里初始化游戏信息·导演对象和运行第一个场景对象

```Cpp
bool AppDelegate::applicationDidFinishLaunching() {
    // 初始化导演
	Director* director = Director::getInstance();
	// 通过导演类对象获取GLView*对象
	GLView* glview = director->getOpenGLView();

    if(!glview) {
#if (CC_TARGET_PLATFORM == CC_PLATFORM_WIN32) || (CC_TARGET_PLATFORM == CC_PLATFORM_MAC) || (CC_TARGET_PLATFORM == CC_PLATFORM_LINUX)
        glview = GLViewImpl::createWithRect("Game", Rect(0, 0, designResolutionSize.width, designResolutionSize.height));
#else  //移动端代码
        glview = GLViewImpl::create("helloworld");
#endif
		// 设置给导演对象
        director->setOpenGLView(glview);
    }

    // 是否显示FPS信息
    director->setDisplayStats(true);

    // 修改FPS.一般不允许修改。耗电量 、手机发热
    director->setAnimationInterval(1.0 / 60);

    // Set the design resolution
	// 设置设计分辨率
    glview->setDesignResolutionSize(designResolutionSize.width, designResolutionSize.height, ResolutionPolicy::NO_BORDER);

	// 实际分辨率和对比分辨率进行比较，实现内容自动缩放
    //Size frameSize = glview->getFrameSize();
    //// if the frame's height is larger than the height of medium size.
    //if (frameSize.height > mediumResolutionSize.height)
    //{        
    //    director->setContentScaleFactor(MIN(largeResolutionSize.height/designResolutionSize.height, largeResolutionSize.width/designResolutionSize.width));
    //}
    //// if the frame's height is larger than the height of small size.
    //else if (frameSize.height > smallResolutionSize.height)
    //{        
    //    director->setContentScaleFactor(MIN(mediumResolutionSize.height/designResolutionSize.height, mediumResolutionSize.width/designResolutionSize.width));
    //}
    //// if the frame's height is smaller than the height of medium size.
    //else
    //{        
    //    director->setContentScaleFactor(MIN(smallResolutionSize.height/designResolutionSize.height, smallResolutionSize.width/designResolutionSize.width));
    //}

    register_all_packages();

    // 创建场景，这是一个自动释放对象
    //auto scene = HelloWorld::createScene();
	LogoScene* scene = LogoScene::create();
    // 导演执行场景
    director->runWithScene(scene);

    return true;
}
```

## ResolutionSize

分辨率

```C#
// 设计分辨率
static cocos2d::Size designResolutionSize = cocos2d::Size(854, 480);
// 对比分辨率
static cocos2d::Size smallResolutionSize = cocos2d::Size(480, 320);
static cocos2d::Size mediumResolutionSize = cocos2d::Size(1024, 768);
static cocos2d::Size largeResolutionSize = cocos2d::Size(2048, 1536);
```

## applicationDidEnterBackground

游戏进入后台时调用的函数﹐比如暂停游戏背景音乐

```Cpp
// 进入到后台
void AppDelegate::applicationDidEnterBackground() {
	// 导演停止动画
    Director::getInstance()->stopAnimation();

    // if you use SimpleAudioEngine, it must be pause  如果使用了声音引擎，就必须要暂停
    // SimpleAudioEngine::getInstance()->pauseBackgroundMusic();
}
```

## applicationWillEnterForeground

游戏进入前台时调用的函数﹐比如恢复背景音乐

```Cpp
// 激活游戏，回到前台
void AppDelegate::applicationWillEnterForeground() {
    Director::getInstance()->startAnimation();

    // if you use SimpleAudioEngine, it must resume here
    // SimpleAudioEngine::getInstance()->resumeBackgroundMusic();
}
```

# xxScene场景类

```C#
Scene* HelloWorld::createScene()
{
    // 'scene' is an autorelease object
    auto scene = Scene::create();
    
    // 'layer' is an autorelease object
    auto layer = HelloWorld::create();

    // add layer as a child to scene
    scene->addChild(layer);

    // return the scene
    return scene;
}
```

# 二段构建对象-创建场景

过程：书写二段构建场景类->applicationDidFinishLaunching中调用create函数->导演执行场景

一段：create创建对象分配对象；

二段：init函数初始化对象。

```Cpp
#include "cocos2d.h"

using namespace cocos2d;

//声明场景类
class LogoScene : public Scene {
public:
    static LogoScene* create();
    virtual bool init() override;
}
```

```Cpp
LogoScene* LogoScene::create() {
	//分配内存
	LogoScene* pScene = new LogoScene;
	//如果分配内存成功并init成功
	if (pScene && pScene->init()) {
		//加入到自动释放池
		pScene->autorelease();
	}
	else {
		delete pScene;
		pScene = nullptr;
	}
	return pScene;
}
```

```Cpp
bool* LogoScene::init() {
	//先初始化父类Scene对象
	if (!Scene::init()) {
		return false;
	}
    //初始化当前场景
    //画一张图片，先创建一张图片
	Sprite* spLogo = Sprite::create("fslogo.png");
    //然后将这张图片作为当前场景的子节点。
	this->addChild(spLogo);
    return true;
}
```

# OpenGL坐标系

也是cocos坐标系，原点（0,0）在左下角，x轴正上方向右，y轴正上方向上。

# Sprite锚点

锚点：就是对于坐标系的偏移点

锚点采用比例设置，默认在图片中心（0.5,0.5）

# Sprite方法

1. setPosition（设置坐标）
2. setAnchorPoint（设置锚点）

# Action动作

移动到，以世界坐标为准

```C#
MoveBy* move = MoveBy::create(3.0f, Vec2(100, 0));
wind->runAction(move);
```

# 2023年3月28日

# 实现背景图轮转

# 调度器

- 默认调度器（帧调度器）：scheduleUpdate()
- 自定义调度器
- 单次调度器：scheduleOnce()

## scheduleUpdate()

> [Cocos2d-x: Node Class Reference](https://docs.cocos2d-x.org/api-ref/cplusplus/V3.9/d3/d82/classcocos2d_1_1_node.html#abf28eebecc59de9221838deedd2a7451)
>
> 其实就是Unity当中的Update

帧调度器，使用此方法，将会在每帧都调用`update(float dt)`方法

使用此方法，需要在场景当中重写`update(float dt)`方法

```Cpp
//init方法当中调用一次即可
this->scheduleUpdate();

void _3_28_Scene::update(float dt) {
	static int n = 0;
	log("n = %d dt = %f", n++, dt);
}
```

## schedule()

> [Cocos2d-x: Node Class Reference](https://docs.cocos2d-x.org/api-ref/cplusplus/V3.9/d3/d82/classcocos2d_1_1_node.html#a1fa0df52e790f26ad723af12229dbd8e)

自定义调度器（其实就是Unity当中的Invoke）

```Cpp
void Node::schedule(const std::function<void(float)>& callback, float interval, unsigned int repeat, float delay, const std::string &key)
```

- callback：调用的函数，参数为deltaTIme（帧间隔时间），调用时自动传入
- interval：调用callback的间隔时间
- repeat：重复次数
- delay：初始时，延迟多少秒才开始调用
- key：给这一次调度定义一个Key（是一个string，就是给定一个名字）

```Cpp
this->schedule([](float dt) {
		static int n = 0;
		log("n = %d dt = %f", n++, dt);
	}, 3.0f, -1, 0.1f, "Custom Schedule");
```

## 实现图片轮转

```cpp
void _3_28_Scene::update(float dt) {
	moveBg(dt);
}

void _3_28_Scene::moveBg(float dt) {
	moveBgUseSpeed(dt, ltyj1, ltyjMoveSpeed);
	moveBgUseSpeed(dt, ltyj2, ltyjMoveSpeed);
	moveBgUseSpeed(dt, ltzj1, ltzjMoveSpeed);
	moveBgUseSpeed(dt, ltzj2, ltzjMoveSpeed);
}

void _3_28_Scene::moveBgUseSpeed(float dt, Sprite* sprite, float speed) {
	Size winSize = Director::getInstance()->getWinSize();
	//s = v * t
	float s = speed * dt;
	//移动图片
	sprite->setPosition(sprite->getPosition() - Vec2(s, 0));
	if (sprite->getPosition().x < 0) {
		sprite->setPosition(Vec2(winSize.width * 2 + sprite->getPosition().x, ltyj1->getPosition().y));
	}
}
```

# 2023年3月29日

# 事件监听器

> [事件分发机制 · GitBook (cocos.com)](https://docs.cocos.com/cocos2d-x/manual/zh/event_dispatcher/)

# 1创建触摸监听器并设置对应函数

```C#
//创建监听器
EventListenerTouchOneByOne* touchListener = EventListenerTouchOneByOne::create();
//开始触摸
touchListener->onTouchBegan = [this](Touch* touch, Event* event) {
    //获取触摸点
    Vec2 touchPos = touch->getLocation();	//第一象限
    log("x = %f, y = %f", touchPos.x, touchPos.y);
    Size playerSize = this->player->getContentSize();

    //判断坐标是否在角色坐标内，在这设置为可移动
    if (touchPos.x >= (player->getPosition().x - playerSize.width / 2)
        && touchPos.y >= (player->getPosition().y - playerSize.height / 2)
        && touchPos.x <= (player->getPosition().x + playerSize.width / 2)
        && touchPos.y <= (player->getPosition().y + playerSize.height / 2)) {
        this->playerSelected = true;
    }
    return true;
};

//触摸移动
touchListener->onTouchMoved = [this](Touch* touch, Event* event) {
    Vec2 touchPos = touch->getLocation();	//第一象限
    log("x = %f, y = %f", touchPos.x, touchPos.y);
    if (this->playerSelected) {
        this->player->setPosition(touchPos);
    }
    Rect playerRect = this->player->getTextureRect();
    log("px = %f, py = %f", playerRect.origin.x, playerRect.origin.y);
};

//触摸结束
touchListener->onTouchEnded = [this](Touch* touch, Event* event) {
    this->playerSelected = false;
};
```

# 2添加到事件分发器

```C#
//获取时间监听器
EventDispatcher* dispatcher = Director::getInstance()->getEventDispatcher();
//添加事件
//一般来说，通过渲染优先级添加事件
dispatcher->addEventListenerWithSceneGraphPriority(touchListener, this);
//通过自定义优先级添加事件
//dispatcher->addEventListenerWithFixedPriority(touchListener, 10);
```

# 2023年4月4日

# 获取角色矩形

```C#
Rect Node::getBoundingBox() const { ... }
```

使用矩形的containsPoint方法判断触摸点是否在矩形内。

```Cpp
//获取角色绑定盒
Rect boundingBox = this->player->getBoundingBox();
//判断是否在触摸点内
if (boundingBox.containsPoint(touchPos)) {
    this->playerSelected = true;
}
```

# 获取
