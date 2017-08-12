안드로이드는 메인스레드에서 인터넷에 접근하려고 하면 오류를 띄운다
안드로이드 앱은 하나의 UI스레드만을 가진다.
이 스레드는 여러 센서에서 정보를 받아오고 화면에 표시될 다음 프레임을 만들어주죠
메인스레드에서는 최대한 적은 작업을 해야한다.
그러나 네트워크 작업은 몇초 정도 걸릴 수 있는데, 메인스레드를 이용하게 되면 화면이 멈추게 된다.

이게 네트워크 관련 작업은 다른 스레드에서 해야하는 이유이다.
하지만 그러려면 결과값을 다른 스레드에서 가져와서 보여주기 위해 UI를 바꾸어야 하는 문제가 있다.
다행히도 안드로이드는 이런 패턴을 위한 프레임워크인 비동기 작업 Async Takk를 지원한다.

비동기 작업은 백그라운드 스레드에서 작업을 하는 동안에 UI 스레드가 화면을 만들 수 있도록 해줍니다.
UI 스레드에는 다른 프로세스에세 실행가능한 오브젝트나 메시지를 전달할 수 있는 메시지 큐와 핸들러가 존재합니다.
비동기작업은 이러한 과정을 잘 포장해서 직관적으로 만들어져 있다.
비동기작업은 제네릭 클래스.
따라서 생성자에서 매개변수화 타입을 받습니다.
각각의 제네릭 파라미터는 세개의 점이 붙는 JAVA변수화 전달인지가 쓰이는데,
이는 기술적으로 배열을 넘겨 준다는 의미입니다.
비동기작업은 세 개의 타입을 받습니다.
	

	함수 onPreExecute	
	Params : 작업 실행을 위한 파라미터의 타입 / 함수 : doInBackground
	Progress : 백그라운드 작업 진행률을 업데이트 하기 위한 타입 / 함수 : onProgressUpdate
	Reuslt : 백그라운드 작업의 결과값의 타입입니다. / 함수 : onPostExecute

비동기 작업을 백그라운드에서 실행하기 위해서는 파라미터와 함께 Exectue를 호출해주면 됩니다.
그러면 비동기작업이 몇가지 단계를 걸쳐 시작하게 됩니다.

첫번째로 UI스레드에 있는 onPreExecute를 실행해서 백그라운드 작업을 하기 전에 UI 스레드에서 하고 싶은 초기화 작업을 할 수 있게 해줍니다. 

그 다음 그 작업을 할 스레드에서 doInBackground함수를 실행합니다. 
★비동기 작업을 사용할때 이 메소드는 반드시 오버라이드 되어야 합니다.


또한 이 메소드는 Execute를 부를 때 넘겨준 파라미터를 가지고 실행됩니다.

만약 여러분이 오래 걸리는 작업의 중간 결과를 UI에 출력하고 싶다면  publishProgress에 progress파라미터를 주어 호출하면되는데
이것이 UI스레드의 onProgressUpdate가 progress파라미터를 가지고 실행되도록 해줍니다. doinBackground에서 publicshProgress를 원하는 마늠 호출 할 수 있습니다.



정리

URL,Void,String타입을 사용하는 비동기작업인 GithubQueryTask를 메인액티비티의 내부클래스로 만들고
NetworkUtils.getResponseFromHttpUrl메소드를 이용하여 GitHub에 요청을 보내기 위해 doinBackground를 오버라이드합니다.
그 반환 값을 텍스트뷰에 넣기 위해 onPostExectute를 오버라이드 합니다. 마지막으로 makeGtihubSearchQuey함수에서 네트워킹 관련 코드를
수정하여 우리가 만든 비동기 작업을 인스턴스화 하여야 합니다.

마지막으로 doinBackground가 완료되면 결과값을 반환하는데 이때 OnPostExecute함수가 그 결과값과 함께 UI 스레드에서 실행됩니다.
비동기작업은 스레드사이의 스레딩과 메세징을 위한 유용한 추상화(abstractioon)입니다.

UI THREAD에서 실행되는 함수
	
	exectue()
	onPreExecute()
	onProgressUpdate()
	onPostExecute()

Background에서 실행되는 함수
	
	doInBackground()
	publicshProgress()
	

public class GithubQueryTask extends AsyncTask<URL, Void, String> >>> 이 타입에 따라 execute와 doInBackground메소드는
URL을 받고, 작업 중간 진행상황을 보여주지 않을 것이며 비동기 작업의 반환 타입이 문자열이라는 것을 알 수 있다.
