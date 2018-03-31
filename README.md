# Sunset

# 制作简单太阳系

 ## 1.制作太阳系预制
     由于行星大多数都是属于球体，所以我们要新建一个球，新建的方法如下：
![](https://img-blog.csdn.net/20170404150919138?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWpsX1JpY2hhcmQ=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
    在场景中创建1个太阳和8大行星，然后将它们分别命名。8大行星的排列顺序是：水星、金星、地球、火星、木星、土星、天王星、海王星.然后将它们延X轴依次排列开，这样做的目的是可以很容易知道行星的旋转法线是（0，Y，Z），因此要确保行星不在一个法平面上，只需确保Y/Z不相等即可。
![](https://img-blog.csdn.net/20160310134951571?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
  首先在网上搜索太阳系贴图:
![](http://a1.qpic.cn/psb?/V139yGGO0Oh9Ae/xscZZJu01Efxp8nZes2x4DeIMcBog0Xx82xdwOYJ2eM!/b/dEABAAAAAAAA&ek=1&kp=1&pt=0&bo=iQNBAgAAAAADJ8s!&vuin=1005962058&tm=1522486800&sce=60-2-2&rf=viewer_4&t=5)
    然后就要制作`Material`了。八大行星和月球的`Material`比较简单，而太阳和它们不一样，太阳是一个恒星，它本身可以发光，这才照亮了太阳系中其他天体。所以在太阳的`Material`中，我们修改其`Shader`为如图所示的`Self-Illumin`，即自发光.
    然后，你只需要把Materials里面的地球贴图拖到你要的球体上,最后得到一下结果：
![](http://m.qpic.cn/psb?/V139yGGO0Oh9Ae/8314qSFAJjFoLANFbFjVXh9SdbmC1Kp*GOgQ8IOUonE!/b/dEIBAAAAAAAA&bo=0wOYAAAAAAADB2o!&rf=viewer_4&t=5)
     unity上显示如图：
![](http://m.qpic.cn/psb?/V139yGGO0Oh9Ae/srY4I6wdi*XKErZ0SxYRMsRrXyHJuNwHuk2FA*RowSk!/b/dEABAAAAAAAA&bo=rAMMAgAAAAADB4M!&rf=viewer_4&t=5)

## 2.编写代码
     主要使用了Transform对象的RotateAround方法。该方法接受3个参数，第一个是围绕的旋转点，在这里即太阳的位置，第二个是旋转的法向量，在这里法向量在（0，Y，Z）平面上，第三个是旋转的速度。为了方便设置旋转中心和速度。
    为了让行星运行的轨迹显现出来，可以给每个行星添加足迹组件（effects->trailer render）
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class sunset : MonoBehaviour
{
    public Transform sun;
    public Transform mercury;
    public Transform venus;
    public Transform earth;
    public Transform mars;
    public Transform jupiter;
    public Transform saturn;
    public Transform uranus;
    public Transform neptune;
    public Transform moon;
    // Use this for initialization
    Vector3[] a = new Vector3[9];
    float speed = 40;
    float y, z;
    void Start()
    {
        int i = 0;
        for (i = 0; i < 9; i++)
        {
            y = Random.Range(1, 360); // 随机设置角度
            z = Random.Range(1, 360); // 随机设置角度
            a[i] = new Vector3(0, y, z); // 以上是为了制造不同的运动法平面，修改y和z可以使得绕不同的轴转
        }
    }

    // Update is called once per frame
    void Update()
    { // 每个星球的旋转动作，用到了初始化的a[i]
        mercury.RotateAround(sun.position, a[0], speed * Time.deltaTime);
        mercury.Rotate(Vector3.up * speed * Time.deltaTime);
        venus.RotateAround(sun.position, a[1], speed * Time.deltaTime);
        venus.Rotate(Vector3.up * speed * Time.deltaTime);
        earth.RotateAround(sun.position, a[2], speed * Time.deltaTime);
        earth.Rotate(Vector3.up * speed * Time.deltaTime);
        mars.RotateAround(sun.position, a[3], speed * Time.deltaTime);
        mars.Rotate(Vector3.up * speed * Time.deltaTime);
        jupiter.RotateAround(sun.position, a[4], speed * Time.deltaTime);
        jupiter.Rotate(Vector3.up * speed * Time.deltaTime);
        saturn.RotateAround(sun.position, a[5], speed * Time.deltaTime);
        saturn.Rotate(Vector3.up * speed * Time.deltaTime);
        uranus.RotateAround(sun.position, a[6], speed * Time.deltaTime);
        uranus.Rotate(Vector3.up * speed * Time.deltaTime);
        neptune.RotateAround(sun.position, a[7], speed * Time.deltaTime);
        neptune.Rotate(Vector3.up * speed * Time.deltaTime);
        moon.RotateAround(earth.position, Vector3.right, 400 * Time.deltaTime);
    }
}
```
    把这个文件挂载在sun上面，然后将各个行星拖入
![](http://a2.qpic.cn/psb?/V139yGGO0Oh9Ae/gNBZDtDlJHNNKNZ0NaWELvnxkPLQugO2tJBG7vqK9t4!/b/dEEBAAAAAAAA&ek=1&kp=1&pt=0&bo=JwIJAQAAAAADFx8!&vuin=1005962058&tm=1522486800&sce=60-1-1&rf=viewer_4&t=5)
     接下来就可以运行了，下图是运行结果：
![](http://a3.qpic.cn/psb?/V139yGGO0Oh9Ae/7nPlLtyy3guzHETAeTMF4cEIR32Yie87rWvzN*lr5tU!/b/dEIBAAAAAAAA&ek=1&kp=1&pt=0&bo=EwJoAQAAAAADF0o!&vuin=1005962058&tm=1522486800&sce=60-1-1&rf=viewer_4&t=5)
