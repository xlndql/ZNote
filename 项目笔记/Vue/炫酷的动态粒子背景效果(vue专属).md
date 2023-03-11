[(95条消息) 炫酷的动态粒子背景效果(vue专属)_吴英琦的博客-CSDN博客_vue 炫酷背景](https://blog.csdn.net/weixin_49356003/article/details/117662403?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-4-117662403-blog-107782737.pc_relevant_multi_platform_whitelistv2_ad_hc&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-4-117662403-blog-107782737.pc_relevant_multi_platform_whitelistv2_ad_hc)

# 一，下载插件

在项目的跟目录里打开cmd命令窗口输入

```
npm i vue-particles -s
```

# 二，挂载插件

在main.js里写入

```
import VueParticles from 'vue-particles'
Vue.use(VueParticles)
```

# 三，使用插件

在组件里写入
```html
<vue-particles 
	class="login-bg" 
	color="#f4f4f4"//粒子的颜色 
	:particleOpacity="0.7" 
	:particlesNumber="100" 
	shapeType="circle" 
	:particleSize="4" 
	linesColor="#f4f4f4"//粒子线的颜色 
	:linesWidth="1" 
	:lineLinked="true"
	:lineOpacity="0.4" 
	:linesDistance="150" 
	:moveSpeed="3" 
	:hoverEffect="true"
	hoverMode="grab" 
	:clickEffect="true" 
	clickMode="push" 
/>
```
<vue-particles class="login-bg" color="#f4f4f4"//粒子的颜色 :particleOpacity="0.7" :particlesNumber="100" shapeType="circle" :particleSize="4" linesColor="#f4f4f4"//粒子线的颜色 :linesWidth="1" :lineLinked="true" :lineOpacity="0.4" :linesDistance="150" :moveSpeed="3" :hoverEffect="true" hoverMode="grab" :clickEffect="true" clickMode="push" />

属性说明：

color: String类型。默认'#dedede'。粒子颜色。 particleOpacity: Number类型。默认0.7。粒子透明度。 particlesNumber: Number类型。默认80。粒子数量。 shapeType: String类型。默认'circle'。可用的粒子外观类型有："circle","edge","triangle", "polygon","star"。 particleSize: Number类型。默认80。单个粒子大小。 linesColor: String类型。默认'#dedede'。线条颜色。 linesWidth: Number类型。默认1。线条宽度。 lineLinked: 布尔类型。默认true。连接线是否可用。 lineOpacity: Number类型。默认0.4。线条透明度。 linesDistance: Number类型。默认150。线条距离。 moveSpeed: Number类型。默认3。粒子运动速度。 hoverEffect: 布尔类型。默认true。是否有hover特效。 hoverMode: String类型。默认true。可用的hover模式有: "grab", "repulse", "bubble"。 clickEffect: 布尔类型。默认true。是否有click特效。 clickMode: String类型。默认true。可用的click模式有: "push", "remove", "repulse", "bubble"。