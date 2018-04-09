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


# 魔鬼与牧师
## 游戏规则如下
![](https://img-blog.csdn.net/2018040313161429)
## 下面是我的代码

FirstController
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Com.Mygame;

public class FirstController : MonoBehaviour, SceneController, UserAction {

	readonly Vector3 water_pos = new Vector3(0,0.5F,0);


	UserGUI userGUI;

	public CoastController fromCoast;
	public CoastController toCoast;
	public BoatController boat;
	private MyCharacterController[] characters;

	void Awake() {
		Director director = Director.getInstance ();
		director.currentSceneController = this;
		userGUI = gameObject.AddComponent <UserGUI>() as UserGUI;
		characters = new MyCharacterController[6];
		loadResources ();
	}

	public void loadResources() {
		GameObject water = Instantiate (Resources.Load ("Perfabs/Water", typeof(GameObject)), water_pos, Quaternion.identity, null) as GameObject;
		water.name = "water";

		fromCoast = new CoastController ("from");
		toCoast = new CoastController ("to");
		boat = new BoatController ();

		loadCharacter ();
	}

	private void loadCharacter() {
		for (int i = 0; i < 3; i++) {
			MyCharacterController cha = new MyCharacterController ("priest");
			cha.setName("priest" + i);
			cha.setPosition (fromCoast.getEmptyPosition ());
			cha.getOnCoast (fromCoast);
			fromCoast.getOnCoast (cha);

			characters [i] = cha;
		}

		for (int i = 0; i < 3; i++) {
			MyCharacterController cha = new MyCharacterController ("devil");
			cha.setName("devil" + i);
			cha.setPosition (fromCoast.getEmptyPosition ());
			cha.getOnCoast (fromCoast);
			fromCoast.getOnCoast (cha);

			characters [i+3] = cha;
		}
	}


	public void moveBoat() {
		if (boat.isEmpty ())
			return;
		boat.Move ();
		userGUI.status = check_game_over ();
	}

	public void characterIsClicked(MyCharacterController characterCtrl) {
		if (characterCtrl.isOnBoat ()) {
			CoastController whichCoast;
			if (boat.get_to_or_from () == -1) { // to->-1; from->1
				whichCoast = toCoast;
			} else {
				whichCoast = fromCoast;
			}

			boat.GetOffBoat (characterCtrl.getName());
			characterCtrl.moveToPosition (whichCoast.getEmptyPosition ());
			characterCtrl.getOnCoast (whichCoast);
			whichCoast.getOnCoast (characterCtrl);

		} else {									// character on coast
			CoastController whichCoast = characterCtrl.getCoastController ();

			if (boat.getEmptyIndex () == -1) {		// boat is full
				return;
			}

			if (whichCoast.get_to_or_from () != boat.get_to_or_from ())	// boat is not on the side of character
				return;

			whichCoast.getOffCoast(characterCtrl.getName());
			characterCtrl.moveToPosition (boat.getEmptyPosition());
			characterCtrl.getOnBoat (boat);
			boat.GetOnBoat (characterCtrl);
		}
		userGUI.status = check_game_over ();
	}

	int check_game_over() {	// 0->not finish, 1->lose, 2->win
		int from_priest = 0;
		int from_devil = 0;
		int to_priest = 0;
		int to_devil = 0;

		int[] fromCount = fromCoast.getCharacterNum ();
		from_priest += fromCount[0];
		from_devil += fromCount[1];

		int[] toCount = toCoast.getCharacterNum ();
		to_priest += toCount[0];
		to_devil += toCount[1];

		if (to_priest + to_devil == 6)		// win
			return 2;

		int[] boatCount = boat.getCharacterNum ();
		if (boat.get_to_or_from () == -1) {	// boat at toCoast
			to_priest += boatCount[0];
			to_devil += boatCount[1];
		} else {	// boat at fromCoast
			from_priest += boatCount[0];
			from_devil += boatCount[1];
		}
		if (from_priest < from_devil && from_priest > 0) {		// lose
			return 1;
		}
		if (to_priest < to_devil && to_priest > 0) {
			return 1;
		}
		return 0;			// not finish
	}

	public void restart() {
		boat.reset ();
		fromCoast.reset ();
		toCoast.reset ();
		for (int i = 0; i < characters.Length; i++) {
			characters [i].reset ();
		}
	}
}
```

UserGUI
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Com.Mygame;

public class UserGUI : MonoBehaviour {
	private UserAction action;
	public int status = 0;
	GUIStyle style;
	GUIStyle buttonStyle;

	void Start() {
		action = Director.getInstance ().currentSceneController as UserAction;

		style = new GUIStyle();
		style.fontSize = 40;
		style.alignment = TextAnchor.MiddleCenter;

		buttonStyle = new GUIStyle("button");
		buttonStyle.fontSize = 30;
	}
	void OnGUI() {
		if (status == 1) {
			GUI.Label(new Rect(Screen.width/2-50, Screen.height/2-85, 100, 50), "Gameover!", style);
			if (GUI.Button(new Rect(Screen.width/2-70, Screen.height/2, 140, 70), "Restart", buttonStyle)) {
				status = 0;
				action.restart ();
			}
		} else if(status == 2) {
			GUI.Label(new Rect(Screen.width/2-50, Screen.height/2-85, 100, 50), "You win!", style);
			if (GUI.Button(new Rect(Screen.width/2-70, Screen.height/2, 140, 70), "Restart", buttonStyle)) {
				status = 0;
				action.restart ();
			}
		}
	}
}
```
ClickGUI
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Com.Mygame;

public class ClickGUI : MonoBehaviour {
	UserAction action;
	MyCharacterController characterController;

	public void setController(MyCharacterController characterCtrl) {
		characterController = characterCtrl;
	}

	void Start() {
		action = Director.getInstance ().currentSceneController as UserAction;
	}

	void OnMouseDown() {
		if (gameObject.name == "boat") {
			action.moveBoat ();
		} else {
			action.characterIsClicked (characterController);
		}
	}
}
```
BaseCode
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Com.Mygame;

namespace Com.Mygame {
	
	public class Director : System.Object {
		private static Director _instance;
		public SceneController currentSceneController { get; set; }

		public static Director getInstance() {
			if (_instance == null) {
				_instance = new Director ();
			}
			return _instance;
		}
	}

	public interface SceneController {
		void loadResources ();
	}

	public interface UserAction {
		void moveBoat();
		void characterIsClicked(MyCharacterController characterCtrl);
		void restart();
	}

	/*-----------------------------------Moveable------------------------------------------*/
	public class Moveable: MonoBehaviour {
		
		readonly float move_speed = 20;

		// change frequently
		int moving_status;	// 0->not moving, 1->moving to middle, 2->moving to dest
		Vector3 dest;
		Vector3 middle;

		void Update() {
			if (moving_status == 1) {
				transform.position = Vector3.MoveTowards (transform.position, middle, move_speed * Time.deltaTime);
				if (transform.position == middle) {
					moving_status = 2;
				}
			} else if (moving_status == 2) {
				transform.position = Vector3.MoveTowards (transform.position, dest, move_speed * Time.deltaTime);
				if (transform.position == dest) {
					moving_status = 0;
				}
			}
		}
		public void setDestination(Vector3 _dest) {
			dest = _dest;
			middle = _dest;
			if (_dest.y == transform.position.y) {	// boat moving
				moving_status = 2;
			}
			else if (_dest.y < transform.position.y) {	// character from coast to boat
				middle.y = transform.position.y;
			} else {								// character from boat to coast
				middle.x = transform.position.x;
			}
			moving_status = 1;
		}

		public void reset() {
			moving_status = 0;
		}
	}


	/*-----------------------------------MyCharacterController------------------------------------------*/
	public class MyCharacterController {
		readonly GameObject character;
		readonly Moveable moveableScript;
		readonly ClickGUI clickGUI;
		readonly int characterType;	// 0->priest, 1->devil

		// change frequently
		bool _isOnBoat;
		CoastController coastController;


		public MyCharacterController(string which_character) {
			
			if (which_character == "priest") {
				character = Object.Instantiate (Resources.Load ("Perfabs/Priest", typeof(GameObject)), Vector3.zero, Quaternion.identity, null) as GameObject;
				characterType = 0;
			} else {
				character = Object.Instantiate (Resources.Load ("Perfabs/Devil", typeof(GameObject)), Vector3.zero, Quaternion.identity, null) as GameObject;
				characterType = 1;
			}
			moveableScript = character.AddComponent (typeof(Moveable)) as Moveable;

			clickGUI = character.AddComponent (typeof(ClickGUI)) as ClickGUI;
			clickGUI.setController (this);
		}

		public void setName(string name) {
			character.name = name;
		}

		public void setPosition(Vector3 pos) {
			character.transform.position = pos;
		}

		public void moveToPosition(Vector3 destination) {
			moveableScript.setDestination(destination);
		}

		public int getType() {	// 0->priest, 1->devil
			return characterType;
		}

		public string getName() {
			return character.name;
		}

		public void getOnBoat(BoatController boatCtrl) {
			coastController = null;
			character.transform.parent = boatCtrl.getGameobj().transform;
			_isOnBoat = true;
		}

		public void getOnCoast(CoastController coastCtrl) {
			coastController = coastCtrl;
			character.transform.parent = null;
			_isOnBoat = false;
		}

		public bool isOnBoat() {
			return _isOnBoat;
		}

		public CoastController getCoastController() {
			return coastController;
		}

		public void reset() {
			moveableScript.reset ();
			coastController = (Director.getInstance ().currentSceneController as FirstController).fromCoast;
			getOnCoast (coastController);
			setPosition (coastController.getEmptyPosition ());
			coastController.getOnCoast (this);
		}
	}

	/*-----------------------------------CoastController------------------------------------------*/
	public class CoastController {
		readonly GameObject coast;
		readonly Vector3 from_pos = new Vector3(9,1,0);
		readonly Vector3 to_pos = new Vector3(-9,1,0);
		readonly Vector3[] positions;
		readonly int to_or_from;	// to->-1, from->1

		// change frequently
		MyCharacterController[] passengerPlaner;

		public CoastController(string _to_or_from) {
			positions = new Vector3[] {new Vector3(6.5F,2.25F,0), new Vector3(7.5F,2.25F,0), new Vector3(8.5F,2.25F,0), 
				new Vector3(9.5F,2.25F,0), new Vector3(10.5F,2.25F,0), new Vector3(11.5F,2.25F,0)};

			passengerPlaner = new MyCharacterController[6];

			if (_to_or_from == "from") {
				coast = Object.Instantiate (Resources.Load ("Perfabs/Stone", typeof(GameObject)), from_pos, Quaternion.identity, null) as GameObject;
				coast.name = "from";
				to_or_from = 1;
			} else {
				coast = Object.Instantiate (Resources.Load ("Perfabs/Stone", typeof(GameObject)), to_pos, Quaternion.identity, null) as GameObject;
				coast.name = "to";
				to_or_from = -1;
			}
		}

		public int getEmptyIndex() {
			for (int i = 0; i < passengerPlaner.Length; i++) {
				if (passengerPlaner [i] == null) {
					return i;
				}
			}
			return -1;
		}

		public Vector3 getEmptyPosition() {
			Vector3 pos = positions [getEmptyIndex ()];
			pos.x *= to_or_from;
			return pos;
		}

		public void getOnCoast(MyCharacterController characterCtrl) {
			int index = getEmptyIndex ();
			passengerPlaner [index] = characterCtrl;
		}

		public MyCharacterController getOffCoast(string passenger_name) {	// 0->priest, 1->devil
			for (int i = 0; i < passengerPlaner.Length; i++) {
				if (passengerPlaner [i] != null && passengerPlaner [i].getName () == passenger_name) {
					MyCharacterController charactorCtrl = passengerPlaner [i];
					passengerPlaner [i] = null;
					return charactorCtrl;
				}
			}
			Debug.Log ("cant find passenger on coast: " + passenger_name);
			return null;
		}

		public int get_to_or_from() {
			return to_or_from;
		}

		public int[] getCharacterNum() {
			int[] count = {0, 0};
			for (int i = 0; i < passengerPlaner.Length; i++) {
				if (passengerPlaner [i] == null)
					continue;
				if (passengerPlaner [i].getType () == 0) {	// 0->priest, 1->devil
					count[0]++;
				} else {
					count[1]++;
				}
			}
			return count;
		}

		public void reset() {
			passengerPlaner = new MyCharacterController[6];
		}
	}

	/*-----------------------------------BoatController------------------------------------------*/
	public class BoatController {
		readonly GameObject boat;
		readonly Moveable moveableScript;
		readonly Vector3 fromPosition = new Vector3 (5, 1, 0);
		readonly Vector3 toPosition = new Vector3 (-5, 1, 0);
		readonly Vector3[] from_positions;
		readonly Vector3[] to_positions;

		// change frequently
		int to_or_from; // to->-1; from->1
		MyCharacterController[] passenger = new MyCharacterController[2];

		public BoatController() {
			to_or_from = 1;

			from_positions = new Vector3[] { new Vector3 (4.5F, 1.5F, 0), new Vector3 (5.5F, 1.5F, 0) };
			to_positions = new Vector3[] { new Vector3 (-5.5F, 1.5F, 0), new Vector3 (-4.5F, 1.5F, 0) };

			boat = Object.Instantiate (Resources.Load ("Perfabs/Boat", typeof(GameObject)), fromPosition, Quaternion.identity, null) as GameObject;
			boat.name = "boat";

			moveableScript = boat.AddComponent (typeof(Moveable)) as Moveable;
			boat.AddComponent (typeof(ClickGUI));
		}


		public void Move() {
			if (to_or_from == -1) {
				moveableScript.setDestination(fromPosition);
				to_or_from = 1;
			} else {
				moveableScript.setDestination(toPosition);
				to_or_from = -1;
			}
		}

		public int getEmptyIndex() {
			for (int i = 0; i < passenger.Length; i++) {
				if (passenger [i] == null) {
					return i;
				}
			}
			return -1;
		}

		public bool isEmpty() {
			for (int i = 0; i < passenger.Length; i++) {
				if (passenger [i] != null) {
					return false;
				}
			}
			return true;
		}

		public Vector3 getEmptyPosition() {
			Vector3 pos;
			int emptyIndex = getEmptyIndex ();
			if (to_or_from == -1) {
				pos = to_positions[emptyIndex];
			} else {
				pos = from_positions[emptyIndex];
			}
			return pos;
		}

		public void GetOnBoat(MyCharacterController characterCtrl) {
			int index = getEmptyIndex ();
			passenger [index] = characterCtrl;
		}

		public MyCharacterController GetOffBoat(string passenger_name) {
			for (int i = 0; i < passenger.Length; i++) {
				if (passenger [i] != null && passenger [i].getName () == passenger_name) {
					MyCharacterController charactorCtrl = passenger [i];
					passenger [i] = null;
					return charactorCtrl;
				}
			}
			Debug.Log ("Cant find passenger in boat: " + passenger_name);
			return null;
		}

		public GameObject getGameobj() {
			return boat;
		}

		public int get_to_or_from() { // to->-1; from->1
			return to_or_from;
		}

		public int[] getCharacterNum() {
			int[] count = {0, 0};
			for (int i = 0; i < passenger.Length; i++) {
				if (passenger [i] == null)
					continue;
				if (passenger [i].getType () == 0) {	// 0->priest, 1->devil
					count[0]++;
				} else {
					count[1]++;
				}
			}
			return count;
		}

		public void reset() {
			moveableScript.reset ();
			if (to_or_from == -1) {
				Move ();
			}
			passenger = new MyCharacterController[2];
		}
	}
}
```




